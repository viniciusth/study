If $E$ is an event, then $\bar{E}$ is the complement of the event -> $E$ doesn't occur.

$Pr[E] = 1 - Pr[\bar{E}]$.
##### Relations
1. $Pr[E_1 \land E_2] \leq Pr[E_1]$
2. $Pr[E_1 \land E_2] \leq Pr[E_2]$
3. $Pr[E_2 \land E_1] = Pr[E_1 \land E_2]$
4. Events $E_1$ and $E_2$ are said to be independent if $Pr[E_1 \land E_2] = Pr[E_1] \cdot Pr[E_2]$

5. $Pr[E_1 \lor E_2] \geq Pr[E_1]$ and same properties as 2, 3.
##### Union Bound
$Pr[E_1 \lor E_2] \leq Pr[E_1] + Pr[E_2]$ 
##### Conditional Probability
Probability of $E_1$ occurring given $E_2$ occurred. 
$Pr[E_1 | E_2] = \frac{Pr[E_1 \land E_2]}{Pr[E_2]}$
-> if $E_1$ and $E_2$ are independent, then $Pr[E_1 | E_2] = Pr[E_1]$
see: [[Bayes Theorem]]

#flashcards/probability
What does $Pr[X | Y]$ mean?::Probability of X happening given that Y happened.
How do you derive a formula for $Pr[X|Y]$? Hint: use $Pr[X \land Y]$.::$\frac{Pr[X\land Y]}{Pr[Y]}$.