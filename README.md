[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

1. Recurrence Relation:

   $T(n) = 1, \text{ if } n \leq 1$
   
   $T(n) = 3T\left(\frac{n}{3}\right) + n^5, \text{ when } n > 1$

2. Expanding Recurrence Relation:

   $T(n) = 3T\left(\frac{n}{3}\right) + n^5$

   $= 3\left(3T\left(\frac{n}{9}\right) + \left(\frac{n}{3}\right)^5\right) + n^5$

   $= 9T\left(\frac{n}{9}\right) + 3\left(\frac{n^5}{3^5}\right) + n^5$

   $= 9T\left(\frac{n}{9}\right) + \frac{n^5}{3^4} + n^5$


   which will eventually lead us to...

4. Substitution:

   $= 3^i T\left(\frac{n}{3^i}\right) + \sum_{j=0}^{i-1} 3^j \left(\frac{n}{3^j}\right)^5$

   Each term in sum represents the contribution of the loops inside the function, considering sizes of $n$ as we go through recursion. At each level of recursion we iterate over a similar structure with a smaller value of    $n$ due to recursive division by 3.

   As we reach the base case $T(1)$, the terms in sum become $1^5 = 1$ because the value of $n$ becomes $1$. So, summing up all these terms approximates to $n^5$.

   Express $T(n)$ as:

   $T(n) = 3^i T(1) + \sum_{j=0}^{i-1} 3^j \left(\frac{n}{3^j}\right)^5$

   $= nT(1) + \text{terms that approximate to } n^5$

   $= n + \text{terms that approximate to } n^5$
   
   $T(n) = 3^iT\left(\frac{n}{3^i}\right) + n^5$

   $\text{Let } i = \log_3{n}$
   
   $= nT(1) + 2n^5$
   
   $= n + 2n^5$


4. Big O Bound:
   
   $n + 2n^5 \in O(n^5)$

   $T(n) \in O(n^5)$

Sources: Used google/ai to make the recurrence relation



