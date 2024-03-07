# binary cross-entropy loss

It is a type of [[cost function]] for [[classification]]

(1) general formulation:

$$
L(X,y)=\bigg\{\begin{matrix} -log\ P(Y=1|X)\quad \text{if }y=1 \\ 
 -log\ P(Y=0|X)\quad \text{if }y=0\end{matrix}
$$

(2) modified to account for class imbalance, we get the weighted loss:

$$
L(X,y)=\bigg\{\begin{matrix} w_p \cdot -log\ P(Y=1|X)\quad \text{if }y=1 \\ 
w_n \cdot -log\ P(Y=0|X)\quad \text{if }y=0\end{matrix}
$$

Here, we add the weight term $w$, which is proportional to the size of the opposite class (in the binary case). For example, if we have a positive class $p$ and a negative class $n$:

$$
w_p=\frac{\text{num negative}}{\text{num total}}\quad \quad w_n = \frac{\text{num positive}}{\text{num total}}
$$


- Links
- [https://gombru.github.io/2018/05/23/cross_entropy_loss/](https://gombru.github.io/2018/05/23/cross_entropy_loss/)
