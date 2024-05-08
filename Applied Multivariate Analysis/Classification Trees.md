#Stat456 #Statistics #CART 

## Elements of a tree:
- Root node
- Splits
- Terminal node
- Parent node
- Child node

## Issues:
- Splitting rules
- Measuring split quality
- Pruning rules

## Determining a split
- Typically only binary splits
- When adding node $m$, $R_m$ is the part of feature space corresponding to node $m$, then the proportion of observations from class $k$ in region $R_m$ is $p_k(m)=n_m^{-1}\sum_{x_i \in R_m}I(y_i=c_k)$
- Observations in node $m$ are classified to the majority class $k(m)=arg\ max_kp_k(m)$

## Impurity measures
- Homogeneous class distribution is preferred
- Misclassification error $Q(m)=n_m^{-1}\sum_{i \in R_m}1{y_i \neq k(m)}=1-max_kp_k(m)$
- Gini index $Q(m)=\sum_{k=1}^Kp_k(m){1-p_k(m)}$
- Lower $Q(m)$ = more pure node

## Splitting by impurity
Considering a parent node $P$ with $n_P$ observations, we can split it into two children nodes $L$ and $R$ with $n_L$ and $n_R$ observations. We want to maximize $M(Split)=Q(P)-(\frac{n_l}{n_P}Q(L)+\frac{n_R}{n_P}Q(R))$. This measures the average increase in quality from parent -> children. 

## Cost-complexity pruning
We have a complexity parameter $\alpha$, and we want to find a subtree $T$ that minimizes the cost function $C(T)=\sum_mn_mQ(m)+\alpha |T|$. $|T|$ is the penalty for size, $\alpha=0$ corresponds to minimizing training error (largest tree). 

Trees are inexpensive and can have mixed variable types, but there is a lack of global optimality (greedy). 