# 01 · The Pivot Method and What "Confidence" Means

## Terminology
- **Target unknown parameter**: the parameter we want an interval for (call it $\theta$).
- **Nuisance parameters**: any *other* unknown parameters in the model that are not our target.

Example: for $N(\mu,\sigma^2)$, if we want a CI for $\mu$, then $\mu$ is the target and $\sigma^2$ is a nuisance parameter. If we want a CI for $\sigma^2$, the roles swap.

## Definition
A **$(1-\alpha)$ confidence interval** for $\theta$ is a random interval $[L(\mathbf X),\,U(\mathbf X)]$ such that

$$
P_\theta\big(L(\mathbf X)\le \theta\le U(\mathbf X)\big)\;\ge\;1-\alpha\qquad\text{for every }\theta .
$$

- The *endpoints* are random (functions of the sample). $\theta$ is a fixed constant.
- If equality holds for every $\theta$, the interval has *exact* coverage. Otherwise (discrete cases, large-sample approximations) coverage is $\ge 1-\alpha$ or only approximate.

## Pivot
A **pivot** $Q(\mathbf X,\theta)$ is a function of the data and the target parameter that satisfies **both** of these conditions:

1. **Free of nuisance parameters in its expression.** $Q$ may contain $\theta$ but no other unknown. If a nuisance parameter appears in $Q$, we cannot rearrange $a\le Q\le b$ into a statement with $\theta$ isolated in the middle, so no CI comes out of it.
2. **Distribution completely known.** The distribution of $Q$ must not depend on $\theta$ or on any nuisance parameter.

Recipe:
1. Find a pivot $Q(\mathbf X,\theta)$.
2. Choose $a,b$ with $P(a\le Q\le b)=1-\alpha$.
3. Rearrange $a\le Q(\mathbf X,\theta)\le b$ into $L(\mathbf X)\le\theta\le U(\mathbf X)$.
   Watch for sign flips when multiplying or dividing by a negative number, and when inverting a positive quantity.

## Worked example: $N(\mu,\sigma^2)$, $\sigma$ known
Target: $\mu$. Nuisance parameters: none (since $\sigma$ is known).

Pivot:

$$
Z=\frac{\bar X-\mu}{\sigma/\sqrt n}\sim N(0,1)
$$

Then $P(-z_{\alpha/2}\le Z\le z_{\alpha/2})=1-\alpha$, and rearranging gives

$$
\boxed{\;\bar X-z_{\alpha/2}\frac{\sigma}{\sqrt n}\;\le\;\mu\;\le\;\bar X+z_{\alpha/2}\frac{\sigma}{\sqrt n}\;}
$$

Common critical values: $z_{0.05}=1.645$, $z_{0.025}=1.96$, $z_{0.005}\approx 2.576$.

If $\sigma$ were unknown, it would be a nuisance parameter sitting inside $Z$, and condition 1 would fail. Lesson 2 fixes this by replacing $\sigma$ with $S$.

## Interpretation (a favourite JAM trap)
- **Correct:** if we repeat the sampling many times, about $95\%$ of the intervals built this way contain $\mu$. The $95\%$ describes the *procedure*.
- **Wrong:** "after observing $\bar x=10$, $P(9.02\le\mu\le10.98)=0.95$". Once the data are observed, the endpoints are numbers and $\mu$ is a number, so the statement is simply true or false (probability $1$ or $0$). Nothing is random any more.

## Length
Length $=$ upper endpoint $-$ lower endpoint. For the $\sigma$-known normal mean:

$$
L=2\,z_{\alpha/2}\,\frac{\sigma}{\sqrt n}
$$

- Higher confidence gives a larger $z_{\alpha/2}$, so a **wider** interval ($99\%$ is wider than $95\%$).
- $L\propto 1/\sqrt n$. To halve $L$, **multiply $n$ by $4$**.
- To get $L\le \ell$, take $n\ge\left(\dfrac{2\,z_{\alpha/2}\,\sigma}{\ell}\right)^2$.
- This $L$ is a constant only for this pivot. With $\sigma$ unknown (t pivot) or for the variance ($\chi^2$ pivot), the length depends on $S$ and is random, so questions there use the *expected* length.

## Quick checks
- $\bar x=10,\ \sigma=2,\ n=16$: the $95\%$ CI is $10\pm0.98=[9.02,\,10.98]$.
- A one-sided bound uses one tail: $P(Z\le z_\alpha)=1-\alpha$ gives $\mu\ge\bar X-z_\alpha\dfrac{\sigma}{\sqrt n}$ (the upper end is $+\infty$).

## Practice
1. $X_1,\dots,X_{25}\sim N(\mu,9)$, $\bar x=4.2$. Find the $95\%$ CI for $\mu$.
2. How large must $n$ be so that the $95\%$ CI for the mean of $N(\mu,4)$ has length at most $0.5$?
3. True or false: "A $99\%$ CI computed from a sample has a $99\%$ chance of containing $\mu$."

<details>
<summary>Answers</summary>

1. $\sigma/\sqrt n=3/5=0.6$, so $4.2\pm1.96(0.6)=4.2\pm1.176$, giving $\mathbf{[3.024,\;5.376]}$.
2. $2(1.96)(2)/\sqrt n\le0.5\Rightarrow\sqrt n\ge15.68\Rightarrow n\ge245.9$, so $\mathbf{n=246}$.
3. **False** as stated (see the Interpretation section). The $99\%$ refers to the procedure before sampling, not to one computed interval.

</details>
