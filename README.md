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

## A. Download.

Either `git clone` the repo to get the latest version of the source or download the latest release from the sidebar.

note(s):

* Unfortunately, because we are using `git submodules` other forms of source download (e.g. the code button in the main github page) do not work.

## B. Usage.

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

## C. Using `git submodules`.

If you want to use the library in your nown mods, you have to include the source.

Another way, is to insert it into the repository itself using `git submodules`, and use git as a makeshift dependency management tool. A tutorial on using git submodules can be found in [Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules), For our purposes, and since we only want to fetch the contents of the repo keeping abreast of the most recent changes, the workflow is pretty simple. From the root dir of your mod:

```bash
git submodule add https://github.com/lambda-dom/weidu_library
git submodule update --init --recursive
```

If you need to update to the latest version, from the dir containing the `weidu_library` (e.g. the root dir of the mod):

```bash
git submodule update --remote weidu_library
```

Unfortunately, git does *not* add the submodule's repo file in a source release, so one has to generate it and then include the generated zip when doing the github release. To generate the zip, we use the python script from [here](https://github.com/Kentzo/git-archive-all). Drop to the root folder of your (local) repo and do:

```bash
python <path to python script> <path to zip>
```

Finally, the usage is now simply:

```weidu
//Set library dir.
OUTER_TEXT_SPRINT library_dir "%MOD_FOLDER%/weidu_library/lib"
```

and you are all set.
