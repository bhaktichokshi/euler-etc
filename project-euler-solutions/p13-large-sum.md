Problem 13: [Large Sum](https://projecteuler.net/problem=13)

i need to find how much was carry forwarded for those n columns; 
chop off extra, and keep only necessar 

example,
12345678901234567890...  (50 digits)
// 10**37
= 1234567890123          (top 13 digits)

general rule of thumb: keep k + len(count_of_numbers) digits from each number

# py solution
```
trimmed = [n // 10**(len(str(n)) - 13) for n in numbers]
str(sum(trimmed))[:10]
```
