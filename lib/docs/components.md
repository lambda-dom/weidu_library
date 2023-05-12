# Components library.

This library streamlines installation of mod components.

## A. Component functions.

note(s):
* all the functions in this section are action functions.

`load_component STR_VAR component tra = "*"`

Installs a component. First it clears up arrays, unloads included and inlined files, etc. so as to start from a clean slate. Then it starts the real work by doing some minimal checking: the component's name must be well-formed (no spaces, lower-cased to play well with linux, etc.) and the component's main file `main.tpa` must exist. Then it sets some variables:
* `component`: component's name.
* `component_dir`: component's root directory.
* `component_resources_dir`: the component's root resources dir, defaulting to `%component_dir%/resources`.
* `component_tra_file`: the component's tra file, an empty stub file if one is not provided in `tra`. This file (*no* .tra extension) is looked up in `%MOD_FOLDER%/languages/%LANGUAGE%/%component%`.

The function then loads the component's tra file and inside this tra scope, it `INCLUDE`'s the component's main file `main.tpa`.

## B. Utility functions.

note(s):
* unless said otherwise, all functions in this section are action functions.

`load_file STR_VAR file dir = "*" tra = "*"`

`INCLUDE` the `file` located at `dir` in its own scope. If dir (relative to the `%MOD_FOLDER%`) not provided then it searches for file in the `lib` dir of the current component. If `tra` (no .tra extension) is provided, it is a tra file that is loaded before loading the file. It is then automatically unloaded after execution. This file is looked up in `%MOD_FOLDER%/languages/%LANGUAGE%/components/%component%`.

## C. Basic resource install functions.

note(s):
* all the functions in this section are action functions.

`copy_resource INT_VAR override = 1 STR_VAR resource ext dest = "*" dir = "*" patch = "*"`

Copies `resource` to the game folder with extension `ext` identifying the resource's type. If `dest` is not provided, it is `resource`. If the `override` flag is 0, it checks first if an equally named resource already exists in-game and if it does, the function FAIL's. If the `override` flag is 1 (the default) copying proceeds as usual. The default `dir` is the mod's resources folder in standardized folder structure. The argument `patch` is the name of a patch function to call and it must be in scope if provided. No arguments are passed to the patch function.

`clone_resource STR_VAR resource ext dest patch = "*"`

Clones existing resource `resource` with extension `ext` as `dest` (*same* extension) and patches it with `patch`. The argument `patch` is the name of a patch function to call and it must be in scope if provided. No arguments are passed to the patch function. The function will FAIL if a similarly named resource already exists in game.
