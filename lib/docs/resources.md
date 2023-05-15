# Resources library.

This library streamlines installation of mod resources. It relies on the conventions set up by the [components library](../components.tpa).

note(s): implementation note:
* since the functions here are all behemoths (for example, the current implementation of `patch_spell` is about 180 LOC, which is a lot -- WeiDU is a *very* verbose language), so they are are segregated to their own files and then `INCLUDE`-ed in the main file.

## A. Spells.

### A. 1. Installers.

note(s):
* all the functions in this section are action functions.

`copy_spells_from_table STR_VAR table patches = "*" tra = "*" subdir = "*"`

Copies spell resources with all the information needed read from `table` (*no extension*). The dir from which the table is read is the component's `resources/2da` dir. The `patches` argument is a library of spell patchers to load; it should be in the component's `lib` folder, that is, `%component_dir%/lib`. If `tra` (no .tra extension) is provided, it is a tra file that is loaded to provide tra references for the patchers. It is then automatically unloaded after execution. This file is looked up in `%MOD_FOLDER%/languages/%LANGUAGE%/components/%component%`. `subdir` is a directory where the spell resources are located; defaults to `%component_resources_dir%/spl`.

The 2da table file must have the following the structure of the [Template Copy Spells Table](../resources/2da/copy_spells_template.2da):

```
2DA V1.0
*
            install name    descr   type    level   flags   school  sectype sound   book_icon   abil_icon   projectile  patch   override    type    id
resource    1       -1      -1      *       -1      *       *       *       *       *           *           *           *       0           *       *
```

The field `install` is a flag to selectively enable or disable installation of a specific spell. The `override` field is a debug flag signaling whether to fail if a same-named resource already exists in-game. The resource's destination name will depend on the last field `id` of the table. If the latter is `*` then the destination is simply the resource; if it is not equal to `*` then it is a symbolic name which either is in `spell.ids` or not. In the first case, this is interpreted as overriding the existing resource, in which case the destination is simply it. If the symbolic name does not exist in `spell.ids` then this means we are adding the spell (via an underlying call to `ADD_SPELL`) in which case the destination name is whatever the `ADD_SPELL` sets it to.

The second field `type` is a symbolic name to use as the type for adding the spell -- this field is used when `id` is not `*`, that is, only when *adding* new spells. When it is not being added, it should be set to `*`. The possible values are (see the [table add_spell_types.2da](../resources/2da/add_spell_types.2da)):

Type    Integer Namespace

priest  1       sppr
wizard  2       spwi
innate  3       spin
class   4       spcl

After this first phase of copying the resource into the game's folder, starts the patching phase. This is done by passing the data fields unchanged to the patcher `patch_spell` -- see its documentation for any specific information for the fields. Finally, the `patch` field is the name of a function to call; the function must be in scope (usually, brought into scope in the `patchers` file) and is called with no arguments. A typical convention is to use `resource` as the function's name.

note(s):
* this final patch call is done after all the initial batch of copying and patching is done and therefore, the patch can assume that the resource already exists in-game and the table data has been patched in.

If you need the name of the resource inside the patch and the spell to patch may have a destination name different from the original name (can happen *only* if `id` is not `*`), use:

```weidu
LPF get_spell_res STR_VAR spell = "%id%" RET resource END
```

where id is the symbolic name of the spell.

note(s): implementation note:
* the correction of self-references is vulnerable to resource renamings. A better way to handle self-references, would be to use a fixed resource reference, e.g. use the convention of the [subspells library](./subspells.md) and use `self#res` as reference to self.

`patch_spells_from_table STR_VAR table patches = "*" tra = "*"`

This is a function analogous to `copy_spells_from_table`, but used to patch existing in-game spell resources. The function arguments, and the structure and meaning of the fields of `table` are virtually identical to that of `copy_spells_from_table` so here we just document the salient differences.

The 2da table file must have the structure of the [Template Paste Spells Table](../resources/2da/paste_spells_template.2da):

```
2DA V1.0
*
            install name    descr   type    level   flags   school  sectype sound   book_icon   abil_icon   projectile  patch
resource    1       -1      -1      *       -1      *       *       *       *       *           *           *           *
```

The fields related to *adding* spells have, naturally enough, been deleted, as well as override. All the other fields have the same meaning as in the `copy_spells_from_table` function. `subdir` is a directory where the spell resources are located; defaults to `%component_resources_dir%/itm`.

### A. 2. Patchers.

note(s):
* all the functions in this section are patch functions.

`set_spell_flags STR_VAR flags`

Sets the spell flags using binary notation, e.g. `LPF set_spell_flags STR_VAR flags = "01010111" END`. There are eight flags that you can set and these are, from left to right (or least-to-most significant) in the argument:
* break invisible
* hostile spell
* outdoors only
* ignore dead magic zones
* ignore wild surges
* can only be cast out of combat
* can target invisible
* can be cast silenced

```
DEFINE_PATCH_FUNCTION patch_spell INT_VAR
    name = 0 - 1
    descr = 0 - 1
    level = 0 - 1
STR_VAR
    type = "*"
    flags = "*"
    school = "*"
    sectype = "*"
    sound = "*"
    book_icon = "*"
    abil_icon = "*"
    projectile = "*"
```

A spell patcher used by `copy_spells_from_table` but that is useful all by itself.

## B. Items.

### B. 1. Installers.

note(s):
* all the functions in this section are action functions.

`copy_items_from_table STR_VAR table = "" patches = "*" tra = "*" subdir = "*"`

Copies item resources with all the information needed read from `table` (*no extension*). The dir from which the table is read is the component's `resources/2da` dir. The `patches` is a library of functions to load; it should be in the component's `lib` folder, that is, `%component_dir%/lib`. If `tra` (no .tra extension) is provided, it is a tra file that is loaded to provide tra references for the patchers. It is then automatically unloaded after execution. As a convenience, the library provides such a tra file for handling unidentified names and descriptions, mostly lifted from [Item Revisions](https://github.com/Gibberlings3/ItemRevisions).

note(s):
* the supplied tra file has tra references in the range 500-999.
* this facility only allows to load one tra file; if you need to load two or more (e.g. the supplied one for handling unidentified strings and your own for the identified ones) you have to orchestrate the loading yourself. One simple possibility is to wrap the `copy_items_from_table` call in a `load_file` call, and use these calls to load the needed tra's.

The 2da table file must have the structure of the [Template Copy Items Table](../resources/2da/copy_items_template.2da):

```
2DA V1.0
*
            install name    descr   id_name id_descr    type    proficiency flags   inventory_icon  ground_icon description_icon    price   stack lore  weight  enchantment  override    patch

resource    1       -1      -1      -1      -1          *       *           *       *               *           *                   -1      -1    -1    -1      -1           0           0
```

The field `install` is a flag to selectively enable or disable installation of a specific spell. The `override` field is a flag used mostly for debugging purposes. It controls whether before copying, a sanity check is made for the existence of an equally named item already exists in game. The `patch` field is the name of a function to call; the function must be in scope (usually, brought into scope in the `patches` file) and is called with no arguments. A typical convention is to use `resource` as the function's name. Note that this final patch call is done after all the initial batch of copying and patching is done and therefore, the patch can assume that the resource already exists in-game and the table data has been patched in.

The other fields are passed to the `patch_item` function.

`patch_items_from_table STR_VAR table = "" patches = "*" tra = "*"`

### B. 2. Patchers.

`set_item_flags STR_VAR flags`

Sets the item flags using binary notation, e.g. `LPF set_spell_flags STR_VAR flags = "0101011100" END`. There are 10 flags available:
* Two-handed
* Cursed
* Magical
* Left-handed
* Silver
* Cold-iron
* Off-handed
* Forbid off-hand
* Undispellable
* Toggle critical aversion

```
patch_item INT_VAR
    name = 0 - 1
    descr = 0 - 1
    id_name = 0 - 1
    id_descr = 0 - 1
    price = 0 - 1
    stack = 0 - 1
    lore = 0 - 1
    weight = 0 - 1
    enchantment = 0 - 1
STR_VAR
    type = "*"
    proficiency = "*"
    flags = "*"
    inventory_icon = "*"
    ground_icon = "*"
    description_icon = "*"
```

A spell patcher used by `copy_spells_from_table` but that is useful all by itself.

## C. Creatures.

### C. 1. Installers.

note(s):
* all the functions in this section are action functions.

`copy_cres_from_table STR_VAR table = "" patches = "*" tra = "*" subdir = "*"` 

Copies item resources with all the information needed read from `table` (*no extension*). The dir from which the table is read is the component's `resources/2da` dir. The `patches` is a library of functions to load; it should be in the component's `lib` folder, that is, `%component_dir%/lib`. `subdir` is a directory where the spell resources are located; defaults to `%component_resources_dir%/cre`.

The 2da table file must have the structure of the [Template Copy Creatures Table](../resources/templates/copy_cre_template.2da):

```
2DA V1.0
*
            install name    str str_ex  dex con int wis chr hps ac  thac0   apr sv_spl  sv_brt  sv_dth  sv_wand sv_ptf  res_fir res_col res_elc res_acd res_mag res_sls res_crs res_prc res_mis patch   override
resource    1       -1      -1  -1      -1  -1  -1  -1  -1  -1  *   -1      -1  *       *       *       *       *       -1      -1      -1      -1      -1      -1      -1      -1      -1      *       0
```

All columns have a more or less evident meaning. The field `install` is a flag to selectively enable or disable installation of a specific spell. The `override` field is a flag used mostly for debugging purposes. It controls whether before copying, a sanity check is made for the existence of an equally named item already exists in game. The `patch` field is the name of a function to call; the function must be in scope (usually, brought into scope in the `patches` file) and is called with no arguments. A typical convention is to use `resource` as the function's name.

All the other fields are passed to the `patch_cre` patcher.

### C. 2. Patchers.

note(s):
* all the functions in this section are patch functions.

```
DEFINE_PATCH_FUNCTION patch_cre INT_VAR
    name = 0 - 1
    str = 0 -1
    str_ex = 0 - 1
    dex = 0 - 1
    con = 0 - 1
    int = 0 - 1
    wis = 0 - 1
    chr = 0 - 1
    hps = 0 - 1
    thac0 = 0 - 1
    apr = 0 - 1
    resist_fire = 0 - 1
    resist_cold = 0 - 1
    resist_electricity = 0 - 1
    resist_acid = 0 - 1
    resist_magic = 0 - 1
    resist_slash = 0 - 1
    resist_crush = 0 - 1
    resist_pierce = 0 - 1
    resist_missile = 0 - 1
STR_VAR
    ac = "*"
    saves_spell = "*"
    saves_breath = "*"
    saves_death = "*"
    saves_wand = "*"
    saves_polymorph = "*"
```

A creature patcher used by `copy_cres_from_table` but that is useful all by itself.

The value of the field `name` is a tra reference used to set both the name and the tooltip of the creature.