# References.

Resource installation is done via tables, but these have a format that implies certain restrinctions in the values (for example, no spaces). This library introduces a tiny dsl to allow more complex expressions.

A *table reference*, as used in several .2da tables used by installer libraries, has the following regexp format:

```regexp
^#([a-zA-Z0-9][a-zA-Z0-9_-]*):(.*)$
```

The first group, an alpha-numeric identifier, uniquely identifies the function that is to be called, while the second group, is the argument to pass to it. The string it returns can be anything, but is usually a string or number that has passed some validation checks. In short, and denoting the first group by `function` and the second by `value`, this is inline notation for the call

```weidu
LAF "%function%" STR_VAR value = "%value% RET resource
```

Each `function` is free to parse `value` as necessary.

file(s):

* [Source code](../../references.tpa).

# A. Main function.

note(s):
* All functions in this section have patch and action variants.

`encode_table_reference STR_VAR value RET return`

This is the main entry point of the library, and parses a `ref` into a function call. In details: parses the string `ref` against the regexp `^#([a-zA-Z0-9][a-zA-Z0-9_-]*):(.*)$` and grabs the extracted function's name and the argument value. If `ref` does not match the regexp, the function FAIL's. If it matches, lookup the name in a table of `name => function` pairs and return whatever the function call returns:

```weidu
LPF "%function%" STR_VAR value = "%value%" RET return
```

Note the signature of the called function: one argument named `value` and the return value named `return` -- the signature of an *encoder*. The available formats are detailed in the formats section.

# B. Formats.

The following functions are the available encoders. There is usually no need to call them directly, rather call them indirectly with a resource ref via `encode_table_reference`.

## B. 1. String formats.

`encode_resource_literal STR_VAR value RET return`

Treats `value` as a literal and returns it unchanged, except for upper-casing. Format is:

```
#lit:<resource reference>
```

note(s):
* it also checks the length, that is, if length of the resource reference is strictly larger than 8 the function FAIL's.

`encode_empty_string STR_VAR value RET return`

Returns the empty string. Format is:

```
#nul:
```

Note that value is the empty string; if anything follows the colon, the function FAIL's.

## B. 2. Numeric formats.

`encode_int_literal STR_VAR value RET return`

Treats `value` as an integer literal and returns it. Format is:

```
#num:<numeric literal>
```

Both decimal and hex literals are accepted.

note(s):
* this is useful mainly if the values in a given column can be either numbers or some other kind of object, and this provides a way to disambiguate. If all values must be integers (as checked by the table processing code) there is little point in using this format. One use case is the [Blocks library](./blocks.md) where the column values can have various interpretations depending on the value of another column (e.g. this is a (very) primitive form of dependent typing).

## B. 3. Spell-related formats.

`encode_spell_res STR_VAR value RET return`

Treats `value` as a symbolic spell reference in `spell.ids` and returns the corresponding resource reference. Function FAIL's if `value` not present in `spell.ids`. Format is:

```
#spl:<spell symbolic reference>
```

`encode_spell_suffix STR_VAR value RET return`

Returns the symbolic spell reference suffixed with the character. For example, e.g. `a:CLERIC_BLESS` returns `sppr101a`. Function FAIL's if the spell symbol (last component) not present in `spell.ids`. Format is:

```
#suf:<one alphanumeric character>:<spell symbolic reference>
```

`encode_spell_affix STR_VAR value RET return`

Returns the symbolic spell reference suffixed with a character and the first two characters relaced by the affix. For example, e.g. `dv:a:CLERIC_BLESS` returns `dvpr101a`. Function FAIL's if the spell symbol (last component) not present in `spell.ids`. Format is:

```
#afx:<two alphanumeric characters>:<one alphanumeric character>:<spell symbolic reference>
```

## B. 4. Projectile-related formats.

`encode_missile_res STR_VAR value RET return`

Treats `value` as a symbolic projectile reference in `missile.ids` and returns the corresponding resource reference. Function FAIL's if `value` not present in `spell.ids`. Format is:

```
#lbl:<missile reference>
```

note(s):
* Function from [Encoders](./internal/encoders.md).

## B. 5. Opcode-related formats.

`encode_opcode_type STR_VAR value RET return`

Returns the numeric id of an opcode type. Function FAIL's if `value` not present in [Opcodes table](../../resources/2da/opcodes/types.2da). Format is:

```
#opc:<opcode type>
```

## B. 6. Sectype-related formats.

`encode_spell_sectype STR_VAR value RET return`

Returns the numeric id of a sectype. Function FAIL's if `value` is not a valid sectype. Associated format is:

```
#sct:<sectype>
```

# C. Other resource encoders.

The next set of encoders have no format associated and are mainly used as value sanitizers.

`encode_bam_ref STR_VAR value RET return`

`encode_projectile_ref STR_VAR value RET return`

`encode_script_ref STR_VAR value RET return`

`encode_dialog_ref STR_VAR value RET return`

These encoders parse a resource reference for a resource of the apprpriate type, do an extra existence check and return the value.
