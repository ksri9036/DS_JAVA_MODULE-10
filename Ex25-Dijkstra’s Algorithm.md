# Ex25 Finding the Fastest Route to a Charging Station using Dijkstra’s Algorithm

## DATE:
16.11.2025

## AIM:
To design and implement a Java program that helps an electric vehicle (EV) find the shortest travel time from its current block to the nearest charging station using Dijkstra’s shortest path algorithm.

## Algorithm
1. Read number of blocks (nodes) and roads (edges) with travel times (weights).  
2. Build a weighted adjacency list for the graph.  
3. Read the list of charging station nodes.  
4. Run Dijkstra’s algorithm from the EV’s current location to compute shortest distances to all nodes.  
5. Find the minimum distance among all charging stations.  
6. Output the fastest route travel time and the corresponding charging station.  

## Program:
```java
/*
Program to find the Fastest Route to a Charging Station using Dijkstra’s Algorithm
Developed by: Kishore B
RegisterNumber: 212224100032
Date: 10.11.2025
*/

import java.util.*;

class Edge {
    int to, weight;
    Edge(int to, int weight) { this.to = to; this.weight = weight; }
}

public class FastestChargingRoute {

    static int[] dijkstra(List<List<Edge>> graph, int src) {
        int n = graph.size();
        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;
        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[1]));
        pq.add(new int[]{src, 0});
        
        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int u = curr[0], d = curr[1];
            if (d > dist[u]) continue;
            for (Edge e : graph.get(u)) {
                if (dist[u] + e.weight < dist[e.to]) {
                    dist[e.to] = dist[u] + e.weight;
                    pq.add(new int[]{e.to, dist[e.to]});
                }
            }
        }
        return dist;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of blocks (nodes): ");
        int n = sc.nextInt();
        System.out.print("Enter number of roads (edges): ");
        int m = sc.nextInt();
        
        List<List<Edge>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());
        
        System.out.println("Enter roads as (u v travelTime) with 0-based indices:");
        for (int i = 0; i < m; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            int w = sc.nextInt();
            graph.get(u).add(new Edge(v, w));
            graph.get(v).add(new Edge(u, w));
        }

        System.out.print("Enter number of charging stations: ");
        int k = sc.nextInt();
        int[] stations = new int[k];
        System.out.println("Enter charging station nodes (0-based):");
        for (int i = 0; i < k; i++) stations[i] = sc.nextInt();

        System.out.print("Enter current block of EV (0-based): ");
        int start = sc.nextInt();

        int[] dist = dijkstra(graph, start);
        int minDist = Integer.MAX_VALUE;
        int nearestStation = -1;
        for (int station : stations) {
            if (dist[station] < minDist) {
                minDist = dist[station];
                nearestStation = station;
            }
        }

        if (nearestStation == -1 || minDist == Integer.MAX_VALUE)
            System.out.println("No reachable charging station.");
        else
            System.out.println("Nearest charging station: " + nearestStation + " with travel time: " + minDist);

        sc.close();
    }
}
```
## OUTPUT
<img width="940" height="478" alt="image" src="https://github.com/user-attachments/assets/74510562-ae75-426e-b93a-e8922918ada1" />

## RESULT
The program successfully computes the shortest travel time from the EV’s current block to the nearest charging station using Dijkstra’s algorithm and handles unreachable cases correctly.
