## Problem 7: [10001st Prime](https://projecteuler.net/problem=7)

i need to find nth prime number mathematically

so what i am thinking is 
lets start from 2 which is the first, and then you go to 3, mark everything divisble by 2 as out of list since they'll not be prime, so i will need to skip from 3 to 5, and again anything divisible by 3 will be marked as not prime etc 

so i have one area where i am storing primes as i am going thru them 
and to find nth prime, i just need to track the length of that list and when i reach required length of n-1 , thats the nubmer i am looking for

### python solution:
```
def nth_prime(n):
    primes = []
    is_prime = {}
    candidate = 2

    while len(primes) < n:
        if candidate not in is_prime:          # not marked → it's prime
            primes.append(candidate)
            # mark all multiples of candidate as not prime
            multiple = candidate * candidate   # start from p² (optimization)
            while multiple <= candidate * n:   # rough upper bound
                is_prime[multiple] = False
                multiple += candidate
        candidate += 1

    return primes[-1]

print(nth_prime(1))   # 2
print(nth_prime(5))   # 11
print(nth_prime(10))  # 29
```

### catch
if i go without an estimated upper bound, it would be heavy calc, 
so calulating known upper bound here,
for nth prime: n * log(n * log(n)) for n >= 6

```
import math

def nth_prime(n):
    # Upper bound estimate for nth prime: n * log(n * log(n)) for n >= 6
    if n < 6:
        limit = 15
    else:
        limit = int(n * (math.log(n) + math.log(math.log(n)))) + 3

    sieve = [True] * (limit + 1)
    sieve[0] = sieve[1] = False

    for p in range(2, int(math.sqrt(limit)) + 1):
        if sieve[p]:                           # p is prime
            for multiple in range(p*p, limit + 1, p):
                sieve[multiple] = False        # mark composites

    primes = [i for i, val in enumerate(sieve) if val]
    return primes[n - 1]

print(nth_prime(1))    # 2
print(nth_prime(5))    # 11
print(nth_prime(10))   # 29
print(nth_prime(100))  # 541
```

## another cool trick
2 is the only eve prime (obv)
all prime numbers after 3 can be simply written as 6k + or - 1 (eg, 5,7,11,13....)
you could check just for the 6k+1s and 6k-1s; make sure to remove any candidate that is already divisble by prime so you do not accidently add digit there. 
this is really helpful in case you have no idea what the upper bound is, and estimates can't be made 
