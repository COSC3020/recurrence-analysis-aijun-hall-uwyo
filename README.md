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
General form of k expansions


$T(n) = 3^k  T(\frac{n}{3^k}) + \sum_{i=0}^{k-1} 3^i  (\frac{n}{3^i})^5$

$3^i (\frac{n}{3^i})^5 = \frac{3^i n^5}{3^{5i}} = \frac{n^5}{3^{4i}}$

$T(n) = 3^k T(\frac{n}{3^k}) + \sum_{i=0}^{k-1} (\frac{n^5}{3^{4i}})$

Stop reccurence at:

$\frac{n}{3^k} = 1 \ \rightarrow \ 3^k = n \ \rightarrow \ k = log_3(n)$

$T(n) = 3^k  T(\frac{n}{3^k}) + \sum_{i=0}^{k-1} (\frac{n^5}{3^{4i}})$

Because $3^k = n$ and $T(1) = \Theta(1)$:

$T(n) = n  \Theta(1) + \sum_{i=0}^{log_3(n) - 1} (\frac{n^5}{3^{4i}})$

$\sum_{i=0}^{log_3(n) - 1} (\frac{n^5}{3^{4i}}) = n^5  \sum_{i=0}^{log_3(n) - 1} (\frac{1}{81})^i$

<hr>

Geometric Series of:

$\sum_{i=0}^{k-1} r^i = \frac{(1 - r^k)}{(1 - r)}$

$r = \frac{1}{81}$,
$k = log_3(n)$

$T(n) = \Theta(n) + n^5 (1 - (\frac{1}{81})^{log_3(n)}) \div (1 - \frac{1}{81})$

$T(n) = \Theta(n) + n^5 (1 - \frac{1}{n^4}) \div (\frac{80}{81})$

$T(n) = \Theta(n) + \Theta(n^5) (1 - \frac{1}{n^4})$

$\Theta(n^5)$ grows larger and faster than all other elements, therefore

$T(n) \in \Theta(n^5)$

<hr>

- Used help from my divide-and-conquer readme to show work and format
- Used [symbolab](https://www.symbolab.com/) to help work through simplifying expressions 

"I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice."
