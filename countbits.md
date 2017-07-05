# Count set bits in an integer

Write a function that takes an unsigned integer and returns the number of 1 bits it has.


### A naive approach

```python
def count(n):
    acc = 0

    while n > 0:
        acc += n & 1
        n >>= 1

    return acc
```

Time complexity: (-)(log n)

### A better approach: Brian Kernighan’s algorithm

This solution relies on a bit manipulation trick. Notice what is the bit representation of n - 1. The least significat bit is unset and all the following bits are set:

`n     = 20 = 10100`

`n - 1 = 19 = 10011`

This means that `n & (n - 1)` unsets the least significant bit of n.

```python
def count(n):
    acc = 0

    while n > 0:
        acc += 1
        n &= n - 1

    return acc
```

Time complexity: O(log n)

### Bonus: find whether a number is a power of two

All power of two numbers have only one bit set. As a result, if n is a power of two, then expression n & (n - 1) is equal to 0.

### Resources

http://www.graphics.stanford.edu/~seander/bithacks.html

http://www.geeksforgeeks.org/count-set-bits-in-an-integer/

http://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/
