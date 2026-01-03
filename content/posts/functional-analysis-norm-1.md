---
date: '2025-08-09T10:05:47+08:00'
draft: false
title: 'Functional Analysis (Part I): Norms'
tags: ['Functional Analysis']
---

## Norms on Quotient Spaces

### Example: Integrable Space

Take the definition of the \(L^1\) space as an example. \(\mathcal L^1(X, \mu)\) is the set of functions \(f\) satisfying \(\int_{X} |f| d\mu < \infty\). The fact that it is a linear space is due to the linearity of the integral. The integral \(\int_{X} |\cdot| ~d\mu\) on \(\mathcal L^1(X, \mu)\) is a seminorm, because \(\int_{X} |f| ~d\mu = 0\) implies only that \(f\) is zero almost everywhere with respect to the measure \(\mu\), not that \(f\) is identically zero. Therefore, for reasons such as turning the seminorm into a norm, we must take the quotient space. Formally, we define \(\mathcal N\) as the set of functions that are zero almost everywhere with respect to the measure \(\mu\). This is undoubtedly a linear subspace. Thus, we take the quotient space \(\mathcal L^1(X, \mu) / \mathcal N\). (Normally, one needs to generally state that the linear subspace is a closed subspace. Under the norm \(\int_{X} |\cdot| ~d\mu\), if \( {f_n} \subset \mathcal N\) and \( f_n \to f\) in \(\mathcal L^1(X, \mu)\), then according to Fatou's Lemma, we get \(f \in \mathcal N\). This ensures that \(\mathcal N\) is closed. This step is usually a general requirement for equipping a quotient space with a norm, but it is unnecessary in my proof). The elements of the quotient space \(\mathcal L^1(X, \mu) / \mathcal N\) are \([f] = f + \mathcal N\). We define the norm on it as \( \left\|[\cdot]\right\| = \inf_{g \in \mathcal N} \int_{X} |\cdot + g| ~d\mu\). According to the triangle inequality:
\[\begin{aligned}
0 & \le \int_{X} |f| ~d\mu  \\
& = \left| \int_{X} |f| d\mu - \int_{X} |g| d\mu \right| \\
& \le \int_{X} |f + g| ~d\mu
\end{aligned}\]
Actually, it can also be handled from the other end:
\[\begin{aligned}
\int_{X} |f+g| ~d\mu & \le \int_{X} |f| ~d\mu + \int_{X} |g| ~d\mu\\
& = \int_{X} |f| ~d\mu
\end{aligned}\]
Taking the infimum, we see that this norm is equivalent to the seminorm of the original space. \(\left\|[f]\right\| = 0\) implies \([f] = [0]\) in the space \(\mathcal L^1(X, \mu) / \mathcal N\), which means \(f \in \mathcal N\). Other linear properties and the triangle inequality are easy to verify. Thus, a norm is defined on \(\mathcal L^1(X, \mu) / \mathcal N\) (directly using the seminorm of the original space). This space is called \(L^1(X, \mu)\).

It's not over yet. The initial condition that \(\mathcal N\) is a closed subspace seems necessary, but it is actually not needed at all. On second thought, this whole process simply transforms the seminorm of the original space into the norm of the quotient space. This entire process does not require utilizing the general properties of norms on quotient spaces. The zero kernel of a seminorm is just a linear subspace. Modding out this linear subspace from the original space is sufficient.

## Norms

Defining a norm induces a metric topology. Norms in finite-dimensional vector spaces are all equivalent (they induce the same metric in the topological sense), but they differ in concrete calculations.

## Separability

A space is separable if it possesses a dense subset and that dense subset is countable. Finding a basis for an infinite-dimensional space is the most classic example—because the summation of uncountably many terms cannot be defined! Thus, the basis must be enumerable, which requires the space to be separable. From this perspective, when we say we can find a basis for an infinite-dimensional space, we mean we can use an enumerable basis to approximate elements in the infinite-dimensional space. For a Hilbert space \(H\), the following three propositions are equivalent:

1. \(H\) is separable.
2. \(H\) has a countable orthonormal basis.
3. All orthonormal systems in \(H\) are at most countable.

## Functional

A functional is a function of functions.

## Extreme Value Theorem

This theorem is quite aesthetic; on a finite-dimensional normed linear space, studying the compactness of a subset is equivalent to studying elements in the dual space—functionals on a finite-dimensional normed linear space attain their maximum values on the subset. There are many such problems in functional analysis, transforming a topological problem into an algebraic problem.

## Annihilator

When I first encountered this, I didn't think much of it; just defining annihilators and pre-annihilators on a space \(X\) and its dual \(X^*\). Just shuffling back and forth on \(X\) and its dual space \(X^*\). Then, I thought about push-forward and pull-back in differential geometry. Next, I suddenly got goosebumps. Doesn't the relationship of this stuff resemble the relationship between ideals and varieties in algebraic geometry? So, similar to Hilbert's Nullstellensatz, there is indeed a relationship between the annihilator and pre-annihilator: taking the annihilator of a subset \(M\) in \(X\) and then taking the pre-annihilator results in the linear closure of \(M\)! It is truly spine-chilling and thoroughly satisfying. Later I learned that this is called a Galois Connection.
