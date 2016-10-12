# Floating point numbers
This is an introduction to some of the basic concepts of floating point numbers. We will build up to prove some interesting facts about their representation.

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

We can now see that floating point numbers are essentially represented in binary scientific notation. In paricular, floating point numbers are expressed in [normalized scientific notation](https://en.wikipedia.org/wiki/Scientific_notation#Normalized_notation).

In binary scientific notation, all numbers are written in the form
![](http://i.imgur.com/NWcpCim.gif). In normalized binary scientific notation,  the exponent *n* is chosen so that the absolute value of *m* remains at least one but less than two (1 ≤ |*m*| < 2).

With this knowledge, we can prove some interesting facts.

### Floating point representation uniqueness

*Claim:* Every number has a unique representation in the floating point binary format

*Proof:* This follows from the normalized scientific notation representation of floating point numbers.

### Sign magnitude shit


