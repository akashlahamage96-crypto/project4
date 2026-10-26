# project4
Binary Search Tree:
//Assignment 4
Implement binary search tree and perform following operations:
a) Insert (Handle insertion of duplicate entry)
b) Delete
c) Search
d) Display tree (Traversal)
e) Display - Depth of tree
f) Display - Mirror image
g) Create a copy
h) Display all parent nodes with their child nodes
i) Display leaf nodes
j) Display tree level wise
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
class BST:
    def __init__(self):
        self.root = None
    # Insert (Duplicate not allowed)
    def insert(self, root, key):
        if root is None:
            return Node(key)
        if key < root.data:
            root.left = self.insert(root.left, key)
        elif key > root.data:
            root.right = self.insert(root.right, key)
        else:
            print("Duplicate Entry Not Allowed :", key)
        return root
    # Search
    def search(self, root, key):
        if root is None:
            return False
        if root.data == key:
            return True
        if key < root.data:
            return self.search(root.left, key)
        return self.search(root.right, key)
    # Find minimum value node
    def minValue(self, root):
        while root.left:
            root = root.left
        return root
    # Delete
    def delete(self, root, key):
        if root is None:
            return root
        if key < root.data:
            root.left = self.delete(root.left, key)
        elif key > root.data:
            root.right = self.delete(root.right, key)
        else:
            if root.left is None:
                return root.right
            if root.right is None:
                return root.left
            temp = self.minValue(root.right)
            root.data = temp.data
            root.right = self.delete(root.right, temp.data)
        return root
    # Inorder Traversal
    def inorder(self, root):
        if root:
            self.inorder(root.left)
            print(root.data, end=" ")
            self.inorder(root.right)
    # Depth of Tree
    def depth(self, root):
        if root is None:
            return 0
        return 1 + max(self.depth(root.left),
                       self.depth(root.right))
    # Mirror Image
    def mirror(self, root):
        if root:
            root.left, root.right = root.right, root.left
            self.mirror(root.left)
            self.mirror(root.right)
    # Copy Tree
    def copyTree(self, root):
        if root is None:
            return None
        newNode = Node(root.data)
        newNode.left = self.copyTree(root.left)
        newNode.right = self.copyTree(root.right)
        return newNode
    # Parent with Child Nodes
    def parentChild(self, root):
        if root:
            if root.left or root.right:
                print("Parent:", root.data, end=" -> ")
                if root.left:
                    print("Left:", root.left.data, end=" ")
                if root.right:
                    print("Right:", root.right.data, end=" ")
                print()
            self.parentChild(root.left)
            self.parentChild(root.right)
    # Leaf Nodes
    def leafNodes(self, root):
        if root:
            if root.left is None and root.right is None:
                print(root.data, end=" ")
            self.leafNodes(root.left)
            self.leafNodes(root.right)
    # Level Wise Display
    def levelWise(self):
        if self.root is None:
            return
        q = [self.root]
        while q:
            node = q.pop(0)
            print(node.data, end=" ")
            if node.left:
               q.append(node.left)
            if node.right:
                q.append(node.right)
                q.append(node.left)
            if node.right:
                q.append(node.right
