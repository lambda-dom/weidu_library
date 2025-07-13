# Libraries.

Top-level libraries:

* [Components](./libraries/components.md): streamline the installation of mod components.

High-level libraries:

* [Installers](./libraries/installers.md): library to install various kinds of resources.
* [Kits](./libraries/kits.md): library to patch classes and kits.
* [HLAs](./libraries/hlas.md): library to patch hla tables.

Support libraries: libraries providing basic functionality supporting everything else.

* [2da](./libraries/2da.md): functions to search and patch through .2da table files.
* [Arrays](./libraries/arrays.md): manipulate (associative) arrays.
* [Creatures](./libraries/creatures.md): handle creature .cre files.
* [Effects](./libraries/effects.md): handle effect .eff files.
* [Generic](./libraries/generic.md): generic reader and writer using relative offset tables.
* [Ids](./libraries/ids.md): functions for getting values out of .ids files.
* [Items](./libraries/items.md): handle item .itm files.
* [Lists](./libraries/lists.md): manipulate lists.
* [Opcodes](./libraries/opcodes.md): opcode patching.
* [Projectiles](./libraries/projectiles.md): handle projectile .pro files.
* [References](./libraries/references.md): inline resource references, especially in installer tables.
* [Spells](./libraries/spells.md): handle spell .spl files.
* [Strings](./libraries/strings.md): string manipulation functions.
* [Tables](./libraries/tables.md): construct and manipulate tables.

Internal libraries: internal libraries, usually low-level, that are not part of the public API. 

* [Binary](./libraries/internal/binary.md): library of binary readers and writers.
* [Encoders](./libraries/internal/encoders.md): library of encoders.
* [Patchers](./libraries/internal/patchers.md): library of patchers of all kinds.
