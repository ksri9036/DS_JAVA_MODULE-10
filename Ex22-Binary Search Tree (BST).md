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

