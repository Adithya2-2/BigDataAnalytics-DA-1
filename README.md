BIG DATA ANALYTICS DA-1



Problem statement:
Single Source Shortest Path Calculation Using Dijkstra's Algorithm on a Distributed System

Objective:
The goal of this project is to implement a distributed version of Dijkstra's algorithm to compute the single-source shortest path (SSSP) in a large graph using the Hadoop MapReduce framework. This algorithm will efficiently calculate the shortest path from a given source node to all other nodes in the graph.

Inputs:
Graph Dataset: A text file representing a directed graph, where each line contains two integers indicating an edge between two nodes (from-node to-node). The graph is represented as an adjacency list.
Source Node: The node from which the shortest paths will be calculated.

Outputs:
Shortest Path Distance: The shortest distance from the source node to each other node in the graph.
Path Statistics: Additional statistics regarding the shortest paths, such as the distribution of path lengths.

Approach:
Adjacency List Creation:
   - Mapper: For each input line (edge), output a key-value pair where the key is the starting node, and the value is the ending node.
   - Reducer: Aggregate all the nodes that a particular node points to, forming the adjacency list for each node.

Shortest Path Calculation:
   - Mapper: For each node, propagate the shortest known distance to its neighbors. If a shorter path to a neighbor is found, update the distance.
   - Reducer: Aggregate the distances from all paths leading to a node, selecting the minimum distance for each node.

Iteration:
   - The MapReduce job iteratively runs until no shorter paths are found in the graph. This ensures that the shortest path to each node from the source node is discovered.

Convergence Check:
   - After each iteration, the algorithm checks whether the shortest paths have converged (i.e., no distances are updated). If they have, the process stops; otherwise, it continues with the updated paths.

Final Statistics Calculation:
   - Mapper: Extract the distance values from the final output and count the occurrences of each distance.
   - Reducer: Aggregate these counts to produce statistics on the distribution of shortest path lengths.

Key Components:
- AdjacencyListMap & Reduce: Constructs the adjacency list of the graph, which is the first step in setting up the input for the shortest path calculation.
- TheMapper & TheReducer: Core components of the Dijkstra algorithm that propagate and reduce the shortest path distances across the graph.
- DijkstraStatisticsMap & Reduce: Collect and summarize statistics on the shortest path distances.

