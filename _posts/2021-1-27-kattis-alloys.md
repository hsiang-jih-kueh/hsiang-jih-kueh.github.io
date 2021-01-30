---
layout: post
title: kattis - alloys
category: competitive programming
tags: [kattis]
---

[link to problem](https://open.kattis.com/problems/alloys)

This is basically an optimisation problem that can be stated as follows:

$$
\begin{equation}
\begin{aligned}

& \underset{x, y}{\text{maximise}}
& & xy \\

& \text{subject to}
& & x + y + z = 1 \\
&
& & 0 \leq x,y,z \leq 1 \\
&
& & x + y \leq c\; (0\leq c\leq 2)
\end{aligned}
\end{equation}
$$

Note that the objective function is independent of $z$, so $z$ is basically just a value we can twiddle to allow $x+y$ to equal anything from $0$ to $1$ whilst still obeying the constraint of $x + y + z = 1$.

In other words, it allows us to relax the equality $x + y + z = 1$ to an inequality $0 \leq x + y \leq 1$.

The optimisation problem can now be rewritten as:

$$
\begin{equation}
\begin{aligned}

& \underset{x, y}{\text{maximise}}
& & xy \\

& \text{subject to}
& & 0 \leq x + y \leq 1 \\
&
& & x + y \leq c\; (0\leq c\leq 2)\\
&
& & 0 \leq x,y\leq 1 \\
\end{aligned}
\end{equation}
$$

Given that two of the inequality constraints are  the same function $x + y$, this problem can be further simplified by breaking it down into two cases, one where $0\leq c \leq 1$ and one where $1 < c \leq 2$, which will allow us to combine them as follows.

----

In the first case where $0\leq c < 1$, we can rewrite the problem as:

$$
\begin{equation}
\begin{aligned}

& \underset{x, y}{\text{maximise}}
& & xy \\

& \text{subject to}
& & 0 \leq x + y \leq c\\
&
& & 0 \leq x,y\leq 1 \\
\end{aligned}
\end{equation}
$$

Throwing mathematical rigour out the window and solely using intuition, if we want to maximise $xy$, we should try to allow $x$ and $y$ to be as large as possible, which means that $x + y$ should be as large as possible, i.e. $x + y = c$.

$$
\begin{equation}
\begin{aligned}

& \underset{x, y}{\text{maximise}}
& & xy \\

& \text{subject to}
& & x + y = c\\
&
& & 0 \leq x,y\leq 1 \\
\end{aligned}
\end{equation}
$$

Squinting our eyes so that we can pretend to not see the constraint that $0\leq x,y\leq1$, we solve the optimisation problem using Lagrange multipliers to get $y = \lambda$ and $x = \lambda$. So, $c = \lambda + \lambda = 2\lambda$. And since $c \in [0,1]$, then $\lambda \in [0,0.5]$, implying that $x,y \in [0,0.5]$, which means that our optimal solution also satisfies the original constraint of $0\leq x,y\leq 1$. Thus, $xy$ has a maximal value of $\frac{c}{2}^2$.

----

Similarly, for the second case where $1 \leq c \leq 2$:

$$
\begin{equation}
\begin{aligned}

& \underset{x, y}{\text{maximise}}
& & xy \\

& \text{subject to}
& & 0 \leq x + y \leq 1\\
&
& & 0 \leq x,y\leq 1 \\
\end{aligned}
\end{equation}
$$

Which, making mathematicians cry for the second time can be rewritten as:

$$
\begin{equation}
\begin{aligned}

& \underset{x, y}{\text{maximise}}
& & xy \\

& \text{subject to}
& & x + y = 1\\
&
& & 0 \leq x,y\leq 1 \\
\end{aligned}
\end{equation}
$$

And when similarly solved via Lagrange multipliers, gives us $xy$ having a maximal value of $0.25$.

----

Thus, when $0 \leq c < 1$, the maximal value of xy is $\frac{c}{2}^2$, but when $1 \leq c \leq 2$, the maximal value of xy is $0.25$.