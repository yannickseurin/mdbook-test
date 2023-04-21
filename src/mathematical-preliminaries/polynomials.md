# Polynomials

## Generalities

Let $\FF$ be a field (not necessarily finite).
A (univariate) *polynomial* with coefficients in $\FF$ is an infinite sequence $(a_i)_{i \in \NN}$ such that $a_i=0$ for all but a finite number of indices $i$.
Polynomials are traditionally denoted
\[
 p(X) = a_0 + a_1 X  + a_2 X^2 + \cdots = \sum_{i=0}^{\infty} a_i X^i
\]
where $X$ is a symbol called *indeterminate*.

The set of all univariate polynomials over $\FF$ is denoted $\FF[X]$:
\[
 \FF[X] := \left\{ \sum_{i=0}^\infty a_i X^i : a_i \in \FF, \exists N \in \NN, \forall i \ge N, a_i = 0 \right\}.
\]

Polynomials can be added:
\[
 \sum_{i=0}^\infty a_i X^i + \sum_{i=0}^\infty b_i X^i = \sum_{i=0}^\infty (a_i+b_i) X^i.
\]

Polynomials can also be multiplied:
\[
 \sum_{i=0}^\infty a_i X^i \cdot \sum_{j=0}^\infty b_j X^j = \sum_{k=0}^\infty c_k X^k \quad \text{with} \quad c_k = \sum_{i+j=k} a_i b_j.
\]

The set $\FF[X]$ equipped with operations $+$ and $\cdot$ is a ring called the *polynomial ring* in $X$ over $\FF$.
Moreover, if we define scalar multiplication of a polynomial $p(X)$ by $a \in \FF$ as multiplication by the constant polynomial $a(X) = a$, then $\FF[X]$ is a vector space over $\FF$.
The set $\{1, X, X^2, \dots\}$ is a basis of this vector space called the *monomial* basis.

The *degree* of a polynomial $p(X)$ is the largest power of $X$ occurring in $p(X)$ with a non-zero coefficient, with the convention that polynomial $0$ has degree $-\infty$.
Hence, $p(X) = \sum_{i=0}^d a_i X^i$ has degree $d$ provided $a_d \neq 0$.
We let $\deg(p)$ denote the degree of a polynomial $p$ and $\PR{d}$ denote the set of polynomials over $\FF$ of degree at most $d$.

Given two non-zero polynomial $a(X)$ and $b(X)$, we say that $b(X)$ *divides* $a(X)$ or that $b(X)$ is a *factor* of $a(X)$ if there exists a polynomial $q(X)$ such that $a(X)=q(X)b(X)$.
The set $\FF[X]$ is a Euclidean domain, meaning one can perform euclidean division in $\FF[X]$: given two polynomials $a(X)$ and $b(X)$ with $b(X) \neq 0$, there exists unique polynomials $q(X)$ and $r(X)$ such that $a(X) = q(X) b(X) + r(X)$ and $\deg(r) < \deg(b)$.

Given a polynomial $p(X) = \sum_i a_i X^i$ in $\FF[X]$ and an element $u \in \FF$, the *evaluation* of $p(X)$ at $u$, written $p(u)$, is $\sum_i a_i u^i$.
We say that $u$ is a *root* of $p(X)$ if $p(u) = 0$.
A consequence of $\FF[X]$ being Euclidean is that $u$ is a root of $p(X)$ if and only if $X-u$ divides $p(X)$.
More generally, $p(u) = v$ if and only if $X-u$ divides $p(X)-v$.
(This will play an important role for the KZG scheme.)

$\todo{add proofs}$

Let $p$ be a non-zero polynomial of degree $d$. Then $p$ has at most $d$ distinct roots in $\FF$.
This can easily be shown from the previous proposition by induction on $d$.

## Lagrange Interpolation

In all the following, a set $\cD = \{x_0, \dots, x_d\}$ of distinct field elements $x_i \in \FF$ will be called an *evaluation domain* (or simply *domain*) of size $d+1$.

A fundamental result about polynomials is that given $d+1$ points $(x_i, y_i)_{0 \le i \le d} \in \FF^2$ with distinct abscissas, i.e. $x_i \neq x_j$ for $i \neq j$, there is a unique polynomial $p(X) \in \PR{d}$ such that $p(x_i) = y_i$ for every $i \in \{0, \dots, d\}$.
It is called the [Lagrange interpolating polynomial](https://en.wikipedia.org/wiki/Lagrange_polynomial).

Uniqueness is proved as follows: assume there exists two polynomials $p(X)$ and $q(X)$ interpolating the $d+1$ points.
Then the polynomial $p(X)-q(X)$ has $d+1$ roots but has degree at most $d$, hence must be the 0 polynomial, which implies that $p(X) = q(X)$.

To establish existence, one introduces the *Lagrange basis* associated with the domain $\cD = \{x_0, \dots, x_d\}$.
This is the tuple of degree-$d$ polynomials $(\ell_0(X), \dots, \ell_d(X))$ defined as
\[
 \ell_j(X) := \prod_{\substack{0 \le k \le d \\ k \neq j}} \frac{X-x_k}{x_j-x_k}.
\]

One can easily check that
\[
 \ell_j(x_i) =
 \begin{cases}
  0 & \text{if } j \neq i \\
  1 & \text{if } j=i.
 \end{cases}
\]

Then the Lagrange interpolating polynomial for $(x_i, y_i)_{0 \le i \le d}$ is given by
\[
\ell(X) := \sum_{j=0}^d y_j \ell_j(X).
\]
This polynomial has degree at most $d$ and it is easy to see that $\ell(x_i) = y_i$ for every $i \in \{0,\dots,d\}$.

Note that the Lagrange basis is indeed a basis for the $\FF$-vector space $\PR{d}$ in the linear algebra sense.
The coordinates of a polynomial $p \in \PR{d}$ in this basis are $(p(x_0), \dots, p(x_d))$.

An important application of Lagrange interpolation is [Shamir's secret sharing](https://en.wikipedia.org/wiki/Shamir%27s_secret_sharing).
