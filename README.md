# weidu_library.

A library of WeiDU functions.

Latest version: v1.0beta1

## A. Libraries.

The library is divided in components. The components are:

* [Arrays](./lib/docs/arrays.md): manipulate arrays.
* [Bits](./lib/docs/bits.md): bit twiddling.
* [Components](./lib/docs/components.md): streamline the installation of mod components.
* [Creatures](./lib/docs/creatures.md): handle creature .cre files.
* [Effects](./lib/docs/effects.md): handle effect .eff files.
* [Items](./lib/docs/items.md): handle item .itm files.
* [Kits](./lib/docs/kits.md): tweak kits and classes.
* [Miscellaneous](./lib/docs/miscellaneous.md): miscellaneous utility functions.
* [Opcode](./lib/docs/opcodes.md): opcode patching.
* [Opcode Arrays](./lib/docs/opcode_arrays.md): a library to process opcodes with associative arrays.
* [Resources](./lib/docs/resources.md): streamline resource installation.
* [Spells](./lib/docs/spells.md): handle spell .spl files.
* [Strings](./lib/docs/strings.md): manipulate strings.
* [Subspells](./lib/docs/subspells.md): high-level library for subspell cloning.
* [Tables](./lib/docs/tables.md): manipulate table 2da files.

## A. Download.

Either `git clone` the repo to get the latest version of the source or download the latest release from the sidebar.

## B. Usage.

For proper usage of the library, the global flag `AUTO_EVAL_STRINGS` *must* be set, e.g. at the top of the main mod's .tp2 file

```
//Flags.
AUTO_EVAL_STRINGS
```
Then just `INCLUDE` the components you want.

One way to set it up, so as to be more robust against renamings and moves, is to have a variable pointing to the components dir and then `INCLUDE "%variable%/component`, e.g. something like this:

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

One important note: the directory where the library components are located is not the root, but the `lib` subdir.

## C. Using `git submodules`.

If you want to use the library in your nown mods, you have to include the source.

Another way, is to insert it into the repository itself using `git submodules`, and use git as a makeshift dependency management tool. A tutorial on using git submodules can be found in [Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules), For our purposes, and since we only want to fetch the contents of the repository keeping abreast of the most recent changes, the workflow is pretty simple. From the root dir of your mod:

```bash
git submodule add https://github.com/lambda-dom/weidu_library
git submodule update --init --recursive
```

If you need to update to the latest version, from the dir containing the `weidu_library` (e.g. the root dir of the mod):

```bash
git submodule update --remote weidu_library
```

Unfortunately, if you use `git submodules` note that github does *not* add the submodule's repository files in a source release, you will have to include the source yourself. To generate a zip including the source of all the included submodules, one can use the python script from [here](https://github.com/Kentzo/git-archive-all). Drop to the root folder of your (local) repo and do:

```bash
python <path to python script> <path to zip>
```

Finally, assuming you do use `git submodules` to include the library, its usage is now:

```weidu
//Set library dir.
OUTER_TEXT_SPRINT library_dir "%MOD_FOLDER%/weidu_library/lib"
```

and you are all set.
