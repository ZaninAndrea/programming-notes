# Week 3
<!-- toc -->
## Lecture
see official notes

## Short: Computational complexity
Computational complexity represents how well our algorithm scales as the data gets bigger and bigger.

We generally talk about the **worst-case-scenario** complexity of an algorithm, aka **O**. But sometimes we care about the **best-case-scenario**, aka $$\Omega$$.

Computational complexity represents how well our algorithm scales as the data gets bigger and bigger.
While calculating computational complexity we will generally ignore all the elements lower-order terms, e.g. in the expression $$n^3 -8n^2 +20n$$ we will only care about $$n^3$$

|O notation| name |
|---|---|
|O(1)| constant time |
|O(log n)| logarithmic time |
|O(n)|linear time|
|O(n log n)|linearithmic time|
|O($$n^2$$)| quadratic time|
|O($$n^c$$)| polynomial time|
|O($$c^n$$)| exponential time|
|O(n!)| factorial time|
|O($$\infty$$)| infinite time|

O(1) stands for constant time, which include also constant time different from 1.

