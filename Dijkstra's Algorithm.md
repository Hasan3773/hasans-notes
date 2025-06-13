Dijkstra's Algorithm: An algorithm to find the shortest path from a node to all other nodes in a **weighted graph**, use bfs if unweighted. 
- Initialize distances - set the source node distance to 0 and all other nodes to inf
- Use a priority queue / min-heap to extract the node with the smallest "tentative dist"
- After you extract the node, update all the neighbors (calculate new dist) if the new dist is smaller than "stored" update the value?
- repeat until all nodes are processed

```
function Dijkstra(graph, source):
    # Step 1: Initialization
    dist[source] = 0                  # Distance to source is 0
    for each vertex v in graph:
        if v ≠ source:
            dist[v] = ∞                # Set all other distances to infinity
        prev[v] = NULL                 # Previous node in optimal path
        unvisited.add(v)               # Add all nodes to the unvisited set
    
    # Step 2: Process nodes
    while unvisited is not empty:
        # Select node with minimum distance
        u = node in unvisited with min dist[u]
        unvisited.remove(u)
        
        for each neighbor v of u:
            alt = dist[u] + weight(u, v)  # Calculate new potential distance
            if alt < dist[v]:             # If shorter path found
                dist[v] = alt              # Update distance
                prev[v] = u                # Store previous node

    return dist, prev   # Shortest path distances and previous nodes
```

There are ‘n’ cities connected by m flights. Each flight starts from the city ‘u’ and arrives at ‘v’ at a price ‘w.’ Now, given all the cities and flights, and the starting city ‘src,’ and the destination ‘dst,’ find the lowest price from ‘src’ to ‘dst’ with up to ‘k’ stops. If no such route exists, the output is -1.

Essentially you're given a bunch of possible flights and then a starting city and a end city with the max number of layover. You must analyze the flights to find the cheapest way from city a to city b.

Dijkstra's Algorithm with BFS: 
- Adjacency List (unordered map with int, vector<int,int>) // start city, end city, cost 
- Time Complexity O((N+M)logM) where N = Cities & M = Flights



