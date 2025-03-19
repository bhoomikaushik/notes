# SRE TRAINING (DAY 24) - REACT VS ANGULAR & PYTHON DATA STRUCTURES
## By bhoomikaushik

## Comparing React and Angular

| Feature         | React  | Angular  |
|---------------|--------|---------|
| Type         | Library | Framework |
| Language     | JavaScript (JSX) | TypeScript |
| Architecture | Component-based | MVC-based |
| Data Binding | One-way binding | Two-way binding |
| Performance  | Faster due to Virtual DOM | Slower due to real DOM manipulation |
| Learning Curve | Easier to learn | Steeper learning curve |
| Use Case     | Best for SPAs and lightweight applications | Best for large-scale enterprise apps |

---

## Understanding MVC Architecture
MVC (Model-View-Controller) is a design pattern used for organizing application structure:

- **Model**: Manages data and business logic
- **View**: Handles the visual representation to users
- **Controller**: Processes user input and updates the model

This separation enhances code maintainability and scalability.

---

## Data Binding Explained
Data binding connects UI elements with application data sources for synchronization:

1. **One-way binding**: Data flows in a single direction (React's approach)
2. **Two-way binding**: Data updates bidirectionally (Angular's approach)

---

# Python Data Structures Overview

## Stack Data Structure
A stack implements the **LIFO (Last In, First Out)** principle. Key operations:

- **Push**: Add element to top
- **Pop**: Remove top element
- **Peek**: View top element without removal
- **isEmpty**: Check if stack contains elements
- **Size**: Get element count

### Python Stack Implementation:
```python
class Stack:
    def __init__(self):
        self.items = []

    def is_empty(self):
        return len(self.items) == 0

    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop() if not self.is_empty() else None

    def peek(self):
        return self.items[-1] if not self.is_empty() else None

    def size(self):
        return len(self.items)

# Example usage
stack = Stack()
stack.push(10)
stack.push(20)
print(stack.pop())  # Output: 20
```

## Queue Data Structure
A queue follows the **FIFO (First In, First Out)** principle. Primary operations:

- **Enqueue**: Add element to end
- **Dequeue**: Remove element from front
- **Front**: View first element

## Linked List Data Structure
A linked list consists of nodes containing data and references to other nodes:

- **Singly Linked List**: Each node points to next node
- **Doubly Linked List**: Nodes have references to both previous and next nodes

---

# Tree Data Structures
Trees are hierarchical structures with connected nodes:

- **Root**: Top-level node
- **Node**: Individual element
- **Branch**: Connection between nodes
- **Leaf**: Node without children

### Common Tree Traversal Methods:
1. **Inorder Traversal (Left-Root-Right)**
2. **Preorder Traversal (Root-Left-Right)**
3. **Postorder Traversal (Left-Right-Root)**
4. **Level Order Traversal**

### Binary Search Tree (BST)
A BST is a specialized tree where each node has at most two children, with left < root < right.

#### Visual Representation of a BST
```
        50
       /  \
     30    70
    /  \   /  \
   20  40 60  80
```

### BST Implementation in Python:
```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

    def insert(self, value):
        if value < self.value:
            if self.left:
                self.left.insert(value)
            else:
                self.left = TreeNode(value)
        else:
            if self.right:
                self.right.insert(value)
            else:
                self.right = TreeNode(value)

    def inorder_traversal(self):
        if self.left:
            self.left.inorder_traversal()
        print(self.value, end=" ")
        if self.right:
            self.right.inorder_traversal()

# Example usage
root = TreeNode(50)
root.insert(30)
root.insert(70)
root.inorder_traversal()  # Output: 30 50 70
```

## Trie Data Structure
A Trie is a tree-like structure optimized for storing strings efficiently:

- **Each node represents a character**
- **Words are stored as paths from the root**

#### Visual Representation of a Trie (for 'hello' and 'hey')
```
        (root)
       /  |  \
      h   a   b
     /       \
    e         e
   / \        \
  l   y        l
 /             \
 l              o
/                
o                
```

### Trie Implementation in Python:
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True

    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end_of_word

# Example output
trie = Trie()
trie.insert("hello")
print(trie.search("hello"))  # Output: True
print(trie.search("hell"))   # Output: False
```
