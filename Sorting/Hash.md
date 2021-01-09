# Hash

- hash[key] = value problems
1. map non-integer: pre-hashing
2. memory hog: hash with chaining

- Pre-hashing
1. def: turn a non-integer key into integer
2. Method
	get the byte used to save strings etc.
	get the memory address if it doesn't change

# Hashing
1. map n integer keys items into m slot
attemp.1: division method
	key % m
	=> too much collision
	=> set m to a prime number
attemp.2: multiplication
	(a * key mod 2^w)>>(w-r)
	w is word length
	get a random natually by the bit digit of a
attemp.3: universal hashing
	h(k) = (ak + b) mod p
	a and b are pure random (0, p-1)

2. expand from n items into n+1
Strategy: given the old slot m, we create a new hash table with m' slot and mapping all the n +1 items there.
Time complexity: Θ(n+m+m')
	- iterate n items, find them in m hash and initialize m' hash table
How big is m'
	- m' = m+1
		disadv. if more items are added, each new items needs more manipuations.
	- m' = 2m 
		table doubling
		to grow from 1 to n items, we double lg(n) times
		time complexity of expansion: 
			Θ(1+2+4+8+...+n)
			 = Θ( 1 + 2^1 + 2^2 + ... + 2^lg(n))
			 = Θ(2n - 1) = Θ(n)
	- Amortization
		T(n): sum( manipulate n times is Θ(n))
		Θ(1) amortized
