# Fixed Point Theorems in Economics
**经济学中的不动点定理**

> Continuity gives existence — contraction gives an algorithm.

不动点定理是现代经济理论的基石。Walras 一般均衡的存在性、Nash 均衡的存在性、动态规划中 Bellman 方程的可解性,本质上都是不动点的故事。本文系统梳理 Brouwer、Kakutani 与 Banach 三个层次递进的不动点定理:从"连续函数 → 连续对应 → 压缩映射",从"仅存在性 → 存在性+算法",对应着经济学问题的三个层级。

---

## 1. Brouwer Fixed Point Theorem
### 布劳威尔不动点定理

#### 定理陈述 / Statement

**(EN)** Let $K \subset \mathbb{R}^n$ be a non-empty, compact, convex set and let $f: K \to K$ be continuous. Then there exists $x^* \in K$ with $f(x^*) = x^*$.

**(中文)** 设 $K \subset \mathbb{R}^n$ 为非空紧致凸集,$f: K \to K$ 连续。则存在 $x^* \in K$ 使得 $f(x^*) = x^*$。

#### English Proof — *via the no-retraction theorem*

It suffices to prove the result for the closed unit ball $B^n = \{x \in \mathbb{R}^n : \|x\| \le 1\}$, since any non-empty compact convex set in $\mathbb{R}^n$ is homeomorphic to $B^k$ for some $k \le n$, and the existence of a fixed point is preserved under homeomorphism.

Suppose, for contradiction, that $f: B^n \to B^n$ is continuous and has *no* fixed point: $f(x) \ne x$ for all $x$. Define
$$
r(x) \;=\; x + t(x)\bigl(x - f(x)\bigr),
$$
where $t(x) \ge 0$ is the unique non-negative scalar that places $r(x)$ on the boundary $S^{n-1}$. Geometrically, $r(x)$ is the point at which the ray from $f(x)$ through $x$ meets the sphere. Because $x \ne f(x)$ everywhere, $t(x)$ is well-defined and continuous in $x$; hence $r$ is continuous. Moreover, if $x \in S^{n-1}$ then the ray exits $B^n$ at $x$ itself, so $r(x) = x$.

Therefore $r: B^n \to S^{n-1}$ is a continuous retraction. But the no-retraction theorem (a standard consequence of $\widetilde H_{n-1}(B^n) = 0$ while $\widetilde H_{n-1}(S^{n-1}) \cong \mathbb{Z}$) forbids such a map. Contradiction. Hence $f$ must have a fixed point. $\blacksquare$

#### 中文证明 —— 基于 Sperner 引理的组合方法

不失一般性,把 $K$ 取为标准单纯形 $\Delta^n = \{x \in \mathbb{R}^{n+1}_{\ge 0} : \sum_{i=0}^n x_i = 1\}$。给定连续映射 $f: \Delta^n \to \Delta^n$,对 $\Delta^n$ 作 $k$ 重重心剖分,得到细网格 $\mathcal{T}_k$。

**标号规则。** 对 $\mathcal{T}_k$ 的每个顶点 $v$,赋一个标号 $\ell(v) \in \{0,1,\dots,n\}$:
$$
\ell(v) \in \bigl\{\, i : v_i > 0 \;\text{且}\; f(v)_i \le v_i \,\bigr\}.
$$
此集合非空——若不然,则 $f(v)_i > v_i$ 对所有 $v_i > 0$ 的指标 $i$ 成立,从而 $\sum_i f(v)_i > \sum_i v_i = 1$,与 $f(v) \in \Delta^n$ 矛盾。再要求位于 $\Delta^n$ 第 $j$ 面 $\{x_j = 0\}$ 上的顶点其标号不为 $j$,这是合法约束。

**Sperner 引理。** 在此标号下,存在一个"完整"的小单纯形 $T_k$——其 $n+1$ 个顶点恰好取齐 $\{0,1,\dots,n\}$ 全部标号。

**取极限。** 设 $T_k$ 的顶点为 $v_0^{(k)}, \dots, v_n^{(k)}$,标号 $i$ 在 $v_i^{(k)}$ 处取到。由 $\Delta^n$ 紧致,经子列可设 $v_i^{(k)} \to x^*$($k\to\infty$ 时单纯形直径 $\to 0$,故所有顶点收敛于同一点)。由标号定义:
$$
f\bigl(v_i^{(k)}\bigr)_i \;\le\; \bigl(v_i^{(k)}\bigr)_i \quad \text{对每个 } i.
$$
取 $k \to \infty$,由 $f$ 连续得 $f(x^*)_i \le x^*_i$ 对所有 $i$。再由 $\sum_i f(x^*)_i = \sum_i x^*_i = 1$,各分量必须取等号,故 $f(x^*) = x^*$。$\blacksquare$

#### Economic Application: Existence of Walrasian Equilibrium

**(EN)** Consider an exchange economy with $L$ goods, prices $p \in \Delta = \{p \in \mathbb{R}^L_+ : \sum_\ell p_\ell = 1\}$, and aggregate excess demand $z(p)$ which (under standard assumptions: continuity, homogeneity, Walras' law $p \cdot z(p) = 0$, and a boundary condition) is continuous on the interior of $\Delta$. Define the *price-adjustment map*
$$
T(p) \;=\; \frac{p_\ell + \max\{0, z_\ell(p)\}}{1 + \sum_{\ell'} \max\{0, z_{\ell'}(p)\}}, \qquad \ell = 1, \dots, L.
$$
$T$ maps $\Delta$ continuously into itself. By Brouwer, there exists $p^* = T(p^*)$.

**Claim.** $z(p^*) \le 0$ componentwise — that is, $p^*$ is a Walrasian equilibrium.

*Proof of claim.* If $p^* = T(p^*)$, then for each $\ell$,
$$
p^*_\ell \cdot \Bigl(1 + \sum_{\ell'} \max\{0, z_{\ell'}(p^*)\}\Bigr) = p^*_\ell + \max\{0, z_\ell(p^*)\}.
$$
Multiply both sides by $z_\ell(p^*)$, sum over $\ell$, and apply Walras' law $\sum_\ell p^*_\ell z_\ell(p^*) = 0$. The result simplifies to $\sum_\ell z_\ell(p^*) \cdot \max\{0, z_\ell(p^*)\} = 0$, which forces $\max\{0, z_\ell(p^*)\} = 0$ for every $\ell$. $\square$

***Intuition.*** The map $T$ raises prices in markets with excess demand and lowers them where there is excess supply — Walras' "tâtonnement". The simplex $\Delta$ is compact and convex; the adjustment is continuous; so Brouwer's theorem makes the equilibrium *topologically inevitable*. We cannot in general write the equilibrium price down explicitly, but its existence is guaranteed by the geometry of the simplex.

**(中文)** 设有 $L$ 种商品的交换经济,价格在单纯形 $\Delta$ 上,超额需求 $z(p)$ 在标准假设下连续并满足 Walras 法则 $p \cdot z(p) = 0$。定义价格调整映射
$$
T(p) \;=\; \frac{p_\ell + \max\{0, z_\ell(p)\}}{1 + \sum_{\ell'} \max\{0, z_{\ell'}(p)\}}.
$$
$T: \Delta \to \Delta$ 连续。由 Brouwer 定理存在 $p^* = T(p^*)$,且代数化简后得 $z_\ell(p^*) \le 0$ 对所有 $\ell$ 成立——这正是市场出清条件。

***直觉。*** 该映射"超额需求市场涨价、超额供给市场跌价",几何上是单纯形上的连续自映射。Brouwer 定理告诉我们:在紧致凸集合上,这种"撞墙必反弹"的连续过程一定存在静止点。我们不需要解出 $p^*$,**拓扑结构本身就保证了均衡的存在**。这是 Arrow–Debreu (1954) 一般均衡存在性证明的核心思想。

---

## 2. Kakutani Fixed Point Theorem
### 角谷不动点定理

#### 定理陈述 / Statement

**(EN)** Let $K \subset \mathbb{R}^n$ be non-empty, compact, and convex. Let $\varphi: K \rightrightarrows K$ be a correspondence (set-valued map) satisfying
1. $\varphi(x)$ is non-empty and convex for every $x \in K$;
2. $\varphi$ has a *closed graph*: $\{(x,y) : y \in \varphi(x)\}$ is closed in $K \times K$.

Then there exists $x^* \in K$ with $x^* \in \varphi(x^*)$.

**(中文)** 设 $K \subset \mathbb{R}^n$ 非空紧凸,对应 $\varphi: K \rightrightarrows K$ 满足
1. $\varphi(x)$ 对每个 $x$ 非空且凸;
2. $\varphi$ 的图 $\operatorname{Gr}(\varphi) := \{(x,y) : y \in \varphi(x)\}$ 在 $K \times K$ 中闭。

则存在 $x^* \in K$ 使 $x^* \in \varphi(x^*)$。

#### English Proof — *via Brouwer + simplicial approximation*

For each integer $k \ge 1$, take a simplicial subdivision $\mathcal{T}_k$ of $K$ with mesh $\le 1/k$. At every vertex $v$ of $\mathcal{T}_k$, choose any $f_k(v) \in \varphi(v)$ (non-empty, by hypothesis 1). Extend $f_k$ to all of $K$ by *barycentric linear interpolation* on each simplex: for $x = \sum_i \lambda_i v_i$ (with $\lambda_i \ge 0$, $\sum \lambda_i = 1$),
$$
f_k(x) \;=\; \sum_i \lambda_i f_k(v_i).
$$

Each $f_k(v) \in \varphi(v) \subset K$, and convexity of $K$ ensures $f_k(x) \in K$. Continuity is built into the construction, so $f_k: K \to K$ is continuous. By **Brouwer**, $f_k$ has a fixed point $x_k = f_k(x_k)$.

By compactness of $K$, pass to a subsequence so that $x_k \to x^*$. The point $x_k$ lies in some simplex of $\mathcal{T}_k$ with vertices $v_0^{(k)}, \dots, v_n^{(k)}$, all within $1/k$ of $x_k$. Write
$$
x_k \;=\; \sum_{i=0}^n \lambda_i^{(k)} f_k(v_i^{(k)}),
$$
with $\lambda_i^{(k)} \ge 0$, $\sum_i \lambda_i^{(k)} = 1$, and $f_k(v_i^{(k)}) \in \varphi(v_i^{(k)})$. Pass to a further subsequence so that $\lambda_i^{(k)} \to \lambda_i^*$ and $f_k(v_i^{(k)}) \to y_i^*$.

Since $v_i^{(k)} \to x^*$, $f_k(v_i^{(k)}) \to y_i^*$, and $(v_i^{(k)}, f_k(v_i^{(k)})) \in \operatorname{Gr}(\varphi)$, the **closed graph** assumption (hypothesis 2) gives $y_i^* \in \varphi(x^*)$ for each $i$. Then **convexity** of $\varphi(x^*)$ (hypothesis 1) gives
$$
x^* \;=\; \sum_i \lambda_i^* y_i^* \;\in\; \varphi(x^*). \quad\blacksquare
$$

#### 中文证明

固定 $k$,对 $K$ 作直径 $\le 1/k$ 的单纯形剖分 $\mathcal{T}_k$。对每个顶点 $v$,任取 $f_k(v) \in \varphi(v)$,在每个小单纯形内对 $f_k$ 作重心线性延拓。由 $\varphi$ 值与 $K$ 的凸性,$f_k: K \to K$ 连续。

由 **Brouwer** 定理,$f_k$ 有不动点 $x_k$。$K$ 紧致,设子列 $x_k \to x^*$。$x_k$ 落在某小单纯形,其顶点 $v_0^{(k)}, \dots, v_n^{(k)}$ 距 $x_k$ 不超过 $1/k$,于是
$$
x_k = \sum_{i=0}^n \lambda_i^{(k)} f_k(v_i^{(k)}), \quad f_k(v_i^{(k)}) \in \varphi(v_i^{(k)}).
$$
再取子列使 $\lambda_i^{(k)} \to \lambda_i^*$, $f_k(v_i^{(k)}) \to y_i^*$。由 $v_i^{(k)} \to x^*$ 及 **图闭**,$y_i^* \in \varphi(x^*)$。再由 $\varphi(x^*)$ **凸**:
$$
x^* = \sum_i \lambda_i^* y_i^* \in \varphi(x^*). \quad\blacksquare
$$

#### Economic Application: Nash Equilibrium

**(EN)** Consider a finite normal-form game with players $i = 1, \dots, n$, finite pure-action sets $A_i$, and expected payoffs $u_i: \prod_j \Delta(A_j) \to \mathbb{R}$ where $\Delta(A_j)$ is the simplex of mixed strategies. Let $\Sigma = \prod_i \Delta(A_i)$ be the strategy profile space — compact and convex.

Define each player's **best-response correspondence**
$$
\mathrm{BR}_i(\sigma_{-i}) \;=\; \arg\max_{\sigma_i \in \Delta(A_i)} u_i(\sigma_i, \sigma_{-i}),
$$
and the joint correspondence $\mathrm{BR}(\sigma) = \prod_i \mathrm{BR}_i(\sigma_{-i})$ from $\Sigma$ to $\Sigma$.

**Verification of Kakutani's hypotheses:**
- *Non-empty*: $u_i$ is continuous (linear in $\sigma_i$) on a compact set, so the argmax is non-empty.
- *Convex*: If $\sigma_i, \sigma_i' \in \mathrm{BR}_i(\sigma_{-i})$, both achieve the same maximum, and any convex combination $\lambda \sigma_i + (1-\lambda)\sigma_i'$ — being linear in $\sigma_i$ for fixed $\sigma_{-i}$ — also achieves it. Convex.
- *Closed graph*: This is the "maximum theorem" — continuity of $u_i$ implies the argmax correspondence has closed graph.

Kakutani delivers $\sigma^* \in \mathrm{BR}(\sigma^*)$ — i.e. $\sigma_i^* \in \mathrm{BR}_i(\sigma_{-i}^*)$ for every $i$ — which is precisely the definition of a **Nash equilibrium** (Nash, 1950).

***Intuition.*** When a player is *indifferent* between several pure strategies, every mixture among them is a best response. The best-response "function" is therefore *not a function* — it is set-valued. Brouwer cannot handle this; it requires single-valued maps. Kakutani's contribution is the right generalization: as long as the set-valued map is convex-valued and has a closed graph (no "vertical jumps escaping"), the fixed-point conclusion survives.

This is exactly what the visualization in Module 1 shows: a discontinuous *function* may jump over the diagonal $y = x$, leaving no fixed point. A *correspondence* "fills in" the jump with a convex (vertical) interval, and that interval intersects the diagonal — producing a Nash equilibrium where pure-strategy play would have failed.

**(中文)** 有限博弈的混合策略空间 $\Sigma = \prod_i \Delta(A_i)$ 紧致凸。每个玩家的最佳反应
$$
\mathrm{BR}_i(\sigma_{-i}) \;=\; \arg\max_{\sigma_i} u_i(\sigma_i, \sigma_{-i})
$$
为非空(连续函数在紧集上有最大值)、凸(线性优化的解集是凸的)、且由极值定理具有闭图。整体最佳反应 $\mathrm{BR}: \Sigma \rightrightarrows \Sigma$ 满足 Kakutani 的全部条件,故存在 $\sigma^* \in \mathrm{BR}(\sigma^*)$,即 Nash 均衡。

***直觉。*** 当玩家对若干纯策略**无差异**时,任意混合都最优,最佳反应不再是函数而是一段"区间"——这正是模块一可视化中那段竖直填充的经济含义。Brouwer 定理处理不了这种集合值跳跃,而 Kakutani 恰好补上这一步。Nash 论文里那句"this is an immediate corollary of Kakutani"就是这个意思:真正的数学难度在 Kakutani,Nash 均衡的存在性几乎是它的一行推论。

---

## 3. Banach Fixed Point Theorem
### 巴拿赫不动点定理(压缩映射定理)

#### 定理陈述 / Statement

**(EN)** Let $(X, d)$ be a non-empty complete metric space and $T: X \to X$ a *contraction*: there exists $L \in [0, 1)$ with
$$
d(T(x), T(y)) \;\le\; L \cdot d(x, y) \qquad \forall\, x, y \in X.
$$
Then:
1. $T$ has a unique fixed point $x^* \in X$.
2. For every $x_0 \in X$, the iterates $x_{n+1} = T(x_n)$ satisfy $x_n \to x^*$.
3. The convergence is geometric, with the *a priori* bound
$$
d(x_n, x^*) \;\le\; \frac{L^n}{1 - L} \, d(x_1, x_0).
$$

**(中文)** 设 $(X, d)$ 是非空完备度量空间,$T: X \to X$ 是压缩映射(存在 $L \in [0,1)$ 使 $d(T(x), T(y)) \le L \cdot d(x,y)$ 对所有 $x,y$ 成立)。则
1. $T$ 有唯一不动点 $x^*$;
2. 对任意 $x_0$,迭代序列 $x_{n+1} = T(x_n)$ 收敛于 $x^*$;
3. $d(x_n, x^*) \le \dfrac{L^n}{1-L} d(x_1, x_0)$。

#### English Proof

**Existence and convergence.** Fix $x_0 \in X$ and define $x_n = T^n(x_0)$. By induction on the contraction inequality,
$$
d(x_{n+1}, x_n) \;\le\; L \, d(x_n, x_{n-1}) \;\le\; \cdots \;\le\; L^n d(x_1, x_0).
$$
For any $m > n$, the triangle inequality and the geometric series give
$$
d(x_m, x_n) \;\le\; \sum_{k=n}^{m-1} d(x_{k+1}, x_k) \;\le\; d(x_1, x_0) \sum_{k=n}^{m-1} L^k \;\le\; \frac{L^n}{1-L}\, d(x_1, x_0).
$$
The right-hand side $\to 0$ as $n \to \infty$, so $\{x_n\}$ is **Cauchy**. By completeness of $X$, $x_n \to x^* \in X$. Since $T$ is Lipschitz it is continuous, so
$$
T(x^*) \;=\; T\bigl(\lim x_n\bigr) \;=\; \lim T(x_n) \;=\; \lim x_{n+1} \;=\; x^*.
$$

**Uniqueness.** If $T(y^*) = y^*$ as well, then
$$
d(x^*, y^*) \;=\; d(T(x^*), T(y^*)) \;\le\; L \cdot d(x^*, y^*),
$$
and $L < 1$ forces $d(x^*, y^*) = 0$, i.e. $x^* = y^*$.

**Error bound.** Letting $m \to \infty$ in the Cauchy estimate above (with $n$ fixed) gives
$$
d(x_n, x^*) \;\le\; \frac{L^n}{1-L}\, d(x_1, x_0). \quad\blacksquare
$$

#### 中文证明

**存在性与收敛。** 取 $x_0 \in X$,定义 $x_n = T^n(x_0)$。由压缩条件迭代:
$$
d(x_{n+1}, x_n) \le L \cdot d(x_n, x_{n-1}) \le \dots \le L^n \, d(x_1, x_0).
$$
对 $m > n$,
$$
d(x_m, x_n) \le \sum_{k=n}^{m-1} d(x_{k+1}, x_k) \le d(x_1, x_0) \sum_{k=n}^{m-1} L^k \le \frac{L^n}{1-L}\, d(x_1, x_0) \xrightarrow{n\to\infty} 0.
$$
故 $\{x_n\}$ 为 Cauchy 列,由 $X$ 完备得 $x_n \to x^* \in X$。$T$ Lipschitz 故连续,
$$
T(x^*) = T(\lim x_n) = \lim T(x_n) = \lim x_{n+1} = x^*.
$$

**唯一性。** 若另有不动点 $y^*$,则 $d(x^*,y^*) = d(T(x^*), T(y^*)) \le L\cdot d(x^*, y^*)$,$L<1$ 蕴含 $d(x^*, y^*)=0$。

**误差估计。** 上式中令 $m \to \infty$ 即得。$\blacksquare$

#### Economic Application: The Bellman Equation in Dynamic Programming

**(EN)** Consider an infinite-horizon discounted decision problem:
- state $s \in S$ (compact),
- action $a \in A(s)$ (compact-valued),
- instantaneous reward $u(s, a) \in \mathbb{R}$ (continuous, bounded),
- transition probability $Q(\,\cdot\,|\,s, a)$ on $S$,
- discount factor $\beta \in [0, 1)$.

The *value function* $V: S \to \mathbb{R}$ satisfies the **Bellman equation**
$$
V(s) \;=\; \max_{a \in A(s)} \Bigl\{\, u(s, a) \;+\; \beta \int_S V(s') \, Q(ds' \mid s, a) \,\Bigr\} \;=:\; (T V)(s).
$$

Take $X = C_b(S)$, the space of bounded continuous functions on $S$ with the supremum norm $\|V\|_\infty = \sup_s |V(s)|$. This is a complete metric space.

**Claim.** The Bellman operator $T: X \to X$ is a contraction with modulus $\beta$.

*Proof.* For $V_1, V_2 \in X$ and any $s$,
$$
\begin{aligned}
(TV_1)(s) - (TV_2)(s)
&\le \max_{a} \beta \!\int\! V_1(s') Q(ds' | s, a) - \max_{a} \beta \!\int\! V_2(s') Q(ds' | s, a) \\
&\le \max_{a} \beta \!\int\! \bigl[V_1(s') - V_2(s')\bigr] Q(ds' | s, a) \\
&\le \beta \, \|V_1 - V_2\|_\infty.
\end{aligned}
$$
By symmetry, $\|TV_1 - TV_2\|_\infty \le \beta \|V_1 - V_2\|_\infty$. $\square$

By **Banach's theorem**, $T$ has a *unique* fixed point $V^* \in C_b(S)$ — the *value function* — and for any initial guess $V_0$ (even $V_0 \equiv 0$), the **value iteration** $V_{n+1} = T V_n$ converges to $V^*$ at geometric rate:
$$
\|V_n - V^*\|_\infty \;\le\; \frac{\beta^n}{1 - \beta} \, \|V_1 - V_0\|_\infty.
$$

***Intuition.*** The discount factor $\beta < 1$ *literally is* the contraction modulus. Each application of $T$ "shrinks" the disagreement between any two candidate value functions by a factor of $\beta$, because tomorrow's payoff difference is worth only $\beta$ times today's. Banach's theorem then promises three things at once:

1. *(Existence)* the value function exists — the optimization problem is well-posed;
2. *(Uniqueness)* it is the *only* solution to the Bellman equation — no spurious value functions;
3. *(Algorithm)* we can compute it numerically by simply iterating from any starting guess, and we know in advance that the error decays as $\beta^n$.

This is the theoretical foundation of essentially every dynamic-programming algorithm in economics — from optimal growth models to consumption-savings problems — and equally the foundation of value iteration in reinforcement learning.

**(中文)** 考虑无限期贴现决策问题:状态 $s$、行动 $a$、单期效用 $u(s,a)$、转移核 $Q(\cdot|s,a)$、贴现率 $\beta \in [0,1)$。值函数 $V$ 满足 **Bellman 方程**
$$
V(s) = \max_{a \in A(s)} \Bigl\{\,u(s,a) + \beta \int V(s') Q(ds' | s, a)\,\Bigr\} =: (TV)(s).
$$

取 $X = C_b(S)$ 配 sup 范数(完备)。直接验证可得 **Bellman 算子** $T$ 是压缩常数为 $\beta$ 的压缩映射:
$$
\|T V_1 - T V_2\|_\infty \le \beta \, \|V_1 - V_2\|_\infty.
$$
由 Banach 定理:
1. **存在唯一**的值函数 $V^*$;
2. 任取初值 $V_0$,**值迭代** $V_{n+1} = T V_n$ 收敛至 $V^*$;
3. 误差 $\|V_n - V^*\|_\infty \le \dfrac{\beta^n}{1-\beta} \|V_1 - V_0\|_\infty$,几何速率收敛。

***直觉。*** 贴现率 $\beta$ 直接就是压缩常数——未来每被推迟一期就被打 $\beta$ 折,所以两个候选值函数的差距每经一次 Bellman 算子就缩小 $\beta$ 倍。Banach 定理同时给了三件事:

1. *存在性*——值函数确实存在,优化问题良定;
2. *唯一性*——Bellman 方程的解是唯一的,不会有"假值函数";
3. *算法*——值迭代是一个可行的数值算法,误差以 $\beta^n$ 速率指数衰减,无需任何先验知识。

这是从最优增长模型、消费-储蓄问题,到强化学习中值迭代算法的全部数学基础。**贴现率本身就是收敛速率**——这条简洁等式是动态宏观经济学最深刻的结论之一。

---

## Summary | 三定理对比

| Theorem    | 映射类型 Map type            | 域 Domain        | 结论 Output                         | 经济学典型用途 Typical use         |
|------------|------------------------------|------------------|--------------------------------------|------------------------------------|
| Brouwer    | continuous function          | compact convex   | existence                            | 一般均衡 Walrasian equilibrium     |
| Kakutani   | closed-graph correspondence  | compact convex   | existence                            | Nash 均衡 Nash equilibrium         |
| Banach     | contraction                  | complete metric  | existence + uniqueness + algorithm   | Bellman 方程、动态规划、强化学习   |

定理强度自上而下递增。Brouwer 处理连续函数,只给"存在";Kakutani 把它推广到集合值映射,代价是要求闭图与凸值;Banach 在完备度量空间上以"压缩"换取了**唯一性**与**可计算**性。三者恰好对应经济学的三个层次问题:

1. **均衡是否存在?** — Brouwer
2. **博弈中的均衡是否存在?**(包含无差异、混合策略) — Kakutani
3. **最优策略如何计算?**(可证明收敛的算法) — Banach

> *Continuity gives existence — contraction gives an algorithm.*
> 连续性赋予存在,压缩性赋予算法。
