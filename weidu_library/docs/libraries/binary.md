# Formatters.

Low-level library to read and write form binary formats. Most likely, there is a higher-level library to do what is needed.
file(s):

* [Source code](../../binary.tpa)

# A. Generic binary readers.

note(s):
* all functions in this section are patch functions.

`read_byte INT_VAR offset RET value`

`read_short INT_VAR offset RET value`

`read_short_signed INT_VAR offset RET value`

`read_long INT_VAR offset RET value`

`read_long_signed INT_VAR offset RET value`

`read_resource INT_VAR offset RET value`

`read_ascii32 INT_VAR offset RET value`

# B. Generic binary writers.

note(s):
* all functions in this section are patch functions.

`write_byte INT_VAR offset STR_VAR value`

`write_short INT_VAR offset STR_VAR value`

`write_short_signed INT_VAR offset STR_VAR value`

`write_long INT_VAR offset STR_VAR value`

`write_long_signed INT_VAR offset STR_VAR value`

`write_resource INT_VAR offset STR_VAR value`

`write_ascii32 INT_VAR offset STR_VAR value`

note(s):
* the arguments to the writers are passed as strings to standardize the API.
