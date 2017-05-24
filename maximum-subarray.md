# Maximum subarray: Kadane's algorithm

#### Intuition

If we know the maximum subarray sum `S` ending at position *i - 1*, then the maximum subarray sum at position *i* is either `S + array[i]` or `array[i]`. Thus, we can compute the maximum subarray sum ending at position *i* for all positions *i* and simply keep track of the maximum.

#### Implementation

```python
def maxsubarray(array):
    currentsum = maxsum = array[0]

    for x in array[1:]:
        currentsum = max(currentsum + x, x)
        maxsum = max(maxsum, currentsum)

    return maxsum
```

#### Runtime complexity

*O(n)*

#### Resources

https://leetcode.com/problems/maximum-subarray
