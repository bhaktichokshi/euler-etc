## Problem 8: [Largest Product in a Series](https://projecteuler.net/problem=8)

to check for n adj numbers in a series, i need to make sure i keep track of those n and their products

so moving ahead would look like
division of 1st in the series 
multiply with the next one 

like you have 123424
and youre supposed to find 3 adj 

so you start with 123 
track product ; which is 6 in this case
then to move ahead, you multiply with 4 and divide with 1 ; update product to 6*4/1 = 24 
and now again, 24*2/2 , which is same
24*4/3 is last

this could mean you are tracking running product internally, and max of products centrally

one thing to note is, 
if you ever encounter 0, (obv) dividing by 0 would mean undefined, and multiplying the running and max product with 0 will always mean 0 even when you have moved ahead.
to keep track of this, you could just make the product = 1 in case you have 0 in your window. 

## python solution
```
def largest_product_in_series(series, n):
    digits = [int(c) for c in series]
    max_product = 0

    for i in range(len(digits) - n + 1):
        window = digits[i:i+n]
        if 0 in window:
            continue                          # skip, product will be 0
        product = 1
        for d in window:
            product *= d
        max_product = max(max_product, product)

    return max_product
```
