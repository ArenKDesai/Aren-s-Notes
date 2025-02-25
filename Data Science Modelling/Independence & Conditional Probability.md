#Stat340 #Independence #ConditionalProbability #PearsonCorrelation #Covariance #Statistics #UWMadison 

$\Omega$ is the set of possible outcomes, with a subset $E \subseteq \Omega$ called an event and probabilities Pr\[*E*] that map events to numbers. Pr\[$\Omega=1$]

### Independence
If $E_1$ and $E_2$ are independent, then Pr\[$E_1 \bigcap E_2$] (or Pr\[$E_1, E_2$]) = Pr\[$E_1$]Pr\[$E_2$]. 
Two random variables X and Y are independent if for all sets $S_1, S_2$, we have Pr\[$X \in S_1, Y \in S_2$] = Pr\[$X \in S_1$]Pr\[$Y \in S_2$]
Example:
A die is rolled and a coin is flipped. For arbitrary outcomes $d \in D$ and $c \in C$, Pr\[$D=d, C=c$] = $\frac{1}{6}*\frac{1}{2}=\frac{1}{12}$.
Independence in variables is not always obvious, but (at least for now) doesn't require a formal proof. 
If X and Y are discrete, the equation above holds. If continuous, then $f_{X,Y}(s,t)=f_X(s)f_Y(t)$. 
[[Expectation]] for expectation of a random variable

### Covariance
Cov(X,Y) = $\mathbb{E}(X-\mathbb{E}X)(Y-\mathbb{E}Y)$.
If Cov(X,Y) = 0, then the normal Var(X+Y) equation applies. This is true when X and Y are independent.

### Pearson Correlation
$p_{X,Y}=\frac{Cov(X,Y)}{\sqrt{(VarX)(VarY)}}$
- Always between -1 and 1. 
- If X and Y are independent, they are uncorrelated. However, if two random variables are uncorrelated, that does not guarantee they are independent. 
- Cov(X,X) = 0
Ex:
```r
mu = c(.5,.5)
CovMx = matrix(c(0.05^2, 0.04^2, 0.04^2, 0.05^2), nrow = 2) # Defines a 2,2 symmetry matrix
library(MASS) # For multivariate normal
WpMp = mvrnorm(n=2000, mu=mu, Sigma=CovMx)
plot(WpMp, xlab = "Wisconsin proportion", ylab = "Michigan proportion")
```
![[Pasted image 20231218212117.png]]

### Conditional Probability
Determining the probability of an event given a related event occurred. 
Pr\[$A|B$]=$\frac{Pr[A \bigcap B]}{Pr[B]}$ (if $B=0$, this is undefined)
For example, consider the probability that a 6-sided die has landed on $3$ given that the die landed on an even number. We can label A = die lands on 2 and B = even. Then, Pr\[$A|B$]=$\frac{^1/_6}{^1/_2}=\frac{1}{3}$. Pr\[$A \bigcap B$]=Pr\[die lands 2] because 2 is an even number. 

## Bayes' Rule
$Pr[A|B]=\frac{Pr[B|A]Pr[A]}{Pr[B]}$
Ex: testing for a rare disease, where A = disease and B = positive test. Given Pr\[A] = Pr\[disease] = $^1/_{10^6}$ and Pr\[B] = Pr\[positive test] = $1.999*10^{-6}$, and finally, Pr\[B|A] = 0.9999. So, $\frac{0.9999*\frac{1}{10^{-6}}}{1.999*10^{-6}}= 0.5002001$, the probability that a patient has the rare disease given a positive test. 