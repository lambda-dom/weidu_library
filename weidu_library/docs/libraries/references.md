# References.

Library to aid in resource name management, by allowing to use more complex resource references than the standard 8-character strings.

A resource reference, as used in several .2da tables used by installer libraries, has the following regexp format:

```regexp
^#([a-zA-Z0-9][a-zA-Z0-9_-]*):(.+)$
```

The first group, an alpha-numeric identifier, uniquely identifies the function that is to be called, while the second group, is the argument to pass to it. The string it returns is the resource's name. In short, and denoting the first group by `function` and the second by `value`, this is inline notation for the call

```weidu
LAF "%function%" STR_VAR value = "%value% RET resource
```

Each `function` is then free to parse `value` as necessary.

file(s):

* [Source code](../../references.tpa).

# A. Main function.

note(s):
* All functions in this section have patch and action variants.

`get_resource_ref STR_VAR ref RET resource`

This is the main entry point of the library, and parses a `ref` into a function call. In details: parses the string `ref` against the regexp `^#([a-zA-Z0-9][a-zA-Z0-9_-]*):(.+)$` and grabs the extracted function's name and value. If `value` does not match the regexp, the function FAIL's. If it matches, return whatever the return value of the function call:

```weidu
LPF "%function%" STR_VAR value = "%value%" RET return
```

Note the signature of the called function: one argument named `value` and the return value named `return` -- the signature of an encoder. The available formats are detailed in the formats section.

note(s):
* even though the return value is named `resource`, this function can return values other than resource (references).

# B. Formats.

The following functions are the available encoders. There is usually no need to call them directly, rather call them indirectly with a resource ref via `get_resource_ref`.

`encode_ref_literal STR_VAR value RET return`

Treats `value` as a literal resource name and returns it unchanged, except for lower-casing. Format is:

```
#lit:<resource reference>
```

note(s):
* it also checks the length, that is, if length of the resource reference is strictly larger than 8 the function FAIL's.

`encode_spell_res STR_VAR value RET return`

Treats `value` as a symbolic spell reference in `spell.ids` and returns the corresponding resource reference. Function FAIL's if `value` not present in `spell.ids`. Format is:

```
#spl:<spell symbolic reference>
```

note(s):
* Function from [Encoders](./internal/encoders.md).

`encode_missile_res STR_VAR value RET return`

Treats `value` as a symbolic projectile reference in `missile.ids` and returns the corresponding resource reference. Function FAIL's if `value` not present in `spell.ids`. Format is:

```
#lbl:<missile reference>
```

note(s):
* Function from [Encoders](./internal/encoders.md).

`encode_spell_suffix STR_VAR value RET return`

Returns the symbolic spell reference suffixed with the character. For example, e.g. `a:CLERIC_BLESS` returns `sppr101a`. Function FAIL's if `value` not present in `spell.ids`. Format is:

```
#suf:<one alphanumeric character>:<spell symbolic reference>
```

`encode_opcode_type STR_VAR value RET return`

Returns the numeric id of an opcode type. Function FAIL's if `value` not present in [Opcodes table](../../resources/2da/opcodes/types.2da). Format is:

```
#opc:<opcode type>
```

# C. Encoders.

`encode_resource_ref STR_VAR value RET return`

Encoder version of `get_resource_ref`.

`encode_bam_ref STR_VAR value RET return`

`encode_projectile_ref STR_VAR value RET return`
