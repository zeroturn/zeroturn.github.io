Binary Numbers

Let's face it, doesn't it irritate you that computer systems use binary numbers?  Really?  Why not use the decimal system like everyone else?

Computers are nothing but a huge collection of on-off switches.  (OK, that is a bit of a simplification, but stay with me.)  It is the binary number system that gives those switches such power.  Binary is a base 2 number system.  It has 2 digits, `0` and `1` representing the decimal numbers from 0 to 1.  Binary numbers can model the physical state of transistor switches that are either on or off, so long as we agree that the "on" state of the transistor means either `1` or `0` and that the "off" state means the opposite.  Therefore, the binary number system really does make a lot of sense when it comes to computers.

Admit it, you can send a lot of messages with a simple on-off device, such as a flashlight, *if you and the recipient of the messages agree on the meaning of the flashes of light*.  A flash of light may mean that "the British are coming", and the absence of a light otherwise.  In binary, this can be represented as a `1` (light on) or `0` (light off).  More complicated schemes can be devised even with a single "switch."  Even more efficient message passing can  be generated with banks or groups of switches.  The meaning of the messages is limited only by your imagination.  A bank of 10 switches may represent the numbers from one to ten (or zero to nine).  Or those 10 switches might represent 10 "English language messages" such as "stop","go", "proceed with caution", "yield to pedestrians," etc.

All you really need to know is that these switches can be either on or off.  But, if you want a deeper understanding of how the transistor switches in a computer work, visit [this website](http://bbrown.kennesaw.edu/web_lectures/transistors/) which uses animations to clarify what is happening in the electronic circuits.  I highly recommend it.

The binary number system is just like the decimal system.  It describes numbers by using the position of the digit to represent *powers* of the base.  So, for example,

`96201` in decimal means

     9x10^4  +  6x10^3  +  2x10^2   +   0x10^1    +    1

In other words, the '1' (the *least significant digit*) represents the 1's place, the '0' represents the 10's place, the '2' represents the 100's place, the 6 represents the 1000's place and the 9 (the *most significant digit*) represents the 10,000's place.

Likewise,

`10101` in binary means

    1x2^4  +  0x2^3  +  1x2^2  +  0x2^1  +  1

In other words, the number is `16` (i.e., 1x2^4) + `0` (i.e., 0x2^3) + `4` (i.e., 1x2^2) + `0` (i.e., 0x2^1) + `1` or decimal 21.

Binary numbers are often grouped in 4's, for reasons that we will get to shortly.  But consider now the case mentioned above where we observed that 10 switches could represent 10 numbers:

`00 0000 0000`  

These 10 binary digits can actually represent 1024 different numbers (or messages) because each position, moving from right to left, represents an increasing power of 2.  Indeed, we can express all of the digits from 0 to 9 using only 4 binary digits (and have room left over).

    Binary      Decimal      Hexadecimal
    0000    ->    0      ->       0
    0001    ->    1      ->       1
    0010    ->    2      ->       2
    0011    ->    3      ->       3
    0100    ->    4      ->       4
    0101    ->    5      ->       5
    0110    ->    6      ->       6
    0111    ->    7      ->       7
    1000    ->    8      ->       8
    1001    ->    9      ->       9
    1010    ->    10     ->       A
    1011    ->    11     ->       B
    1100    ->    12     ->       C
    1101    ->    13     ->       D
    1110    ->    14     ->       E
    1111    ->    15     ->       F

From the table above, it is clear that we can express the numbers from 0 to 15 with only four transistors (4 binary digits).  We can express 256 numbers or symbols with only 8 transistors (8 binary digits).  For example, with a mere 8 transistors, we can represent all of the decimal digits from 0 to 9, and all of the upper and lower case English alphabet, plus assorted punctuation marks, control characters, and other useful symbols.  All that we must do is use 8 transistors ***and*** agree on what those numbers mean.  Indeed, one of the early agreements of this type was called [ASCII](https://en.wikipedia.org/wiki/ASCII), the American Standard Code for Information Interchange.  Furthermore, so long as we agree on a [*protocol*](https://en.wikipedia.org/wiki/Communications_protocol "a set of rules for sending and receiving messages") for sending *sequences* of symbols, we can express *every word* in the English language and communicate *every sentence* in English that has ever been written, *or will ever be written*, with only 8 transistors.  Impressed?  You should be.

###### Hexadecimal
Ok, you are convinced that the use of binary was actually a good idea.  But what about these hexadecimal numbers?  What gives with them?

Hexadecimal is a base 16 number system.  It has 16 digits, representing the decimal numbers from 0 to 15.  We can use the decimal symbols to do double duty to represent the hexadecimal values from 0 to 9, but we run out of decimal symbols at number 9, so mathematicians had to come up with a few more hexadecimal symbols to represent the decimal numbers 10 - 15.  They could have adopted various "squiggles" but, instead, they rather unimaginatively came up with the "symbols" A, B, C, D, and E to represent those remaining hexadecimal digits greater than 9.  So, the hexadecimal digits range from 0-9 and A-E.

It turns out to be convenient to express binary numbers in hexadecimal.  Computers operate on groups of 8 bits referred to as **bytes**.  As noted above, it is often convenient to split those groups of 8 into two groups of 4.  Each group of 4 bits is referred to as a *nibble* or *nybble*.  A nibble, that is 4 bits, can represent the numbers from decimal 0 to 15.  If you were paying attention earlier, you will have noticed that this is *perfectly suited for hexadecimal* !

Now, the fact of the matter is that it can be difficult to speak or write about binary numbers.  Consider these, for example:

`01100110`, `11100011`, `01010010`, `11111000` 

If these numbers are broken up into nibbles and expressed in hexadecimal notation, they are much easier to speak and write about.  

`01100110` becomes `0110 0110` which becomes `66`;

`11100011` becomes `1110 0011` which becomes `E3`;

`01010010` becomes `0101 0010` which becomes `52`;

`11111000` becomes `1111 1000` which becomes `F8`.

The value of using hexadecimal notation becomes even more apparent when we begin to talk about 16, 32, 64 and 128 bit numbers.  A string of hexadecimal characters is much easier to speak and write about than a string of binary numbers.  For example, it would be much easier to talk about the two 16-bit numbers `0110 0110 1110 1100` and `0101 0010 1111 1000` as hexadecimal `66E3` and `52F8`.[^1]

So there you have it.   Computer engineers were **not** just trying to make life difficult for you.  There really was a reason to use binary and hexadecimal numbers!

[Home Page](/home)

[^1]: The order of these hexadecimal numbers could actually be reversed depending upon the particular computer architecture.  In other words, the two 16-bit numbers might be expressed as **E366** and **F852**, instead of 66E3 and 52F8 respectively, depending upon whether the computer architecture used the *"little endian"* notation or *"big endian"* notation.  *"Endianness"* is beyond the scope of these articles, but more information can be found [here](http://www.cs.umd.edu/class/sum2003/cmsc311/Notes/Data/endian.html) and [here](http://betterexplained.com/articles/understanding-big-and-little-endian-byte-order/).