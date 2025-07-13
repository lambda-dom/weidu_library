# weidu_library.

A library of WeiDU functions.

# A. Usage.

## A. 1. Download.

Either `git clone` the repo to get the latest version of the source or download the latest release from the sidebar.

## A. 2. Usage.

For proper usage of the library, two things _must_ be done. First, the global flag `AUTO_EVAL_STRINGS` must be set at the top of the mod's main .tp2 file:

```weidu
//Flags.
AUTO_EVAL_STRINGS
```

Second, the global variable `WEIDU_LIBRARY_DIR` _must_ be set and point to the path where the libraries are located, e.g.:

```weidu
//Flags.
AUTO_EVAL_STRINGS

//Preamble.
ALWAYS
    //Set library dir.
    OUTER_TEXT_SPRINT WEIDU_LIBRARY_DIR "weidu_library/weidu_library"
END
```

Then, to use any specific component just `INCLUDE` it, e.g.:

```weidu
INCLUDE "%WEIDU_LIBRARY_DIR%/spells.tpa"
```

# B. Libraries.

Consult [weidu_library docs](./weidu_library/docs/weidu_library.md) for more details.
