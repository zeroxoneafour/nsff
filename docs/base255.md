# base 255
## why base 255?
If 255 sounds especially odd to you as a developer, that's because, well, it is. You probably know the number 256, an 8 binary bit number, also known as a byte or a `char`. Integers (a C `int`) could be said to be 4 digit base 256 numbers on a 32-bit system, or 8 digit base 256 numbers on a 64-bit system.  
A `char` is 8 bits long, so it has 256 possible combinations. According to `format.md`, the null character is used to separate sections of the files. So, we use every character _but_ the null character. This results in each "char" having 255 possible combinations.

## how is this implemented?
Take a `char` and convert it to an `int`. It will be a number between 0 and 255, or 256 values. Subtract one from whatever that value is. It will kick the 0 (null) out of the positive number system and leave 255 numbers, between 0 and 254. This is one digit of our base 255, and does not include null, a character we need for other purposes.

## How much data can this format store?
Normally, a 8-byte (8 digit) base 10 number can store 100 million numbers. An 8-byte integer can store about 18 quintillion (billion billion) numbers. An 8-byte base 255 number can store around 568 quadrillion numbers less, but that still rounds up to 18 quintillion.
