# Decision Theory
### Bayesian decision theory
In decision theory, we assume the **agent** has a set of possible actions $\mathcal{A}$ to choose from. Each of these actions has costs and benefits which will depend on the underlying state of nature $h \in \mathcal{H}$. We can encode this info into a loss function $l(h, a)$ , that specifies the loss we incur if we take action $a \in \mathcal{A}$ when the state of nature is $h \in \mathcal{H}$.
Once we have specified the loss function, we can compute the **posterior expected loss** or **risk** for each possible action $a$ given all the relevant evidence, which may be a single datum $x$ or an entire data set $\mathcal{D}$, depending on the problem:
$$
\rho(a|x) \triangleq \mathbb{E}_{p(h|x)} [\ell (h, a)] - \sum_{h \in \mathcal{H}} \ell (h,a) p(h|x) 
$$
The **optimal policy** $\pi^{*}(x)$ also called the **Bayes estimator** or **Bayes decision rule** $\delta^{*}(x)$ specifies what action to take when presented with evidence $x$ so as to minimize the risk. 
$$
\pi^{*}(x) = \underset{a \in \mathcal{A}}{argmin} \mathbb{E}_{p(h|x)} [\ell(h,a)]
$$
An alternative, but equivalent, way of stating this result is as follows. Let us define a utility function $U(h, a)$ to be the desirability of each possible action in each possible state. If we set $U(h, a) = −ℓ(h, a),$ then the optimal policy is as follows:
$$
\pi^{*}(x) = \underset {a \in \mathcal{A}}{argmax} \mathbb{E}_{h}[U(h,a)]
$$
This is called the **maximum expected utility principle**.
$$

$$
#### Classification problems
###### Zero-one loss
Suppose the states of nature correspond to class labels, so $\mathcal{H}= \mathcal{Y}= \{ 1, \dots, C \}$ . Furthermore suppose the actions also corresponds to class labels, so $\mathcal{A} = \mathcal{Y}$.
### Choosing the "right" model
### Frequentist decision theory
### Empirical risk minimization
### Frequentist hypothesis testing