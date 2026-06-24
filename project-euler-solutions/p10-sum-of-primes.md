## Problem 10: [Summation of Primes](https://projecteuler.net/problem=10)

sum of primes < n;
again, to find primes, you'll need to start from 2, mark all 2 multiples as non-prime, move onto 3, mark all 3 multiples as non-prime and so on

one tracker is for storing all the primes
and max range (not inclusive), would ne n (2 >= c < n)

you could mark p sq, p sq +p etc as composite too - as an optimisation

## py solution

```
def sieve(n):
    is_prime = [False, False] + [True] * (n - 2)
    for p in range(2, int(n**0.5) + 1):
        if is_prime[p]:
            for m in range(p*p, n, p):
                is_prime[m] = False
    primes = [i for i, v in enumerate(is_prime) if v]
    return primes, sum(primes)

primes, total = sieve(50)
print(primes)
print(total)
```
