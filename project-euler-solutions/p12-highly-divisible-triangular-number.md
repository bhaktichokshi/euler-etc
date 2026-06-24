Problem 12: [Highly Divisible Triangular Number](https://projecteuler.net/problem=12)

seq of triangle numbers is basically seq of sum till that number (n*(n+1)/2)

goal is to find the first triangle number to have above n divisors. 

one thing at a time,
finding all divisors of a number n, you'll need to travarse from 1 to root of n (you can travarse from 1 to n, but for a pair a * b = n, atleast one of them needs to fall between 1 and root of n and if both were greater than root of n, the product would be greater than n - which is not possible)

so easiest approach is to travarse triangle series, and then keep track of their divisors. 

### find all divisors

```
def count_divisors(n):
    count = 0
    i = 1
    while i * i <= n: # i is less than root of n
        if n % i == 0:
            count += 2        # i and n//i are both divisors
            if i * i == n:
                count -= 1    # perfect square, don't double count
        i += 1
    return count
```

### triangle
```
def triangle(n):
    return n * (n + 1) // 2
```

### all together
```
def first_triangle_with_divisors(x):
    n = 1
    while True:
        t = triangle(n)
        if count_divisors(t) > x:
            return t
        n += 1
```
