# Kruskal's algorithm (Minimum Spanning Tree)

#### Intuition

Kruskal's algorithm processes the edges in order of their weight values (smallest to largest), taking for the MST each edge that does not form a cycle with edges previously added, stopping after adding V-1 edges.


#### Implementation

– use a priority queue to consider the edges in order by weight

– use a union-find data structure to identify those that cause cycles

– use a queue to collect the edges belonging to the MST

```python
def kruskal(edges, vcount):
    heap = Heap(edges, lt=lambda left, right: left.weight < right.weight)
    mst = []
    uf = UnionFind(vcount)

    while heap and len(mst) < vcount - 1:
        edge = heap.pop()

        if not uf.connected(edge.from, edge.to):
            mst.append(edge)
            uf.union(edge.from, edge.to)

    return mst
```


#### Runtime complexity

*O(E log E) = O(E log V)*


#### Space complexity

*O(E)*


#### Resources

https://en.wikipedia.org/wiki/Kruskal%27s_algorithm#Complexity

http://algs4.cs.princeton.edu/43mst/
