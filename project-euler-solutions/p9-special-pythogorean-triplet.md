## Problem 9: [Special Pythagorean Triplet](https://projecteuler.net/problem=9)

given,
a + b + c = 1000
a sq = b sq + c sq (pythogoras theorem)

keep n = 1000 (so we can simply derive eq based on n, and not mess up numbers)

you can choose to dervice for any one of a, b or c; i am choosing b 

```
b = n - a - c 

also,
a³ = a * a² = a(b² - c²)
and 
n³ = a³ + b³ + c³ + 3(a²b + a²c + b²a + b²c + c²a + c²b) + 6abc

substituting in a sq = b sq + c sq;

a²b + a²c  →  (b²-c²)b + (b²-c²)c  =  b³ - bc² + b²c - c³

b²a + c²a  →  a(b² + c²)  =  (n-b-c)(b²+c²)

b²c + c²b  →  bc(b+c)

so basically, 
b = (n² - 2nc + 2c²) / 2(n - c)
and for n = 1000
b = (1000000 - 2000c + 2c²) / 2(1000 - c)
```

## py solution based on above eqs
```
for c in range(1, 1000):
    numerator = 1000000 - 2000*c + 2*c**2
    denominator = 2*(1000 - c)
    
    if numerator % denominator == 0:        # b must be integer
        b = numerator // denominator
        a = 1000 - b - c
        
        if a > 0 and b > 0 and c > 0:       # all must be positive
            print(f"a={a}, b={b}, c={c}")
            print(f"Check a²+c²=b²: {a**2 + c**2} = {b**2}")
            print(f"abc = {a * b * c}")
            break
```
