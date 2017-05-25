# Fisher–Yates Shuffle

#### Intuition

Shuffling *n* elements is equivalent to choosing one permutation from *n!*, i.e., first choosing 1 element from *n*, then 1 from *n - 1*, etc.

#### Implementation

```python
import random


def shuffle(array):
    if len(array) > 1:
        n = len(array) - 1  # last index
        for i in range(0, n):
            k = random.randint(i, n)  # inclusive range [i:n]
            if i != k:
                array[i], array[k] = array[k], array[i]
```

#### Runtime complexity

*O(n)*

#### Space complexity

*O(1)*

#### Resources

https://en.wikipedia.org/wiki/Fisher-Yates_shuffle

http://eli.thegreenplace.net/2010/05/28/the-intuition-behind-fisher-yates-shuffling/
