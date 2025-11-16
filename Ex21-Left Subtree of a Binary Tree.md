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
