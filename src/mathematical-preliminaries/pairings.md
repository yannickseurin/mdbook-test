# Pairings

Pairings have allowed a great number of new applications in cryptography.
They were first used by Menezes, Okamoto, and Vanstone to [break the discrete logarithm problem in supersingular elliptic curves](https://dl.acm.org/doi/pdf/10.1145/103418.103434) (this is the so-called MOV attack).
Later, they were used constructively by Joux to obtain a [tripartite Diffie-Hellman protocol](https://cgi.di.uoa.gr/~aggelos/crypto/page4/assets/joux-tripartite.pdf) and by Boneh and Franklin to obtain an [identity-based encryption scheme](https://crypto.stanford.edu/~dabo/papers/bfibe.pdf).
This got the three of them the [Gödel prize in 2013](https://www.eatcs.org/index.php/component/content/article/1-news/1584-goedel-prize-2013).

We will start with the abstract definition of pairing groups and then we will see how to construct such groups from specific elliptic curves.

## Abstract Definition

Let $\GG_1$, $\GG_2$, and $\GG_t$ be three cyclic groups of prime order $r$.
For reasons that will become clear later, we will denote $\GG_1$ and $\GG_2$ additively and $\GG_t$ multiplicatively (in particular, $\GG_1$ and $\GG_2$'s identity elements are denoted $0$ while $\GG_t$'s identity element is denoted $1$).
A *pairing* is an efficiently computable function $e \colon \GG_1 \times \GG_2 \to \GG_t$ which satisfies two properties:

- **non-degeneracy**: $P \neq 0$ and $Q \neq 0$ implies $e(P,Q) \neq 1$;
- **bilinearity**: for every $P_1, P_2 \in \GG_1$ and $Q \in \GG_2$ and for every $P \in \GG_1$ and $Q_1, Q_2 \in \GG_2$,
\[\begin{aligned}
 e(P_1 + P_2, Q) & = e(P_1, Q) e(P_2, Q) \\
 e(P, Q_1 + Q_2) & = e(P,Q_1) e(P, Q_2).
\end{aligned}\]

Note that bilinearity  implies the (more useful in practice) property that for every $P \in \GG_1$, $Q \in \GG_2$, and $a,b \in \ZZ_r$,
\[
 e(a P, b Q) = e(P, Q)^{ab}.
\]

Non-degeneracy has many other definitions (all equivalent assuming bilinearity), such as:

- $e$ is not the constant function $1$,
- if $G_1$ and $G_2$ are generators of respectively $\GG_1$ and $\GG_2$, then $e(G_1, G_2)$ is a generator of $\GG_t$.

Constructing groups admitting a pairing is not very hard.
For example, take $\GG_1 = \GG_2 = \ZZ_r$ (the group of integers mod $r$ equipped with addition), take for $\GG_t$ any cyclic group of order $r$, let $g$ be a generator of $\GG_t$, and define $e(x,y) := g^{xy}$.

However, for being useful from a cryptographic point of view, we need the discrete logarithm problem to be hard in the three groups $\GG_1$, $\GG_2$, and $\GG_t$.
(In the example above, while it may be hard in $\GG_t$, it is certainly not in $\GG_1$ and $\GG_2$.)
This is where elliptic curves come to the rescue.

Some more vocabulary: A pairing is said *symmetric* when $G_1 = G_2$ and *asymmetric* when $G_1 \neq G_2$.
As we will see, both types can be constructed from elliptic curves.
Historically, the first proposed constructions were symmetric, but nowadays the asymmetric type prevails for efficiency reasons.
To the best of my knowledge, it is an open problem to construct a pairing such that $\GG_1 = \GG_2 = \GG_t = \GG$ and the discrete logarithm problem is conjectured hard in $\GG$.



## Constructing Pairings

Although we defined the curve equation with coefficients in $\FF$, nothing prevents us to consider which points $(x,y)$ satisfy these equation when $x$ and $y$ are in an *extension* of $\FF$.
From now on, we assume that $\FF$ has prime order $p$ and denote it $\FF_p$.
Let $\FF' = \FF_{p^m}$ be an extension of $\FF_p$ of degree $m$.
We let $E(\FF')$ denote the set of points $(x,y) \in (\FF')^2$ satisfying the curve equation together with the point at infinity:
\[
 E(\FF') = \{(x,y) \in (\FF')^2 : y^2 = x^3 + ax + b\} \cup \{\cO\}.
\]
Since $\FF \subset \FF'$, it is easy to see that $E(\FF) \subset E(\FF')$.
In fact, $E(\FF)$ is a subgroup of $E(\FF')$ as adding two points or inverting a point in $E(\FF)$ yields a point in $E(\FF)$.

How does the group structure of $E(\FF_{p^m})$ evolve as we keep increasing $m$?
This is related to the


An important parameter for defining pairings is the *embedding degree*.
Let $r$ be a prime divisor of $n := |E(\FF)|$.
The embedding degree of $E(\FF)$ with respect to $r$ is the smallest positive integer $k$ such that $r$ divides $p^k-1$, i.e.,
\[
 p^k -1 = 0 \bmod r.
\]
Equivalently, this is the multiplicative order of $p$ modulo $r$.
It is well-defined and it is at most $r-1$ since by [Euler's theorem](https://en.wikipedia.org/wiki/Euler%27s_theorem), $p^{r-1} = 0 \bmod r$.

There are two important properties associated with the embedding degree:

- $k$ is the smallest integer such that $E(\FF_{p^k})[r]$ has order strictly larger than $r$;
- $k$ is the smallest integer such that $\FF_{p^k}$ contains all the *$r$-th roots of unity* over $\FF_p$.
What does that mean exactly?
An $r$-th root of unity

The Weil pairing was

The Tate-Lichtenbaum pairing (often simply called Tate pairing) was introduced in cryptography by [Frey and Rück](https://www.ams.org/journals/mcom/1994-62-206/S0025-5718-1994-1218343-6/S0025-5718-1994-1218343-6.pdf) in a paper extending the MOV attack.

[Ate pairing](https://eprint.iacr.org/2006/110.pdf) and [optimal ate pairing](https://eprint.iacr.org/2008/096.pdf).


## Pairing-Friendly Curves

- supersingluar curves
- MNT and BLS
- BN


## Further Resources

Here are some good resources about pairing-friendly elliptic curves:

- [Pairings for beginners](https://www.craigcostello.com.au/s/PairingsForBeginners.pdf) by Craig Costello
- Section 5.4 of the [Moonmath manual](https://leastauthority.com/community-matters/moonmath-manual/)
- Martijn Maas' [master thesis](https://www.win.tue.nl/~bdeweger/downloads/MT%20Martijn%20Maas.pdf)
- this post about [the security of pairing-friendly curves](https://research.nccgroup.com/2022/03/02/estimating-the-bit-security-of-pairing-friendly-curves/) by Giacomo Pope
- a post about [BLS12-381](https://hackmd.io/@benjaminion/bls12-381) by Ben Edgington
- a post about [BN254](https://hackmd.io/@jpw/bn254) by Jonathan Wang.

----

[^char]: It is possible to define elliptic curves over fields of characteristic 2 or 3 but equations are more complicated.
