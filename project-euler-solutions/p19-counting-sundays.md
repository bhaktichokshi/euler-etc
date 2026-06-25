# Problem 19: [Counting Sundays](https://projecteuler.net/problem=19)

step 1 is to define leap year 
```
def is_leap(year):
    if year % 400 == 0:
        return True
    elif year % 100 == 0:
        return False
    elif year % 4 == 0:
        return True
    else:
        return False
```

step 2 is to get days of month
```
def days_in_month(month, year):
    days = {
        1: 31, 2: 28, 3: 31, 4: 30,
        5: 31, 6: 30, 7: 31, 8: 31,
        9: 30, 10: 31, 11: 30, 12: 31
    }
    if month == 2 and is_leap(year):
        return 29
    return days[month]
```

## final - trace thru it all
note: start day is 1st jan, 1901, which will be tuesday since 1900 was a non-leap year having 365 days so we shift by 1 (monday to tuesday)

```
def count_sundays():
    count = 0
    day = 1  # Tuesday, Jan 1 1901

    for year in range(1901, 2001):
        for month in range(1, 13):
            if day == 6:           # is the 1st a Sunday?
                count += 1
            day = (day + days_in_month(month, year)) % 7

    return count

print(count_sundays())  # 171
```
