# Critical Routers

You are given an undirected connected graph. An articulation point (or cut vertex) is defined as a vertex which, when removed along with associated edges, makes the graph disconnected (or more precisely, increases the number of connected components in the graph). The task is to find all articulation points in the given graph.

**Input:**
The input to the function/method consists of three arguments:

* `numNodes`, an integer representing the number of nodes in the graph.
* `numEdges`, an integer representing the number of edges in the graph.
* `edges`, the list of pair of integers - A, B representing an edge between the nodes A and B.

**Output:**
Return a list of integers representing the critical nodes.

**Example:**

```
Input: numNodes = 7, numEdges = 7, edges = [[0, 1], [0, 2], [1, 3], [2, 3], [2, 5], [5, 6], [3, 4]]
Output: [2, 3, 5]
```

**Code:**

```python
def getCriticalNodes(links, numLinks, numRouters):
    order = 0;
    graph = {}
    for i in range(numRouters):
        graph[i] = set()
    
    for i, j in links:
        graph[i].add(j)
        graph[j].add(i)

    ret = set()
    low = [0 for i in range(numRouters)]
    ids = [-1 for i in range(numRouters)]
    parent = [-1 for i in range(numRouters)]
    
    for i in range(numRouters):
        if ids[i] == -1:
            dfs(graph, low, ids, parent, i, ret, order)
    return ret

def dfs(graph, low, ids, parent, cur, ret, order):
    children = 0
    order += 1
    ids[cur] = order
    low[cur] = order
    for n in graph[cur]:
        if ids[n] == -1:
            children += 1
            parent[n] = cur
            dfs(graph, low, ids, parent, n, ret, order)
            low[cur] = min(low[cur], low[n])
            if parent[cur] == -1 and children > 1 or parent[cur] != -1 and low[n] >= ids[cur]:
                ret.add(cur)
        elif n != parent[cur]:
            low[cur] = min(low[cur], low[n])
```
keep check the order and the lowest reach order. 
