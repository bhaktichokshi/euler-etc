## Problem 17: [Number Letter Counts](https://projecteuler.net/problem=17)

we'll need a map to store numbers to words for 1 to 19, and also the tens (10, 20, 30 etc)
rest of them can be built

1-19 -> direct lookup
20-99 -> tens place (round down to nearest 10) + ones place (eg 47 -> forty + seven)
100-999 -> hundreds digit + "hundred" + "and" + remainder (eg 342 → three + hundred + and + forty + two)
1000 → one + thousand (special case, only one in range)

## py solution
```
def count_letters(n):
    ones = {1:'one',2:'two',3:'three',4:'four',5:'five',
            6:'six',7:'seven',8:'eight',9:'nine',10:'ten',
            11:'eleven',12:'twelve',13:'thirteen',14:'fourteen',
            15:'fifteen',16:'sixteen',17:'seventeen',18:'eighteen',19:'nineteen'}
    tens = {20:'twenty',30:'thirty',40:'forty',50:'fifty',
            60:'sixty',70:'seventy',80:'eighty',90:'ninety'}

    if n in ones:
        return len(ones[n])
    
    elif n in tens:
        return len(tens[n])
    
    elif 20 < n < 100:                          # e.g. 47 → forty + seven
        return len(tens[n - n%10]) + len(ones[n%10])
    
    elif 100 <= n < 1000:
        hundreds_part = len(ones[n//100]) + len('hundred')
        remainder = n % 100
        if remainder == 0:                      # exact hundred, no "and"
            return hundreds_part
        else:                                   # add "and" (3 letters) + remainder
            return hundreds_part + 3 + count_letters(remainder)
    
    elif n == 1000:
        return len('one') + len('thousand')     # onethousand = 11


total = sum(count_letters(n) for n in range(1, 1001))
print(total)  # 21124
```
