**GRAPHS** is a data structure consisting of a set of vertices (or nodes) and a set of edges that connect these vertices.  Edges may be directed (representing a one-way relationship) or undirected (representing a two-way relationship), and they can have weights assigned to them to represent costs or distances.  Graphs are used to model various real-world scenarios, such as social networks, road maps, and dependencies between tasks, enabling the analysis of connections and relationships. This C++ code implements Dijkstra's algorithm to find the shortest paths from a single source vertex to all other vertices in an undirected graph.

**1. Includes and Namespace:**

```c++
#include <iostream>
#include <vector>
#include <queue>
#include <climits> // For INT_MAX

using namespace std;
```

*   `#include <iostream>`: For input/output operations (like `cout`).
*   `#include <vector>`: For using `std::vector` to represent the adjacency list of the graph and store distances.
*   `#include <queue>`: For using `std::priority_queue` to implement Dijkstra's algorithm efficiently.
*   `#include <climits>`: For using `INT_MAX` to represent infinity (an initially infinite distance).
*   `using namespace std;`: To avoid writing `std::` before standard library elements.

**2. `Edge` Structure:**

```c++
struct Edge {
    int to;
    int weight;
};
```

*   Defines a structure `Edge` to represent an edge in the graph. Each edge has:
    *   `to`: The destination vertex of the edge.
    *   `weight`: The weight (cost) of the edge.

**3. `addEdge()` Function:**

```c++
void addEdge(vector<vector<Edge>>& adj, int u, int v, int w) {
    adj[u].push_back({v, w});
    adj[v].push_back({u, w}); // For undirected graph
}
```

*   This function adds an undirected edge between vertices `u` and `v` with weight `w` to the adjacency list `adj`.  Because the graph is undirected, the edge is added to both `adj[u]` (u to v) and `adj[v]` (v to u).

**4. `dijkstra()` Function:**

```c++
vector<int> dijkstra(const vector<vector<Edge>>& adj, int start) {
    int n = adj.size();
    vector<int> dist(n, INT_MAX); // Initialize distances to infinity
    dist[start] = 0;

    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    pq.push({0, start}); // {distance, vertex}

    while (!pq.empty()) {
        int u = pq.top().second;
        int d = pq.top().first;
        pq.pop();

        if (d > dist[u]) continue; // Optimization: Skip if we have a better path already

        for (const Edge& edge : adj[u]) {
            int v = edge.to;
            int weight = edge.weight;

            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }
    return dist;
}
```

*   This function implements Dijkstra's algorithm.
*   `n`: Number of vertices in the graph.
*   `dist`: A vector to store the shortest distances from the `start` vertex to all other vertices. Initialized to `INT_MAX` (infinity).
*   `pq`: A priority queue (min-heap) to store vertices and their current shortest distances from the source. The priority queue is ordered by distance.
*   The `while` loop continues as long as the priority queue is not empty.
*   Inside the loop:
    *   `u`: The vertex with the smallest distance from the source that has not yet been visited.
    *   `d`: The distance from the source to `u`.
    *   The `if (d > dist[u]) continue;` line is an optimization.  If we've already found a shorter path to `u`, we can skip processing it.
    *   The inner loop iterates through all the neighbors `v` of `u`.
    *   If a shorter path to `v` is found (`dist[u] + weight < dist[v]`), the distance to `v` is updated, and `v` is added to the priority queue.
*   Returns the `dist` vector containing the shortest path distances.

**5. `main()` Function:**

```c++
int main() {
    int numVertices = 6;
    vector<vector<Edge>> adj(numVertices);

    // Build the graph (example)
    addEdge(adj, 0, 1, 4);
    addEdge(adj, 0, 2, 2);
    addEdge(adj, 1, 2, 1);
    addEdge(adj, 1, 3, 5);
    addEdge(adj, 2, 3, 8);
    addEdge(adj, 2, 4, 10);
    addEdge(adj, 3, 4, 6);
    addEdge(adj, 3, 5, 5);
    addEdge(adj, 4, 5, 4);

    int startVertex = 0;
    vector<int> shortestPaths = dijkstra(adj, startVertex);

    cout << "Shortest paths from vertex " << startVertex << ":" << endl;
    for (int i = 0; i < numVertices; ++i) {
        cout << "To vertex " << i << ": ";
        if (shortestPaths[i] == INT_MAX) {
            cout << "Infinity" << endl;
        } else {
            cout << shortestPaths[i] << endl;
        }
    }

    return 0;
}
```

*   `numVertices`: The number of vertices in the graph.
*   `adj`: The adjacency list representing the graph. `adj[u]` contains a list of edges going from vertex `u`.
*   The `addEdge()` function is used to add the edges to the graph.
*   `startVertex`: The source vertex.
*   `shortestPaths`: Stores the result of Dijkstra's algorithm.
*   The code then prints the shortest paths from the `startVertex` to all other vertices.

**Graph (Visual Representation):**

```
      0
     / \
    4   2
   / \   \
  1---2   4
     / \ / \
    5   8 6 5
       \ /
        5
```

**Output:**

```
Shortest paths from vertex 0:
To vertex 0: 0
To vertex 1: 3
To vertex 2: 2
To vertex 3: 8
To vertex 4: 12
To vertex 5: 13
```

**Explanation of the Output:**

The output shows the shortest distances from vertex 0 to all other vertices. For example, the shortest path from vertex 0 to vertex 1 is 3 (0 -> 2 -> 1), the shortest path from vertex 0 to vertex 3 is 8 (0 -> 2 -> 1 -> 3), and so on.
