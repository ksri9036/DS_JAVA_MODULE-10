# Ex21 Count the Number of Nodes in the Left Subtree of a Binary Tree  

## DATE:  
16.11.2025  

## AIM:  
To design and implement a Java program that constructs a binary tree from given level order input and counts the number of nodes present in the left subtree of the root node.  

## Algorithm  
1. Start the program.  
2. Define a Node class to represent each node of the binary tree.  
3. Build the binary tree from a given level order array.  
4. Recursively count the number of nodes in the left subtree of the root.  
5. Display the total count.  
6. End the program.  

## Program:
```java
/*
Program to construct a binary tree from given level order input 
and count the number of nodes in the left subtree of the root node.
Developed by: Kishore B
RegisterNumber: 212224100032
Date: 10.11.2025
*/
import java.util.*;

class Node {
    int data;
    Node left, right;
    Node(int data) {
        this.data = data;
        left = right = null;
    }
}

public class LeftSubtreeCount {
    public static Node insertLevelOrder(int[] arr, int i) {
        if (i < arr.length) {
            Node root = new Node(arr[i]);
            root.left = insertLevelOrder(arr, 2 * i + 1);
            root.right = insertLevelOrder(arr, 2 * i + 2);
            return root;
        }
        return null;
    }

    public static int countNodes(Node root) {
        if (root == null)
            return 0;
        return 1 + countNodes(root.left) + countNodes(root.right);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of nodes: ");
        int n = sc.nextInt();
        int[] arr = new int[n];
        System.out.println("Enter level order elements:");
        for (int i = 0; i < n; i++)
            arr[i] = sc.nextInt();

        Node root = insertLevelOrder(arr, 0);
        int leftCount = countNodes(root.left);
        System.out.println("Number of nodes in left subtree: " + leftCount);
        sc.close();
    }
}
```
## OUTPUT
<img width="943" height="145" alt="image" src="https://github.com/user-attachments/assets/23941bb6-c485-4c81-8d38-c4a6bb003fa1" />

## RESULT
The program has been successfully implemented and executed.

# Ex22 Searching for a Book ID in a Binary Search Tree (BST)

## DATE:  
16.11.2025  

## AIM:  
To design and implement a Java program that constructs a Binary Search Tree (BST) using given Book IDs and checks whether a specific Book ID exists in the BST.  

## Algorithm  
1. Start the program.  
2. Define a `Node` class with data, left, and right references.  
3. Create an `insert()` function to insert nodes into the BST following BST rules.  
4. Create a `search()` function to find a Book ID in the BST.  
5. Build the BST using given Book IDs.  
6. Search for a specific Book ID entered by the user.  
7. Display whether the Book ID exists in the tree.  
8. End the program.  

## Program:
```java
/*
Program to construct a Binary Search Tree (BST) using given Book IDs 
and check whether a specific Book ID exists in the BST.
Developed by: Kishore B
RegisterNumber: 212224100032
Date: 10.11.2025
*/
import java.util.*;

class Node {
    int data;
    Node left, right;
    Node(int data) {
        this.data = data;
        left = right = null;
    }
}

public class BookSearchBST {
    public static Node insert(Node root, int data) {
        if (root == null)
            return new Node(data);
        if (data < root.data)
            root.left = insert(root.left, data);
        else if (data > root.data)
            root.right = insert(root.right, data);
        return root;
    }

    public static boolean search(Node root, int key) {
        if (root == null)
            return false;
        if (root.data == key)
            return true;
        if (key < root.data)
            return search(root.left, key);
        else
            return search(root.right, key);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Node root = null;
        System.out.print("Enter number of Book IDs: ");
        int n = sc.nextInt();
        System.out.println("Enter Book IDs:");
        for (int i = 0; i < n; i++) {
            int id = sc.nextInt();
            root = insert(root, id);
        }

        System.out.print("Enter Book ID to search: ");
        int key = sc.nextInt();

        if (search(root, key))
            System.out.println("Book ID found in the library system.");
        else
            System.out.println("Book ID not found in the library system.");
        sc.close();
    }
}
```
## OUTPUT
<img width="929" height="176" alt="image" src="https://github.com/user-attachments/assets/7cd8a6b3-e53f-4032-84fa-5f649262fb7c" />

## RESULT
The program has been successfully implemented and executed.

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
