# Problem 15: [Lattice Paths](https://projecteuler.net/problem=15)

every path from top-left to bottom-right on an n×n grid takes exactly 2n steps (n rights and n downs), in any order

basically combination(2n,n)

and comb(a,b)=a! / (b! * (a-b)!):

### py solution based on comb(a,b)
```
def factorial(n):
    res = 1
    for i in range(1,n+1):
        res *= i
    return res

def comb(a,b):
    return factorial(a)//(factorial(b)*factorial(a-b))
```
