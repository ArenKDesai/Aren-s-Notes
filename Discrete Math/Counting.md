#CS240 #Counting #Choosing #Permutation #BinomialTheorem #UWMadison

### Product Rule
- Used for sequences
- i.e. if there are n options in m selections, total number of options is nm

### Sum Rule
- Used for when a selection is made
- i.e. When there are n options from m selections, there are n + m selections made

### Generalized Product Rule
- Used when the number of choices made does not depend on the previous choices
- Start with k options. Then, choose 1, and move on to k-1 options. Choose 1, move to k-2. 
- If you are choosing 3 people out of 20, then there are $20*19*18$ choices. 

### Inclusion-Exclusion Rule
- For the union of two finite sets A and B, then $|A \bigcup B| = |A| + |B| - |A \bigcap B|$
- In other words, the count of two options is the addition of all of the options for A and all of the options for B, minus the overlap. 
- i.e. With two dice, the number of possibilities where at least one of the die is a 3 is $6 + 6 - 1 = 11$
- This can be generalized to $n$ sets in such a way that you can add the sizes of the sets, subtract the pairwise overlap, add the 3rd overlap, subtract 4th, etc. 

## Choosing
If you want to choose $n$ assets from a set of $r$, there are $\frac{n!}{r!(n-r)!}$ options to choose from. 
The order does not matter, but the assets you are choosing are unique. 
This can also be shown as $C(n,r)$

## Permutation
If you already have $r$ assets and you want to choose from $n$ options (such as where to place them), there are $\frac{n!}{(n-r)!}$ options to choose from. 
This can be shown as $P(n,r)$

## Strings
You can count how to rearrange the letters in a string (word) of length $n$ and letters $a_1$, $a_2$, ..., $a_n$ with $n!/\prod{count(a_n)}$ (reminder: $\prod$ = multiplication sum)

### Binomial Theorem
For any non-negative integer $n$ and any real numbers $a$ and $b$:
$(a+b)^n=\sum^n_{k=0}\binom{n}{k}a^{n-k}b^k=\sum^n_{k=0}\binom{n}{k}a^kb^{n-k}$

### Pigeonhole Principle
If you're trying to estimate how many events need to occur to reach a guaranteed outcome, it is $k(b-1)+1$, where $k$ = size of set and $b$ = minimum outcome.  