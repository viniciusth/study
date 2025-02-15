see [[books/Introduction to Modern Cryptography/Basic Probability#Conditional Probability|Conditional Probability]].
If $Pr[E_2] > 0$ then:
$$Pr[E_1 | E_2] = \frac{Pr[E_2 | E_1] \cdot Pr[E_1]}{Pr[E_2]}$$
##### Proof
$$Pr[E_1 | E_2] = \frac{Pr[E_1 \land E_2]}{Pr[E_2]} = \frac{Pr[E_2 \land E_1]}{ Pr[E_2]} = \frac{Pr[E_2|E_1] \cdot Pr[E_1]}{Pr[E_2]}$$
1. Use conditional probability definition
2. Swap order (for clarity)
3. Probability of $E_2$ and $E_1$ happening is the same as probability of $E_2$ happening given that $E_1$ happened times the probability of $E_1$ happening -> \
	1. other way to phrase it: force $E_1$ to happen with $Pr[E_1]$, and then for $E_2$ to happen we have probability $Pr[E_2|E_1]$.
	2. Mathematical notation: $Pr[E_1 \land E_2] = Pr[E_1|E_2] \cdot Pr[E_2]$ and $Pr[E_1 \land E_2] = Pr[E_2|E_1] \cdot Pr[E_1]$
	