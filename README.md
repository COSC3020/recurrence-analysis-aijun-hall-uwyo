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

Base Case: $O(1)$ for return statement when $n <=1$

Loops: First loop runs $n^2$ times. Second inner loop runs $n$ times. Third inner-inner loop runs $n^2$ times. This makes a total of $n^5$ loop iterations

Recursion: `mystery(n/3)` is called 3 times with the input of `n/3`: $3T(\frac{n}{3})$

$$
    T(n) =
    \begin{cases}
        1, & \text{if } n \leq 1 \\
        3T\left(\frac{n}{3}\right) + n^5, & \text{if } n > 1
    \end{cases}
$$

Solving:

$T(n) = 3T(\frac{n}{3}) + n^5$



$T(\frac{n}{3}) = 3T(\frac{\frac{n}{3}}{3}) + (\frac{n}{3})^5$

$T(\frac{n}{3}) = 3T(\frac{n}{9}) + \frac{n^5}{243}$



$T(n) = 3[3T(\frac{n}{9}) + \frac{n^5}{243}] + n^5$

$T(n) = 6T(\frac{n}{9}) + \frac{n^5}{81} + n^5$



$T(\frac{n}{9}) = 3T(\frac{\frac{n}{9}}{3}) + (\frac{n}{9})^5$

$T(\frac{n}{9}) = 3T(\frac{n}{27}) + \frac{n^5}{59049}$



$T(n) = 6[3T(\frac{n}{27}) + \frac{n^5}{59049}] + \frac{n^5}{81} + n^5$

$T(n) = 9T(\frac{n}{27}) + \frac{2n^5}{19683} + \frac{n^5}{81} + n^5$

$T(n) = 9T(\frac{n}{27}) + \frac{19928n^5}{19683}$

<hr>

$$
\text{1. If } n^{\log_b a} > f(n), \text{ then:}
$$

$$
T(n) \in O\big(n^{\log_b a}\big)
$$

$$
\text{2. If } n^{\log_b a} < f(n), \text{ then:}
$$

$$
T(n) \in O\big(f(n)\big)
$$

$$
\text{3. If } n^{\log_b a} = f(n), \text{ then:}
$$

$$
T(n) \in O\big(n^{\log_b a} \log n\big)
$$

<hr>

$3T\left(\frac{n}{3}\right) + n^5$

$a = 3$

$b = 3$

$f(n) = n^5$

$n^{log_3(3)} = 1 < n^5$

Therefore

$T(n) \in \Theta(n^5)$
