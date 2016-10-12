# Floating point numbers
This is an introduction to some of the basic concepts of floating point numbers in the [IEEE 754 floating point standard](https://en.wikipedia.org/wiki/IEEE_floating_point). We will build up to prove some interesting facts about their representation.

Let's start simple. How about a basic refresher on binary numbers (the subscript at the end of a number indicates its base):

### Binary review
*Converting a binary number to decimal:*

![](http://i.imgur.com/DqwdaL4.gif)

*With a binary fraction, we simply continue the pattern:*

![](http://i.imgur.com/Dfr683N.gif)

### The floating point format
Single precision floating point numbers are laid out as follows:


![floating point representation](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d2/Float_example.svg/590px-Float_example.svg.png)

* The 31st bit is the *sign bit*. A value of 0 indicates a positive number. A value of 1 indicates a negative number.
* The next 8 bits (30 through 23) give us the exponent *exp*
* The last 23 bits (22 through 0) give us the *fraction*

There are 32 bits in all.

More succinctly, here is the formula:

![floating point representation](http://i.imgur.com/egmmaZ7.gif)

The first term in the formula gives its sign via the *sign bit*.

The second term in the formula is a binary fraction.

The exponent *exp* is biased by subtracting 127. This allows our biased exponent to take both positive and negative values.

Here are some examples of converting from the the single precision floating point format to a decimal number:
#### Ex1
![](http://i.imgur.com/V81DtAp.gif)

#### Ex2
![](http://i.imgur.com/DrWFdk1.gif)

#### Ex3 (a different way of looking at Ex2)
![](http://i.imgur.com/rEJP6Kb.gif)

In the last step, we simply move the decimal over four places. This is binary scientific notation!

Recall the single precision floating point number formula:

![floating point representation](http://i.imgur.com/egmmaZ7.gif)

We can now see that floating point numbers are essentially represented in binary scientific notation. In particular, floating point numbers are expressed in [normalized scientific notation](https://en.wikipedia.org/wiki/Scientific_notation#Normalized_notation).

In binary scientific notation, all numbers are written in the form
![](http://i.imgur.com/NWcpCim.gif). In normalized binary scientific notation,  the exponent *n* is chosen so that the absolute value of *m* remains at least one but less than two (1 ≤ |*m*| < 2).

With this knowledge, we can prove some interesting facts.

### Floating point representation uniqueness

*Claim:* Every number has a unique representation in the floating point binary format

*Proof:* This follows from the normalized scientific notation representation of floating point numbers. There is only one possible value for *m*, which determines the value of *n*.

### Lexicographical ordering of the floating point format
From [Bruce Dawson](http://www.cygnus-software.com/papers/comparingfloats/Comparing%20floating%20point%20numbers.htm):

>The IEEE float and double formats were designed so that the numbers are “lexicographically ordered”, which – in the words of IEEE architect William Kahan means “if two floating-point numbers in the same format are ordered ( say x < y ), then they are ordered the same way when their bits are reinterpreted as Sign-Magnitude integers.”


Let's try to prove this fact!

*Claim:* Let *f<sub>1</sub>* < *f<sub>2</sub>* where *f<sub>1</sub>* and *f<sub>2</sub>* are both positive floats. When their bits are interpreted as integers *i<sub>1</sub>* and *i<sub>2</sub>* respectively, *i<sub>1</sub>* < *i<sub>2</sub>*.

*Proof:* Recall the floating point representation:

![floating point representation](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d2/Float_example.svg/590px-Float_example.svg.png)

Since *f<sub>1</sub>* and *f<sub>2</sub>* are positive, we know the sign bit will be zero for both.

We have two cases:

1. The exponent of *f<sub>1</sub>* is less than the exponent of *f<sub>2</sub>*
2. The exponent of *f<sub>1</sub>* is equal to the exponent of *f<sub>2</sub>*

Note that we cannot have the exponent of *f<sub>1</sub>* be greater than the exponent of *f<sub>2</sub>* -- that would violate our assumption that *f<sub>1</sub>* < *f<sub>2</sub>*.

Let ![](http://i.imgur.com/vMUzL9U.gif) and ![](http://i.imgur.com/zri7oXk.gif) represent the eight exponent bits of *f<sub>1</sub>* and *f<sub>2</sub>* respectively. In case (1), we know that there exists some *i* between 23 and 30 (inclusive) such that  *b<sub>i</sub>* < *c<sub>i</sub>*, and for all *j* > *i*, *b<sub>j</sub>* = *c<sub>j</sub>*. In other words, if the exponent of *f<sub>2</sub>* is larger, there is a first digit where the exponent bits differ and *f<sub>2</sub>*'s is larger.

It follows that *i<sub>1</sub>* < *i<sub>2</sub>*, because the eight exponent bits precede the 23 fraction bits.

In case (2), since the exponents are equal, we know that the *f<sub>2</sub>*'s fraction must be larger than *f<sub>1</sub>*'s fraction. It follows that *i<sub>1</sub>* < *i<sub>2</sub>*.

### Addendum
I have not covered special cases in the floating point format, in particular the representation of zero and the representation of [subnormal numbers](https://en.wikipedia.org/wiki/Denormal_number) (that link does not give a great explanation of the concept, but I am unaware of a better source). Observant readers may have noticed there is no way to represent zero in the floating point format given the formulas I have provided!

Extending these proofs to cover the zero and subnormal cases is left as an excercise for the reader.

Another interesting fact that I will not go into extreme detail here is that for floats of the same sign:
1. Adjacent floats have adjacent integer representations
2. Incrementing the integer representation of a float moves to the next representable float, moving away from zero

(credit: [Bruce Dawson](https://randomascii.wordpress.com/2012/01/23/stupid-float-tricks-2/) for the wording of this fact)
