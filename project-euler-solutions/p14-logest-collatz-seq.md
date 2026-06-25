# Problem 14: [Longest Collatz Sequence](https://projecteuler.net/problem=14)

to count the chain numbers for given n, we can simply traverse
```
n = 13
c = 0
while True:
    if n%2 == 0: # eve
        n = n/2
    else:
        n = 3*n +1 
    c += 1
    if n == 1:
        break
print(c)
```

but to do this for all numbers one by one, that would be costly and a bit unnecessary. 
instead, choose to cache numbers for which we have already counted chain count.

### py solution w/ caching
```
def longest_collatz(limit):
    cache = {1: 0}
    
    def chain_len(n):
        if n in cache:
            return cache[n]
        if n % 2 == 0:
            result = 1 + chain_len(n // 2)
        else:
            result = 1 + chain_len(3 * n + 1)
        cache[n] = result
        return result
    
    return max(range(1, limit), key=chain_len)

print(longest_collatz(1000000))
```
