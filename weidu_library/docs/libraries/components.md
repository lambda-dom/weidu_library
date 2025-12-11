# Components library.

Library streamlining installation of mod components.

file(s):

* [Source code](../../components.tpa)

# A. Installers.

note(s):
* all the functions in this section are action functions.

By convention, all resources should be placed in standard locations, appropriate subdirs of the component's dir. These locations are given by the next set of functions, all relying on the variable `COMPONENT_NAME` being set, e. g. by an `install_component` call.

note(s):
* all the functions in this section have action and patch variants.

`install_component STR_VAR COMPONENT_NAME`

Installs component `COMPONENT_NAME`. First it clears up arrays, unloads included and inlined files, etc. so as to start from a clean slate. Then it starts the real work by doing some minimal checking: `COMPONENT_NAME` must be well-formed (no spaces, lower-cased to play well with linux, etc.), the component's main .tpa and main .tra files must exist. Then it loads the tra file and `INCLUDE`'s the `main.tpa` file.

notes(s):
* because of dynamic scoping, the argument `COMPONENT_NAME` functions as a global variable. In particular, it ought _not_ be set.

# B. Component functions.

`get_component_root RET dir`

Return the (full path of the) root dir of the component. Currently, this is `%MOD_FOLDER%/components/%COMPONENT_NAME%`.

`get_component_main RET file`

Return the (full path of the) main file of the component. Currently, this is `%MOD_FOLDER%/components/%COMPONENT_NAME%/main.tpa`.

`get_component_resources_dir RET dir`

Return the (full path of the) dir of the component's resources dir. Currently, this is `%MOD_FOLDER%/components/%COMPONENT_NAME%/resources`

`get_component_tra_dir RET dir`

Return the (full path of the) dir where the tra files used by the component can be located. Currently, this is `%MOD_FOLDER%/languages/%LANGUAGE%/%COMPONENT_NAME%`.

`get_component_tra_main RET file`

Return the (full path of the) main tra of the component. Currently, this is `%MOD_FOLDER%/languages/%LANGUAGE%/%COMPONENT_NAME%/setup.tra`.

`get_component_external_dir RET dir`

Return the (full path of the) dir where external data is placed. Currently, this is `weidu_external/data/%MOD_FOLDER%/%COMPONENT_NAME%`.

# C. Action functions.

note(s):
* all the functions in this section are action functions.

`install_subcomponent STR_VAR subcomponent tra = "*"`

`INCLUDE` the `subcomponent` file (full path) in its own scope. If `tra` file (full path) is provided, it is a tra file that is loaded before loading the file. It is then automatically unloaded after execution.

note(s):
* the function `CLEAR`'s everything except memory on entry. To be able to chain `install_subcomponent` calls, it re-`INCLUDE`'s the `components` library.

To ensure translations work correctly, pass a tra path like `%MOD_FOLDER%/languages/%LANGUAGE%/<tra file name>`. This can easily be done by composing the `tra` path using `get_component_tra_dir`, e. g. a dance like:

```weidu
LAF get_component_root RET root = dir END
LAF get_component_tra_dir RET dir = dir END

LAF install_subcomponent STR_VAR
    subcomponent = "%root%/subcomponents/subcomponent.tpa"
    tra = "%dir%/subcomponent.tra"
END
```
