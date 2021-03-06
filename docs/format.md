# format
## base 255
If you haven't read the doc on base 255, you should read it at `base255.md`. It covers what base 255 is, how to use it, and why it is good in this case. A base 255 number is pointed out in the format definition as `<255>`.
## null
Null is the one `char` value not found in a base 255 "digit". It is used to separate values. A null is found in the format definition as `<\0>`.
## the format
`<255><\0><255><\0>Contents of section<\0>...`

The first `<255>` is the amount of sections in the current virtual file. A single real file can have many virtual files. The first `<\0>` notates the end of the base 255 number. If the virtual file contains no data, the `<255>` can be ommited. The `<\0>` is there regardless.

The second `<255>` is the amount of nulls in the current section. It is preceded by a `<\0>`. The `<255>` can be ommited if the section contains no nulls. The null is written regardless.

The "Contents of section" is the section of the virtual file. It must contain exactly the amount of nulls as described in the second `<255>`. It is preceded by a `<\0>`, which is _not_ notated by the second `<255>`.

There are as many sections as described in the first `<255>`. For each section, there is a `<255>` to determine how many nulls are in the section contents, a `<\0>`, the contents of the section, and then another `<\0>`. After all of the sections are described, the file can end _or_ another virtual file can be initialized.

## examples
In these examples, hex characters such as the first char after the null are notated with a slash and then the hex number, such as `<\01>` or `<\1>` (the same thing).

`<\2><\0><\0>A section<\0><\0>Hello, World!<\0><\1><\0><\1><\0>Hello, Nulls<\0>!<\0>`

This shows -
* Two virtual files, one with two sections and one with one section
* The first virtual file contains the string "A section" and the string "Hello, World!"
* The second virtual file contains the string "Hello, Nulls`<\0>`!", which contains a null.
