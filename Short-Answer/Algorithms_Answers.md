# Exercise I
## a)
Time complexity is `O(n)`.

There is only one loop.  With each iteration of the loop, `a` increases by `n^2`.  How many iterations does it take for a sum of `n^2` to equal `n^3`?  The answer is `n`.

```python
a = 0
while (a < n * n * n): # Time n
    a = a + n * n
```

## b)
Time complexity is `O(n^3)`.

There's several loops, most of them (but not all) with running times proportional to `n`.  The number of iterations in the inner loops is slightly smaller than `n` in each case, but it is smaller than `n` by a small amount that doesn't scale with `n`.  Thus, they don't affect our calculations.

```python
sum = 0
for i in range(n): # n
    i += 1
    for j in range(i + 1, n): # n
        j += 1
        for k in range(j + 1, n): # n
            k += 1
            for l in range(k + 1, 10 + k): # constant (10)
                l += 1
                sum += 1
```

Overall complexity is thus `n * n * n * 10`, which simplifies to `n^3`.


## c)
Time complexity is `O(n)`.

When you call `bunnyEars(n)`, the function will run once and then call itself for `n-1`.  Thus, the function winds up being called `n` times.

```python
def bunnyEars(bunnies):
    if bunnies == 0:
        return 0

    return 2 + bunnyEars(bunnies-1) # This will run n times
```

# Exercise II
The building is an ordered list of floors, because each subsequent floor is a bit taller than the other and thus that much closer to the egg breaking height.  The egg is a variable with unknown value that fits in the ordered list, at floor f.  So this problem is about searching on an ordered list.

The baseline naive solution is to go up floor by floor, dropping eggs until you find f.  The performance of that would be `O(n)`, assuming that the value of `f` is truly unknown and can be as high as the last floor of an arbitrarily tall building.  In other words, we'll have to break a number of eggs that is proportional to `n` (and `n` itself in the worst case).

A better solution is a binary search.  Start at the middle of the building and drop an egg.  If it cracked, now search only in the bottom half of the building.  Otherwise, search only in the top half. Repeat that process recursively until you find f.  This process should run in `O(log(n))`, and result at most in `log(n)` cracked eggs.