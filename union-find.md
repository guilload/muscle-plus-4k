# Union-find

#### Intuition

The connected components are represented as forest of trees.


#### Implementation

– the parent of a node at index *i* is found at *A[i]*, if `i == A[i]`, then node *i* is the root of the tree

– rather than arbitrarily connecting the second tree to the first for `union(...)`, keep track of the size of each tree and always connect the smaller tree to the larger

```python
class UnionFind(object):

    def __init__(self, capacity):
        self._array = range(capacity)
        self._sizes = [1] * capacity
        self.count = capacity

    def connected(self, p, q):
        return p == q or self.find(p) == self.find(q)

    def find(self, p):
        while p != self._array[p]:
            p = self._array[p]

        return p

    def union(self, p, q):
        if p != q:
            proot = self.find(p)
            qroot = self.find(q)

            if proot != qroot:
                psize = self._sizes[proot]
                qsize = self._sizes[qroot]

                if psize < qsize:
                    self._array[proot] = qroot
                    self._sizes[qroot] += psize
                else:
                    self._array[qroot] = proot
                    self._sizes[proot] += qsize

                self.count -= 1
```


#### Runtime complexity

init: *O(n)*

connected: *O(log n)*

find: *O(log n)*

union: *O(log n)*


#### Space complexity

*O(n)*


#### Resources

https://en.wikipedia.org/wiki/Disjoint-set_data_structure

http://algs4.cs.princeton.edu/15uf/
