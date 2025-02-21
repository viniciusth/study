https://codeforces.com/contest/2069
### E
in a string S, each character will have at most 3 options on how to be separated.
aba & bab are the only cases where a character will have 3 options

a & b separation should be done in the end only, as they are more "free"
question really is about: what is the maximum amount of ba & ab you can fit in this string? maximize this amount. then $a + b \geq n - c * 2$ is the condition for YES.

now aba & bab only actually have two options, and these are the cases where we meaningful decisions to take. 

abababab -> $[ab][ab][ab][ab]$ or $a[ba][ba][ba]b$ or $a[ba]b[ab][ab]$ or ...
	this means that not picking the first one that shows up will at worst you need one more a & b? and at best you maintain the amount (ababa needs one a).
maybe analyze sequences of contiguous "ab" ababab, or "ba" bababa
-> choices here for a sequence s is either use $\frac{|s|}{2}$ of their type, or reduce a & b by 1 and choose any pair (x, y) to use where $x + y = \frac{|s|}{2} - 1$
-> ambiguity on how to classify smth like ababa or babab
-> ababa can be split into any pair without having to sacrifice anything, but by default they consume an a no matter what you do. babab same but with b
-> would greedy be optimal? if x is the group with the max ab count cost and you can do the operation, when would it be bad to do so? doesn't feel like there could be a bad one.
	if so, this gives us a two phase algorithm:
		1. sort ab & ba groups by cost decreasing, grab as much as you can
			1. I guess here what we're trying to prove is the problem where you have an array $A = {a_1, \ldots, a_n}$ and you want to pick a subset $S \in A, \sum_{a_i \in S} a_i \leq x$ and the sum is maximal. -> this is not doable in greedy
			2. a thing to observe is that the sum is $\leq n$, and we can solve the subset sum problem in $O(n \sqrt{n})$, do that to get the max amount of elements ab we can do. we want to use the max amount of groups so handle that to get the max.
		2. after using the max amount of groups isolated, we have the smallest amount of ab & ba groups available, we should just always pick the biggest ones because now we can choose any pair we want, thus sacrificing 1 a & 1 b for the biggest one will be optimal.
		3. check if the condition holds.
I'm trolling lol, one oversight here: you don't need to always get a full chain, you can get parts of it. 
-> lets reduce the problem:
-> for strings of type abababa (alternating, end & start with same character) -> you can choose any number of ab and ba to use s.t. $ab + ba \leq |s|/2$, save this amount in a spare var
-> now you should only have sequences of same letter aaaaa, bbbbb and alternating chains which end on different character. if the chain has size 1, try using ab or ba to finish them
-> some a's and b's will have to be used no matter what -> those that aren't part of any chain
-> now you only have chains of ab and ba. if you have spare a's and b's then now its time to use them, grab the biggest chains and use $min(a, b)$ on them, those are your free pairs, the others you are forced to use their values, so check if you have enough pairs to do it, if you do then delete them and then check if you have enough pairs left to fill the free chains.

failed, lets see a hint from editorial:

---
> same analysis as I did for alternating odd & alternating even
> ok so what im missing is basically the idea that if you have an even alternating ababab, then just use ab on it until you cant anymore as it is optimal, and you should go from smallest to largest, as the blocks of size 1 cant have ba used on them.
> use ab as much as you can on abab, ba on baba, then try filling
---
### F
