# Lowest-Common-Ancestor-LCA-in-a-Binary-Tree-Binary-Search-Tree
PROJECT TITLE


Submitted by:                   Abdul Samad Islam,Attaullah
                                             
Student ID:                        4089,4868
Submitted to:                    MAM ARSHI 
Subject:                              DATA STRUCTURE
Semester:                          3 (Computer Science)
Section:                              BSCS (C)
#include <iostream>
using namespace std;

// Definition of Tree Node
struct Node {
    int data;
    Node* left;
    Node* right;
    
    Node(int val) {
        data = val;
        left = right = NULL;
    }
};

// Function to find LCA in a Binary Tree
Node* findLCA(Node* root, int n1, int n2) {
    if (root == NULL) return NULL;
    
    if (root->data == n1 || root->data == n2) return root;
    
    Node* leftLCA = findLCA(root->left, n1, n2);
    Node* rightLCA = findLCA(root->right, n1, n2);
    
    if (leftLCA && rightLCA) return root;
    
    return (leftLCA != NULL) ? leftLCA : rightLCA;
}

// Function to find LCA in a BST
Node* findLCA_BST(Node* root, int n1, int n2) {
    if (root == NULL) return NULL;
    
    if (root->data > n1 && root->data > n2) {
        return findLCA_BST(root->left, n1, n2);
    }
    
    if (root->data < n1 && root->data < n2) {
        return findLCA_BST(root->right, n1, n2);
    }
    
    return root;
}

// Function to insert a node into BST
Node* insert(Node* root, int key) {
    if (root == NULL) return new Node(key);
    if (key < root->data) root->left = insert(root->left, key);
    else root->right = insert(root->right, key);
    return root;
}

// Main function to test LCA functions
int main() {
    // Creating a Binary Search Tree (BST)
    Node* root = NULL;
    root = insert(root, 20);
    insert(root, 10);
    insert(root, 30);
    insert(root, 5);
    insert(root, 15);
    insert(root, 25);
    insert(root, 35);
    
    int n1 = 5, n2 = 15;
    Node* lcaBST = findLCA_BST(root, n1, n2);
    cout << "LCA of " << n1 << " and " << n2 << " in BST: " << lcaBST->data << endl;
    
    // Creating a Binary Tree
    Node* rootBT = new Node(1);
    rootBT->left = new Node(2);
    rootBT->right = new Node(3);
    rootBT->left->left = new Node(4);
    rootBT->left->right = new Node(5);
    rootBT->right->left = new Node(6);
    rootBT->right->right = new Node(7);
    
    n1 = 4, n2 = 5;
    Node* lcaBT = findLCA(rootBT, n1, n2);
    cout << "LCA of " << n1 << " and " << n2 << " in Binary Tree: " << lcaBT->data << endl;
