# Ex23 Breadth-First Search (BFS) Traversal of a City Junction Map

## DATE:
16.11.2025  

## AIM:
To design and implement a Java program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph, and find all reachable locations from a given source junction.

## Algorithm
1. Start the program.  
2. Read the number of junctions (vertices) and roads (edges).  
3. Build an adjacency list to represent the graph.  
4. Read the source junction.  
5. Use a queue and a visited array to perform BFS.  
6. Print the order of traversal showing all reachable junctions.  
7. Stop the program.  

## Program:
```java
/*
Program to perform Breadth-First Search (BFS) traversal on a city's junction map represented as a graph
Developed by: Kishore B
RegisterNumber: 212224100032
Date: 10.11.2025
*/

import java.util.*;

public class BFSJunctionMap {
    static void bfsTraversal(Map<Integer, List<Integer>> graph, int src, int n) {
        boolean[] visited = new boolean[n];
        Queue<Integer> queue = new LinkedList<>();

        visited[src] = true;
        queue.add(src);

        System.out.print("BFS Traversal (reachable junctions): ");
        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");

            for (int neighbor : graph.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of junctions (nodes): ");
        int n = sc.nextInt();

        System.out.print("Enter number of roads (edges): ");
        int e = sc.nextInt();

        Map<Integer, List<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++)
            graph.put(i, new ArrayList<>());

        System.out.println("Enter the roads (u v) with 0-based indices:");
        for (int i = 0; i < e; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u); // Undirected graph
        }

        System.out.print("Enter source junction (0-based): ");
        int src = sc.nextInt();

        bfsTraversal(graph, src, n);
        sc.close();
    }
}
```
## OUTPUT
<img width="936" height="387" alt="image" src="https://github.com/user-attachments/assets/20891545-c24e-42db-b9d4-d7a260325e6a" />

## RESULT
The Java program successfully performs BFS traversal on a city’s junction map and lists all reachable junctions from the given source node.
