## Problem 18: [Maximum Path Sum I](https://projecteuler.net/problem=18)

my first instinct is to keep track of row , row + 1 and row + 2
now in order to maximise the sum, you need to see if the number you are selecting is the most optimal choice for the next to next as well (because if i go from 3 to 7 and then i have to settle for 4 because i wont be able to access 6, but i am ok with that because i can compensate with 9)


eg\
3\
7 4\
2 4 6\
8 5 9 3

r 3 - default\
r+1 7,4 - at this point, i have combinations of 3,7,2; 3,7,4; 3,4,4; 3,4,6\
r+2 2,4,6

max will be 3+7+4 = 14 

then\
r 7\
r+1 4\
r+2 8,5,9,3\
but at this point i have to choose from 7,4,5 of 7,4,9 

but this could go wrong if the 4th row is just bigger or smaller - so this means that i should quite literally track all rows? 

we can move upward instead, start from bottom row, check both child for all; make a decision to pick max and then move forward

```
triangle = [
    [75],
    [95, 64],
    [17, 47, 82],
    [18, 35, 87, 10],
    [20,  4, 82, 47, 65],
    [19,  1, 23, 75,  3, 34],
    [88,  2, 77, 73,  7, 63, 67],
    [99, 65,  4, 28,  6, 16, 70, 92],
    [41, 41, 26, 56, 83, 40, 80, 70, 33],
    [41, 48, 72, 33, 47, 32, 37, 16, 94, 29],
    [53, 71, 44, 65, 25, 43, 91, 52, 97, 51, 14],
    [70, 11, 33, 28, 77, 73, 17, 78, 39, 68, 17, 57],
    [91, 71, 52, 38, 17, 14, 91, 43, 58, 50, 27, 29, 48],
    [63, 66,  4, 68, 89, 53, 67, 30, 73, 16, 69, 87, 40, 31],
    [ 4, 62, 98, 27, 23,  9, 70, 98, 73, 93, 38, 53, 60,  4, 23],
]

# start from second last row, work upward
dp = triangle[-1][:]                        # bottom row is base case

for row in range(len(triangle) - 2, -1, -1):
    for col in range(len(triangle[row])):
        # each cell picks the better of the two children below it
        dp[col] = triangle[row][col] + max(dp[col], dp[col+1])

print(dp[0])  # 1074
```


this one - i still am confused. to me, both upward and downward are greedy. i dont see why 2nd is DP.
