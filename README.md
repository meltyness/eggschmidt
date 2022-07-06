# eggschmidt
A non-working prototype of a compression scheme.

Eggschmidt Protocol
-------------------

Alice, and Bob share a large list of prime numbers, indexed by their occurence in The Sequence of Prime Numbers.

For illustration purposes:

i | prime
-----------
0 | 2
1 | 3
2 | 5
3 | 7
4 | 11
.
.
.

Alice, after encrypting data in an ideal cryptographic scheme, would like to further compress this message.
	*which would result in a uniformly-distributed sequence of zeros and ones 

Alice proceeds with the following sequence of actions:

-- Blocking
- Alice breaks the message, M, into a sequence of submessages, {M_i} each consisting of N bits, 
	* N is an integer for which it is always tractable for Alice to quickly "distill"
	* Quickly meaning, faster than the period of the PPS of the channel

-- Distilling
For each submessage, M_i
- Alice "distills" the message by:
	- factor M_i into its prime factors, or
	- identify that it, M, itself is prime
	- Record the result into {P_j, j, n} Where:
		- P_j is the prime factor
		- j is the index, in the sequence of all primes
		- n is the number of repetitions of P_j
	* This process takes at most sqrt(N) by the Fundamental Theorem of Arithmetic

-- Encoding
- For each submessage, M_i Alice encodes as follows:
	- Produce a message D, comprised of
		- j in binary
		- n in binary
	- Within D, identify the shortest "non-occurent" sequence s
	- Modify D to escape after each j and each n with the sequence s
	- Prepend D with an escaped header identifying s

Alice transmits D to Bob
