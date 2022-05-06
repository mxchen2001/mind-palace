# Bridge Finding Algorithms

There was a recent question on the Algorithms Test that one of my friends helped write. The question was how to find a bridge — an edge in a graph that connects two components such that if the edge is removed, the graph becomes disconnected. Off the top of my head, I came up with a non-optimal solution. I will assume `DFS` and `BFS` are available to use.

```py
def findBridge(graph):
    edges = getEdges(graph)

    bridges = []
    visited = set()

    for edge in edges:
        if edge not in visited
            visited.add(edge)
            subgraph = removeEdge(graph, edge)

            tree = dfs(subgraph, edge)

            if getNodeCount(tree) != getNodeCount(graph):
                bridges.append(edge)

    return bridges
```

However, this solution is not optimal. There exist a linear time algorithm, Tarjan's Algorithm, that can find all bridges in O(V + E) time.

The algorithm involve 2 key factors: 
1) Saving the level.
2) Keeping track of the lowest reachable node. 


The idea is that as we traverse the graph in a DFS manner, we will keep track of the nodes level where the level is increasing from root to leaves and unique. At the same time, we need to keep track of a the lowest reachable level with consideration of backedges.

```py
class Node:
    def __init__(self, value):
        self.value = value
        self.lowest_reachable = -1
        self.level = -1
        self.adjacent = []

def tarjanDFS(current, visited):
    for node in current.adjacent:
        if node not in visited:
            tarjanDFS(node, visited)
            node.lowest_reachable = min(node.lowest_reachable, node.lowest_reachable)
        else:
            node.lowest_reachable = min(node.lowest_reachable, node.level)



def tarjan(graph):


```