## Problem 20: [Factorial Digit Sum](https://projecteuler.net/problem=20)

first step it to get factorial (but be smart, cache results); then simply sum
```
def factorial(n, cache_map={}):
    res = 1
    for i in range(1, n+1):
        if i in cache_map:
            cache_map[n] = res * cache_map[i]
            return cache_map[n]
        res *= i
    cache_map[n] = res
    return res

cache_map = {}
for n in range(1, 101):
    factorial(n, cache_map)

print(sum(int(d) for d in str(cache_map[100])))
```
