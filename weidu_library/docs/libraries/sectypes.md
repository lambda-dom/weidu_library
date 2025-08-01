# The Sectypes library.

A library to handle the processing (addition, editing, etc.) of sectypes.

file(s):

* [Source code](../../sectypes.tpa).

# A. Basic getters.

`patch_get_sectype_id STR_VAR sectype RET id`

Getter for `msectype.2da`: get the `id` of the `sectype` , -1 if `sectype` not valid. This is a patch function.

`get_sectype_id STR_VAR sectype RET id`

Get the `id` of the `sectype` , -1 if `sectype` not valid. This is both a patch and action function.

note(s):
* Each call to this function requires opening `msectype.2da` and perform a linear search. If the calls can be batched, use `patch_get_sectype_id STR_VAR sectype RET id` instead.

# B. Sectype addition.

note(s):
* all functions in this section are both patch and action functions.

`add_sectype INT_VAR tra_ref STR_VAR sectype RET id`

A wrapper around the `ADD_SECTYPE` WeiDU macro. Add `sectype` with `tra_ref` associated removal string and return the corresponding numeric id.

`add_sectypes STR_VAR table tra = "*"`

Batch addition of sectypes using `table`. The table must conform to [Template Sectype Addition](../../resources/2da/sectypes/sectypes.2da)
