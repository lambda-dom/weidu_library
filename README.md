# weidu_library.

A library of WeiDU functions.

## A. Libraries.

The library is divided in components. The components are:

* [Arrays](./lib/docs/arrays.md): manipulate arrays.
* [Bits](./lib/docs/bits.md): bit twiddling.
* [Components](./lib/docs/components.md): streamline the installation of mod components.
* [Creatures](./lib/docs/creatures.md): handle creature .cre files.
* [Effects](./lib/docs/effects.md): handle effect .eff files.
* [Items](./lib/docs/items.md): handle item .itm files.
* [Kits](./lib/docs/kits.md): tweak kits and classes.
* [Opcode](./lib/docs/opcodes.md): opcode patching.
* [Resources](./lib/docs/resources.md): streamline resource installation.
* [Spells](./lib/docs/spells.md): handle spell .spl files.
* [Strings](./lib/docs/strings.md): manipulate strings.
* [Subspells](./lib/docs/subspells.md): high-level library for subspell cloning.
* [Tables](./lib/docs/tables.md): manipulate table 2da files.

## Usage.

Just `INCLUDE` the components you want. One way to set it up, so as to be more robust against renamings and moves, is to have a variable pointing to the components dir and then `INCLUDE "%variable%/component`, e.g. something like this:

```
//Flags.
AUTO_EVAL_STRINGS

//Preamble.
ALWAYS
    //Set library dir.
    OUTER_TEXT_SPRINT library_dir "weidu_library/lib"
END

//Library includes.
INCLUDE "%library_dir%/components.tpa"
```

Two important notes. First, the directory where the library components are located is not the root, but the `lib` subdir. Second, the flag `AUTO_EVAL_STRINGS` is necessary.
