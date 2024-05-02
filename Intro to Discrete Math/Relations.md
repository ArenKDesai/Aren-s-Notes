#CS240 #Relations #Functions #UWMadison

$a \equiv_b c$ means $a$ is equal to $c \mod b$.

## The Empty Set
$\emptyset$ is antisymmetric and symmetric, not reflexive, and transitive

### Reflexivity
If $R$ is a relation on set $A$, $R$ is reflexive only if for every $x \in A$, $xRx$

### Anti-Reflexivity
$R$ is anti-reflexive if for every $x \in R$, it is **not** true that $xRx$

### Symmetry
$R$ is symmetric iff for $x, y \in A$, $xRy$ and $yRx$. 

### Anti-Symmetry
If $x \neq y$, then it cannot be the case that $xRy$ and $yRx$. 

### Transitivity
If $xRy$ and $yRz$, then it must be the case that $xRz$. 

### One-To-One
A function is one-to-one if for every $f(x_a)=y_a$ and $f(x_b)=y_b$ where $x_a \neq x_b$, then $y_a \neq y_b$

### Onto / Surjective
A function is onto if there is an $x_n$ for every $y_n$ in $f(x_n) = y_n$. 

### Bijection
One-to-one and onto. 

### Total
A function where for every $x_n$ in $f(x_n) = y_n$ there is a $y_n$.

## Equivalence Relations
A relation $R$ is an equivalence relation if $R$ is reflexive, transitive, and symmetric. This is denoted as $a$ ~ $b$ to reference $aRb$. 

## Order Relations
A relation $R$ is an order relation if $R$ is antisymmetric and transitive. 

### Partial Order
Reflexive, anti-symmetric, and transitive. 

### Total Order
There is a relation between all members of a set. 

### Strict Order
Antireflexive. 