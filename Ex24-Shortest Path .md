# Ex24 Shortest Path and Reachability in a Heritage Town using BFS

## DATE:
16.11.2025

## AIM:
To design and implement a Java program that, given a map of attractions in a heritage town connected by walking paths, recommends:
- The shortest number of paths (minimum hops) from a starting attraction to a target attraction.
- The number of reachable attractions from the same starting point using Breadth-First Search (BFS).

## Algorithm
1. Read number of attractions (nodes) `n` and number of paths (edges) `m`.  
2. Build adjacency list for the undirected graph.  
3. Run BFS from the start node to compute distances and visited nodes.  
4. Shortest hops = distance[target] (use -1 or "unreachable" if not visited).  
5. Reachable count = number of visited nodes (excluding the start if you prefer).  
6. Print results.

## Program:
```java
import java.util.*;

public class HeritageTownBFS {
    static List<List<Integer>> buildGraph(int n, int[][] edges) {
        List<List<Integer>> g = new ArrayList<>();
        for (int i = 0; i < n; i++) g.add(new ArrayList<>());
        for (int[] e : edges) {
            int u = e[0], v = e[1];
            g.get(u).add(v);
            g.get(v).add(u);
        }
        return g;
    }

    static int[] bfsDistances(List<List<Integer>> g, int src) {
        int n = g.size();
        int[] dist = new int[n];
        Arrays.fill(dist, -1);
        Queue<Integer> q = new LinkedList<>();
        dist[src] = 0;
        q.add(src);
        while (!q.isEmpty()) {
            int u = q.poll();
            for (int v : g.get(u)) {
                if (dist[v] == -1) {
                    dist[v] = dist[u] + 1;
                    q.add(v);
                }
            }
        }
        return dist;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of attractions (n): ");
        int n = sc.nextInt();
        System.out.print("Enter number of paths (m): ");
        int m = sc.nextInt();

        System.out.println("Enter edges (u v) using 0-based indices, one per line:");
        int[][] edges = new int[m][2];
        for (int i = 0; i < m; i++) {
            edges[i][0] = sc.nextInt();
            edges[i][1] = sc.nextInt();
        }

        List<List<Integer>> graph = buildGraph(n, edges);

        System.out.print("Enter start attraction (0-based): ");
        int start = sc.nextInt();
        System.out.print("Enter target attraction (0-based): ");
        int target = sc.nextInt();

        int[] dist = bfsDistances(graph, start);

        int reachableCount = 0;
        for (int d : dist) if (d != -1) reachableCount++;

        System.out.println();
        if (dist[target] == -1)
            System.out.println("Target is unreachable from start.");
        else
            System.out.println("Shortest number of paths (minimum hops) from " + start + " to " + target + ": " + dist[target]);

        System.out.println("Number of reachable attractions from " + start + ": " + reachableCount);
        sc.close();
    }
}
```
## OUTPUT
<img width="934" height="512" alt="image" src="https://github.com/user-attachments/assets/13a4298b-153f-4fef-91b5-fe98830de223" />

## RESULT
The program correctly computes the shortest number of paths (minimum hops) between two attractions and the total number of reachable attractions from a given starting point using BFS traversal.
