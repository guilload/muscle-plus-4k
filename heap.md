# Binary heap

#### Intuition

A heap is a tree data structure that satisfies the heap property: in a **min** heap, the keys of parent nodes are **less** than or equal to those of the children.


#### Implementation

– usually based on an array (fixed size or dynamic array)

– **1-indexed** arrays make the math more convenient

– if a node is at index `k`, then its left child is at index `2 * k`, its right child is at index `2 * k + 1`, and its parent is at index `k / 2`

– to add a new element, add the new item at the end of the array and then swim up through the heap with that item to restore the heap condition

– to remove the root, take the smallest item off the top, put the item from the end of the heap at the top, and then sink down through the heap with that item to restore the heap condition

– to build a heap over n elements in linear time, since the leaves are already valid "sub-heaps", it's only necessary to bubble up the elements of the **first half** of the array, working **from end to start**

```python
class Heap(object):
    """
    Minimum binary heap
    """
    @staticmethod
    def merge(*heaps):
        array = [None]

        for heap in heaps:
            array.extend(heap._array[1:])

        return Heap(array)

    def __init__(self, array=None):
      self._array = [None]  # 1-indexed array

      if array:
        self._array.extend(array)
        self.heapify()

    def __len__(self):
        return len(self._array) - 1

    def heapify(self):
        """
        Floyd algorithm, runs in O(n) time
        """
        for i in range(len(self._array) / 2, 0):
            self._siftdown(i)

    def peek(self):
        return self._array[1]

    def pop(self):
        self._swap(1, -1)  # swap root and last element
        value = self._array.pop()
        self._siftdown(1)  # restore heap property
        return value

    def push(self, value):
        self._array.append(value)
        self._siftup()  # restore heap property

    def _siftdown(self, i):
        array = self._array
        j = i * 2  # left child

        while j < len(array):

            # select min(leftchild, rightchild)
            if j + 1 < len(array) and array[j + 1] < array[j]:
                j += 1

            if array[i] <= array[j]:  # heap property is satisfied
                break

            self._swap(i, j)
            i = j
            j = i * 2

    def _siftup(self):
        array = self._array
        i = len(array) - 1  # last element

        while i > 1 and array[i / 2] > array[i]:
            self._swap(i / 2, i)
            i /= 2

    def _swap(self, i, j):
        self._array[i], self._array[j] = self._array[j], self._array[i]
```


#### Runtime complexity

heapify: *O(n)*

merge: *O(n)*

peek: *O(1)*

pop: *O(log n)*

push: *O(log n)*


#### Space complexity

*O(n)*


#### Resources

https://en.wikipedia.org/wiki/Heap_(data_structure)

http://algs4.cs.princeton.edu/24pq/

https://stackoverflow.com/questions/6299859/how-can-stdmake-heap-be-implemented-while-making-at-most-3n-comparisons/6300047#6300047

https://www.youtube.com/watch?v=MiyLo8adrWw
