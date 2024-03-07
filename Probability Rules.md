[[probability]]

#### Rule 1: Range of possible probabilities
The probability of an impossible event is zero; the probability of a certain event is one. Therefore, for any event $A$, the range of possible probabilities is: $0 ≤ P(A) ≤ 1$

#### Rule 2: Disjoint and exhaustive
For $S$ the sample space of all possibilities, $P(S) = 1$. That is, the sum of all the probabilities for all possible events is equal to one. Recall the party affiliation above: if you have to belong to one of the three designated political parties $R$, $D$, or $I$, then $P(R)+P(D)+P(I)=1$.

#### Rule 3: Negation rule
For any event $A$, $P(!A) = 1 - P(A)$
It follows then that $P(A) = 1 - P(!A)$

#### Rule 4: Addition Rule
This is the probability that exactly **one** of two events occur, i.e., $P(A \lor B)$
##### Mutually exclusive events
* If two events, say $A$ and $B$, are **mutually exclusive** - that is $A$ and $B$ have no outcomes in common - then $P(A \lor B) = P(A) + P(B)$
##### Not mutually exclusive
If there are two ways that A can occur, by itself and with B, its probability is $P(A)$. So the probability of $A$ just by itself is $P(A)-P(A,B)$. The same goes for B by itself. If you add these together, you get $P(A  \lor  B) = P(A) + P(B) - 2P(A, B) = P(A) + P(B) — 2P(A)P(B)$

#### Rule 5: Multiplication Rule
This rule governs the probability that **both** events occur, i.e., $P(A, B)$
##### Dependent events
* If $A$ and $B$ are not independent, the probability that **both** events occur is equal to the probability that one of them occurs multiplied by the conditional probability that the other one occurs given the first one. In other words: $P(A, B) = P(A)P(B|A) = P(B)P(A|B)$ 
##### Independent events
* If $A$ and $B$ are independent - neither event influences or affects the probability that the other event occurs - then $P(A, B) = P(A)P(B)$
* This particular rule extends to more than two independent events. For example, $P(A, B, C) = P(A)P(B)P(C)$

#### Rule 6: Conditional Probability
This is [[Bayes Theorem]].

$P(A|B)=\frac{P(A,B)}{P(B)}=\frac{P(B|A)P(A)}{P(B)}$ 



# Resources

* [University of Florida Open Textbook, chapter on probability](https://bolt.mph.ufl.edu/6050-6052/unit-3/)