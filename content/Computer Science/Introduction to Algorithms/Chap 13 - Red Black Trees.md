# Red-Black Trees
### Properties of red-black tree
A red-black tree is a binary search tree with one extra bit of storage per node. Its color, which can be either `RED` or `BLACK`. By constraining the node colors on any simple path from the root to a leaf, red-black trees ensure that no such path is more than twice as long as any other, so that the tree is approximately balanced.
Each node of the red-black tree contains *color, key, left, right* and *p* .

A red-black tree is a binary search tree that satisfies the following *red-black properties*:
1. Every node is either red or black
2. The root is black
3. Every leaf is back.
4. If a node is red then both its children are black
5. For each node, all simple paths from the node to descendant leaves contain the same number of black nodes.

We call the number of black nodes on any simple path from, but not including, a node x down to a leaf the **black-height** of the node, denoted $bh(x)$.
The black-height of a red-black tree is the black-height of its root.

>[!Tip]
>Kindly watch this really cool playlist of red-black tree on YT about [Red-Black Tree](https://www.youtube.com/watch?v=qvZGUFHWChY&list=PL9xmBV_5YoZNqDI8qfOZgzbqahCUmUEin&pp=iAQB)

___
### Rotations
The search-tree operations such as `TREE-INSERT`, `TREE-DELETE` also works on RB trees but they modify the tree, which can violate the red-black properties.
To restore these properties, colors and pointer within nodes needs to to changed, For this purpose we use a local operation called **rotation** in a search tree that preserves that binary-search-tree property .

##### Kinds of rotation
- Left rotation - 
	A **left rotation** takes a node and moves it down to the left while shifting its right child up to become the parent of the original node.

- Right rotation -
	A **right rotation** is the mirror image of a left rotation. It takes a node and moves it down to the right while shifting its left child up to become the parent of the original node.

>[!tldr] $\text{LEFT-ROTATE}$
>$y = x.right$  
>$x.right = y.left \qquad\qquad$ // turn y’s left subtree into x’s right subtree   
> if $y.left \neq T.nil\qquad\qquad$ // if y’s left subtree is not empty . . .   
> $\qquad y.left.p = x\qquad\qquad$ // . . . then x becomes the parent of the subtree’s root   
> $y.p = x.p\qquad\qquad\qquad\quad$ // x’s parent becomes y’s parent   
> if $x.p == T.nil\qquad\qquad$ // if $x$ was the root . . .   
> $\qquad T.root = y\qquad\qquad\qquad$ // . . . then y becomes the root   
> elseif $x == x.p.left\qquad\qquad$ // otherwise, if x was a left child . . .   
> $\qquad x.p.left = y\qquad\qquad\qquad\quad\space$ // . . . then y becomes a left child   
> else $x.p.right = y\qquad\qquad\quad$ // otherwise, x was a right child, and now y is   
> $y.left = x\qquad\qquad\qquad\qquad$ // make x become y’s left child   
> $x.p = y$  

>[!tldr] $\text{RIGHT-ROTATE}$ 
>$x = y.left$  
>$y.left = x.right \qquad\qquad$ // turn x’s right subtree into y’s left subtree  
>if $x.right \neq T.nil\qquad\qquad$ // if x’s right subtree is not empty . . .   
>$\qquad x.right.p = y\qquad\qquad$ // . . . then y becomes the parent of the subtree’s root  
>$x.p = y.p\qquad\qquad\qquad\quad$ // y’s parent becomes x’s parent  
>if $y.p == T.nil\qquad\qquad$ // if $y$ was the root . . .   
>$\qquad T.root = x\qquad\qquad\qquad$ // . . . then x becomes the root   
>elseif $y == y.p.right\qquad\qquad$ // otherwise, if y was a right child . . .   
>$\qquad y.p.right = x\qquad\qquad\qquad\quad\space$ // . . . then x becomes a right child  
>else $y.p.left = x\qquad\qquad\quad$ // otherwise, y was a left child, and now x is  
>$x.right = y\qquad\qquad\qquad\qquad$ // make y become x’s right child  
>$y.p = x$  
### Insertion
In order to insert a node into a red-black tree with n internal nodes in $O(\lg n)$ time and maintain the red-black properties, we’ll need to slightly modify the TREEI NSERT procedure. The procedure `RB-INSERT` starts by inserting node into the tree $T$ as if it were an ordinary binary search tree, and then it colors $z$ red.
To guarantee that the red-black properties are preserved, an auxiliary procedure `RB-INSERT-FIXUP` on the facing page recolors nodes and performs rotations. The call `RB-INSERT(T, z)` inserts node $z$, whose key is assumed to have already been filled in, into the red-black tree $T$.

>[!tldr] $\text{RB-INSERT}$
>$x = T.root$  
>$y= T.nil$   
>while $x\neq T.nil$  
>$\qquad y = x$  
>$\qquad$ if $z.key < x.key$  
>$\qquad\qquad x = x.left$  
>$\qquad x = x.right$  
>$z.p = y$  
>if $y == T.nil$  
>$\qquad T.root = z$   
>else if $z.key < y.key$  
>$y.left = z$  
>else $y.right = z$  
>$z.left = T.nil$  
>$z.right = T.nil$  
>$z.color = RED$  
>$\text{RB-INSERT-FIXUP}(T, z)$  

>[!tldr] $\text{RB-INSERT-FIXUP}$
>while $z.p.color == RED$  
>$\qquad$ if $z.p == z.p.p.left$  
>$\qquad\qquad y= z.p.p.right$  
>$\qquad\qquad$if $y.color == RED$
>$\qquad\qquad\qquad z.p.color = BLACK$
>$\qquad\qquad\qquad z.color = BLACK$  
>$\qquad\qquad\qquad z.p.p.color = RED$  
>$\qquad\qquad\qquad z= z.p.p$  
>$\qquad\qquad$else  
>$\qquad\qquad\qquad$ if $z == z.p.right$  
>$\qquad\qquad\qquad\qquad z = z.p$  
>$\qquad\qquad\qquad\qquad \text{LEFT-ROTATE}(T, z)$  
>$\qquad\qquad\qquad z.p.color = \text{BLACK}$  
>$\qquad\qquad\qquad z.p.p.color = \text{RED}$  
>$\qquad\qquad\qquad$ $\text{RIGHT-ROTATE}(T, z, p.p)$  
>$\qquad$else   
>$\qquad\qquad y = z.p.p.left$  
>$\qquad\qquad$ if $y.color == \text{RED}$
>$\qquad\qquad\qquad z.p.color = \text{BLACK}$  
>$\qquad\qquad\qquad y.color = \text{BLACK}$   
>$\qquad\qquad\qquad z.p.p.color = \text{RED}$  
>$\qquad\qquad\qquad z = z.p.p$  
>$\qquad\qquad$else  
>$\qquad\qquad\qquad$ if $z == z.p.left$  
>$\qquad\qquad\qquad\qquad z = z.p$  
>$\qquad\qquad\qquad\qquad \text{RIGHT-ROTATE}(T,z)$  
>$\qquad\qquad\qquad z.p.color = \text{BLACK}$  
>$\qquad\qquad\qquad z.p.p.color = \text{RED}$  
>$\qquad\qquad\qquad \text{LEFT-ROTATE}(T, z.p.p)$  
>$T.root.color = \text{BLACK}$  
### Deletions
Deletion of a node takes $O(\text{log } n)$ time . Deleting a node from a red-black tree is more complicated than inserting a node, because it needs to maintain the tree's balance and the properties of the red-black tree after removing a node. 
##### Steps : 
- Find the node to delete
- Remove the node, then either 
	- Replace it with its successor, if necessary
	- Or fix any violations of the red-black properties.
- If the node being deleted is black, the tree might violate the property that all paths from any node to its leaves must contain the same number of black nodes. In such cases, a **fix-up operation** is needed to restore the properties of the red-black tree.

##### Deletion cases :
 To handle the violation caused by deleting a black node, the tree undergoes **case-by-case adjustments**. Let's assume `x` is the node that replaces the deleted node, and `w` is `x`'s sibling:
###### 1. Case 1: `x`'s sibling `w` is red
- If `x`'s sibling `w` is **red**, this means the parent of `x` must be black. To fix this, we perform a rotation:
    - **Recolor** `w` as black and `x`'s parent as red.
    - **Left-rotate** (if `w` is the right sibling of `x`) or right-rotate the tree (if `w` is the left sibling).
    - After the rotation, `w` becomes black, and the red-black tree properties are restored.
###### 2. Case 2: `w` is black, and both of `w`'s children are black
- If both of `w`'s children are **black**, the tree can temporarily "borrow" a black node by **recoloring**:
    - **Recolor** `w` as red, making `x`'s parent the new black node to "compensate" for the missing black node.
    - Then move `x` up the tree to the parent and repeat the process. This can propagate the violation upward, so it may require further fixing.

###### 3. Case 3: `w` is black, and `w`'s left child is red, and `w`'s right child is black
- In this case, perform a **right-rotation** (if `w` is the right sibling of `x`).
    - This rotation will bring the red child up and make `w`'s right child the new black node.
    - After that, recolor `w` and its left child to maintain the red-black properties.

###### 4. Case 4: `w` is black, and `w`'s right child is red
- If `w`'s right child is **red**, perform a **left-rotation** at the parent of `x`.
    - Then, recolor `w`'s right child as black and the parent as red.
    - This balances the black nodes and fixes the violation.

>[!tldr] $\text{RB-TRANSPLANT}(T, u, v)$
>if $u.p == T.nil$  
>$\qquad T.root = v$  
>elseif $u == u.p.left$   
>$\qquad u.p.left = v$  
>else $u.p.right = v$  
>$v.p= u.p$  

>[!tldr] $\text{RB-DELETE}(T, z)$
>$y = z$  
>$y.original-color = y.color$  
>if $z.left == T.nil$  
>$x = z.right$  
>$\text{RB-TRANSPLANT}(T, z, z.right)$  
>elseif $z.right == T.nil$  
>$\qquad x= z.left$  
>$\qquad\text{RB-TRANSPLANT}(T, z, z.left)$  
>else $y = \text{TREE-MINIMUM}(z.right)$  
>$\qquad y.original-color = y.co\lor$  
>$\qquad x = y.right$  
>$\qquad$ if $y \neq z.right$  
>$\qquad\qquad \text{RB-TRANSPLANT}(T, y,y.right)$  
>$\qquad\qquad y.right = z.right$  
>$\qquad$ else $x.p = y$  
>$\text{RB-TRANSPLANT}(T, z,y)$  
>$\qquad y.left = z.left$  
>$\qquad y.left.p = y$  
>$\qquad y.color = z.color$  
>if $y-original-color == \text{BLACK}$  
>$\qquad \text{RB-DELETE-FIXUP}(T, x)$   

>[!tldr] $\text{RB-DELETE-FIXUP}(T, x)$
>while $x \neq T.root$ and $x.color == \text{BLACK}$  
>$\qquad$ if $x == x.p.left$  
>$\qquad\qquad w = x.p.right$  
>$\qquad\qquad$if $w.color == \text{RED}$  
>$\qquad\qquad\qquad w.color = \text{BLACK}$   
>$\qquad\qquad\qquad \text{LEFT-ROTATE}(T, x.p)$  
>$\qquad\qquad\qquad w=x.p.right$  
>$\qquad\qquad$ if $w.left.color == \text{BLACK}$ and $w.right.color == \text{BLACK}$  
>$\qquad\qquad\qquad w.color = \text{RED}$  
>$\qquad\qquad\qquad x = x.p$  
>$\qquad\qquad$else  
>$\qquad\qquad\qquad$ if $w.right.color == \text{BLACK}$  
>$\qquad\qquad\qquad\qquad w.left.color = \text{BLACK}$  
>$\qquad\qquad\qquad\qquad \text{RIGHT-ROTATE}(T,w)$  
>$\qquad\qquad\qquad\qquad w = x.p.right$  
>$\qquad\qquad\qquad w.co\lor = x.p.color$  
>$\qquad\qquad\qquad x.p.color = \text{BLACK}$  
>$\qquad\qquad\qquad w.right.color = \text{BLACK}$  
>$\qquad\qquad\qquad \text{LEFT-ROTATE}(T,X.P)$  
>$\qquad\qquad\qquad x = T.root$  
>
>$\qquad$else  
>$\qquad\qquad$ $w= x.p.left$  
>$\qquad\qquad$ if $w.color == \text{RED}$  
>$\qquad\qquad\qquad w.color = \text{BLACK}$  
>$\qquad\qquad\qquad x.p.color=\text{RED}$  
>$\qquad\qquad\qquad\text{RIGHT-ROTATE}(T, x.p)$  
>$\qquad\qquad\qquad w = x.p.left$  
>$\qquad\qquad$if $w.right.color == \text{BLACK}$ and $w.left.color == \text{BLACK}$  
>$\qquad\qquad\qquad w.co\lor = \text{RED}$  
>$\qquad\qquad\qquad x = x.p$  
>$\qquad\qquad$ else  
>$\qquad\qquad\qquad$if $w.left.color == \text{BLACK}$  
>$\qquad\qquad\qquad\qquad w.right.color = BLACK$  
>$\qquad\qquad\qquad\qquad w.color = RED$  
>$\qquad\qquad\qquad\qquad \text{LEFT-ROTATE}(T,w)$  
>$\qquad\qquad\qquad\qquad w=x.p.left$  
>$\qquad\qquad\qquad w.color = x.p.color$  
>$\qquad\qquad\qquad x.p.color = BLACK$  
>$\qquad\qquad\qquad w.left.color = BLACK$  
>$\qquad\qquad\qquad \text{RIGHT-ROTATE}(T,x.p)$  
>$\qquad\qquad\qquad x=T.root$  
>$x.color = \text{BLACK}$  

The total cost of `RB-DELETE` without the call to `RB-DELETE-FIXUP` takes $O(\lg n)$ time. The procedure `RB-DELETE-FIXUP` takes $O(\lg n)$ times. The overall time for `RB-DELETE` is therefore also $O(\lg n)$.

#### Complete implementation

```cpp
#include <iostream>
using namespace std;

struct Node {
  int data;
  Node *parent;
  Node *left;
  Node *right;
  int color;
};

typedef Node *NodePtr;

class RedBlackTree {
   private:
  NodePtr root;
  NodePtr TNULL;

  void initializeNULLNode(NodePtr node, NodePtr parent) {
    node->data = 0;
    node->parent = parent;
    node->left = nullptr;
    node->right = nullptr;
    node->color = 0;
  }

  // Preorder
  void preOrderHelper(NodePtr node) {
    if (node != TNULL) {
      cout << node->data << " ";
      preOrderHelper(node->left);
      preOrderHelper(node->right);
    }
  }

  // Inorder
  void inOrderHelper(NodePtr node) {
    if (node != TNULL) {
      inOrderHelper(node->left);
      cout << node->data << " ";
      inOrderHelper(node->right);
    }
  }

  // Post order
  void postOrderHelper(NodePtr node) {
    if (node != TNULL) {
      postOrderHelper(node->left);
      postOrderHelper(node->right);
      cout << node->data << " ";
    }
  }

  NodePtr searchTreeHelper(NodePtr node, int key) {
    if (node == TNULL || key == node->data) {
      return node;
    }

    if (key < node->data) {
      return searchTreeHelper(node->left, key);
    }
    return searchTreeHelper(node->right, key);
  }

  // For balancing the tree after deletion
  void deleteFix(NodePtr x) {
    NodePtr s;
    while (x != root && x->color == 0) {
      if (x == x->parent->left) {
        s = x->parent->right;
        if (s->color == 1) {
          s->color = 0;
          x->parent->color = 1;
          leftRotate(x->parent);
          s = x->parent->right;
        }

        if (s->left->color == 0 && s->right->color == 0) {
          s->color = 1;
          x = x->parent;
        } else {
          if (s->right->color == 0) {
            s->left->color = 0;
            s->color = 1;
            rightRotate(s);
            s = x->parent->right;
          }

          s->color = x->parent->color;
          x->parent->color = 0;
          s->right->color = 0;
          leftRotate(x->parent);
          x = root;
        }
      } else {
        s = x->parent->left;
        if (s->color == 1) {
          s->color = 0;
          x->parent->color = 1;
          rightRotate(x->parent);
          s = x->parent->left;
        }

        if (s->right->color == 0 && s->right->color == 0) {
          s->color = 1;
          x = x->parent;
        } else {
          if (s->left->color == 0) {
            s->right->color = 0;
            s->color = 1;
            leftRotate(s);
            s = x->parent->left;
          }

          s->color = x->parent->color;
          x->parent->color = 0;
          s->left->color = 0;
          rightRotate(x->parent);
          x = root;
        }
      }
    }
    x->color = 0;
  }

  void rbTransplant(NodePtr u, NodePtr v) {
    if (u->parent == nullptr) {
      root = v;
    } else if (u == u->parent->left) {
      u->parent->left = v;
    } else {
      u->parent->right = v;
    }
    v->parent = u->parent;
  }

  void deleteNodeHelper(NodePtr node, int key) {
    NodePtr z = TNULL;
    NodePtr x, y;
    while (node != TNULL) {
      if (node->data == key) {
        z = node;
      }

      if (node->data <= key) {
        node = node->right;
      } else {
        node = node->left;
      }
    }

    if (z == TNULL) {
      cout << "Key not found in the tree" << endl;
      return;
    }

    y = z;
    int y_original_color = y->color;
    if (z->left == TNULL) {
      x = z->right;
      rbTransplant(z, z->right);
    } else if (z->right == TNULL) {
      x = z->left;
      rbTransplant(z, z->left);
    } else {
      y = minimum(z->right);
      y_original_color = y->color;
      x = y->right;
      if (y->parent == z) {
        x->parent = y;
      } else {
        rbTransplant(y, y->right);
        y->right = z->right;
        y->right->parent = y;
      }

      rbTransplant(z, y);
      y->left = z->left;
      y->left->parent = y;
      y->color = z->color;
    }
    delete z;
    if (y_original_color == 0) {
      deleteFix(x);
    }
  }

  // For balancing the tree after insertion
  void insertFix(NodePtr k) {
    NodePtr u;
    while (k->parent->color == 1) {
      if (k->parent == k->parent->parent->right) {
        u = k->parent->parent->left;
        if (u->color == 1) {
          u->color = 0;
          k->parent->color = 0;
          k->parent->parent->color = 1;
          k = k->parent->parent;
        } else {
          if (k == k->parent->left) {
            k = k->parent;
            rightRotate(k);
          }
          k->parent->color = 0;
          k->parent->parent->color = 1;
          leftRotate(k->parent->parent);
        }
      } else {
        u = k->parent->parent->right;

        if (u->color == 1) {
          u->color = 0;
          k->parent->color = 0;
          k->parent->parent->color = 1;
          k = k->parent->parent;
        } else {
          if (k == k->parent->right) {
            k = k->parent;
            leftRotate(k);
          }
          k->parent->color = 0;
          k->parent->parent->color = 1;
          rightRotate(k->parent->parent);
        }
      }
      if (k == root) {
        break;
      }
    }
    root->color = 0;
  }

  void printHelper(NodePtr root, string indent, bool last) {
    if (root != TNULL) {
      cout << indent;
      if (last) {
        cout << "R----";
        indent += "   ";
      } else {
        cout << "L----";
        indent += "|  ";
      }

      string sColor = root->color ? "RED" : "BLACK";
      cout << root->data << "(" << sColor << ")" << endl;
      printHelper(root->left, indent, false);
      printHelper(root->right, indent, true);
    }
  }

   public:
  RedBlackTree() {
    TNULL = new Node;
    TNULL->color = 0;
    TNULL->left = nullptr;
    TNULL->right = nullptr;
    root = TNULL;
  }

  void preorder() {
    preOrderHelper(this->root);
  }

  void inorder() {
    inOrderHelper(this->root);
  }

  void postorder() {
    postOrderHelper(this->root);
  }

  NodePtr searchTree(int k) {
    return searchTreeHelper(this->root, k);
  }

  NodePtr minimum(NodePtr node) {
    while (node->left != TNULL) {
      node = node->left;
    }
    return node;
  }

  NodePtr maximum(NodePtr node) {
    while (node->right != TNULL) {
      node = node->right;
    }
    return node;
  }

  NodePtr successor(NodePtr x) {
    if (x->right != TNULL) {
      return minimum(x->right);
    }

    NodePtr y = x->parent;
    while (y != TNULL && x == y->right) {
      x = y;
      y = y->parent;
    }
    return y;
  }

  NodePtr predecessor(NodePtr x) {
    if (x->left != TNULL) {
      return maximum(x->left);
    }

    NodePtr y = x->parent;
    while (y != TNULL && x == y->left) {
      x = y;
      y = y->parent;
    }

    return y;
  }

  void leftRotate(NodePtr x) {
    NodePtr y = x->right;
    x->right = y->left;
    if (y->left != TNULL) {
      y->left->parent = x;
    }
    y->parent = x->parent;
    if (x->parent == nullptr) {
      this->root = y;
    } else if (x == x->parent->left) {
      x->parent->left = y;
    } else {
      x->parent->right = y;
    }
    y->left = x;
    x->parent = y;
  }

  void rightRotate(NodePtr x) {
    NodePtr y = x->left;
    x->left = y->right;
    if (y->right != TNULL) {
      y->right->parent = x;
    }
    y->parent = x->parent;
    if (x->parent == nullptr) {
      this->root = y;
    } else if (x == x->parent->right) {
      x->parent->right = y;
    } else {
      x->parent->left = y;
    }
    y->right = x;
    x->parent = y;
  }

  // Inserting a node
  void insert(int key) {
    NodePtr node = new Node;
    node->parent = nullptr;
    node->data = key;
    node->left = TNULL;
    node->right = TNULL;
    node->color = 1;

    NodePtr y = nullptr;
    NodePtr x = this->root;

    while (x != TNULL) {
      y = x;
      if (node->data < x->data) {
        x = x->left;
      } else {
        x = x->right;
      }
    }

    node->parent = y;
    if (y == nullptr) {
      root = node;
    } else if (node->data < y->data) {
      y->left = node;
    } else {
      y->right = node;
    }

    if (node->parent == nullptr) {
      node->color = 0;
      return;
    }

    if (node->parent->parent == nullptr) {
      return;
    }

    insertFix(node);
  }

  NodePtr getRoot() {
    return this->root;
  }

  void deleteNode(int data) {
    deleteNodeHelper(this->root, data);
  }

  void printTree() {
    if (root) {
      printHelper(this->root, "", true);
    }
  }
};

int main() {
  RedBlackTree rbt;
  rbt.insert(55);
  rbt.insert(40);
  rbt.insert(65);
  rbt.insert(60);
  rbt.insert(75);
  rbt.insert(57);

  rbt.printTree();
  cout << endl
     << "After deleting" << endl;
  bst.deleteNode(40);
  bst.printTree();
}
```

___
#### Problems
##### Persistent dynamic sets
A set in which you need to maintain past versions of a dynamic set as it is updated. We call such a set persistent. One way to implement a persistent set is to copy the entire set whenever it is modified, but this approach can slow down a program and also consume a lot of space. 
##### Join operation on red-black trees
he join operation takes two dynamic sets $S_1$ and $S_2$ and an element x such that for any $x_1 \in S_1$ and $x2 \in S_2$, we have $x_{1}.key \leq x.key \leq x_{2}.key$ . It returns a set$S = S_{1} \cup \{ x \} \cup S_{2}$.
##### AVL trees
An AVL tree is a binary search tree that is height balanced: for each node x, the heights of the left and right subtrees of x differ by at most 1. To implement an AVL tree, maintain an extra attribute $h$ in each node such that $x.h$ is the height of node $x$. This ensure that 
This ensures that the tree remains balanced and can perform operations like search, insert, and delete in **O(log n)** time.
After every insertion or deletion, the tree may become unbalanced. When that happens, the tree performs rotations to restore balance.
___
###### 2-3 Trees
- A tree where each node has either 2 or 3 children, and it keeps all its levels balanced (i.e., all leaves are at the same level).
- The tree adjusts its structure by merging and splitting nodes when necessary, so that all paths from the root to a leaf have the same length, ensuring balance.
-  The uniform structure helps maintain **logarithmic time complexity** for operations. It's a predecessor to more complex trees like B-trees.
###### B-Trees
- A generalized version of the 2-3 tree, where each node can have **more than 2 or 3 children**. B-trees are widely used in databases and filesystems.
- B-trees keep data sorted and allow searches, sequential access, insertions, and deletions in **logarithmic time**. It handles large amounts of data efficiently by keeping the tree balanced across multiple levels.
- It minimizes disk access times and is ideal for systems that need to store large amounts of data.
###### Red-Black Trees (Bayer, Guibas, and Sedgewick)
- A self-balancing binary search tree with an additional color property (red or black) for each node.
- The tree ensures balance by following certain rules:
    1. Every node is either red or black.
    2. The root is always black.
    3. No two red nodes can be adjacent.
    4. Every path from a node to its leaves must have the same number of black nodes.
    These properties help the tree stay approximately balanced, leading to **O(log n)** time complexity for insertions, deletions, and searches.
- **Variants**:
    - AA-trees: A simpler version of red-black trees where left children are never red, making it easier to code.
    - Left-Leaning Red-Black Trees (LLRB): A modified version where red links always lean left, simplifying the balancing operations.
###### 5. Treaps (Seidel and Aragon)
- A hybrid between a **binary search tree** and a **heap**.
- Each node has both a key (for the binary search tree property) and a priority (for the heap property). The nodes are arranged like a binary search tree based on keys, but they also follow the heap property for priorities.
- It allows for randomized balancing of the tree, ensuring that operations like insert and delete still take **O(log n)** time.
###### 6. Splay Trees (Sleator and Tarjan)
-  A type of **self-adjusting binary search tree**.
- Every time you access a node (whether you're inserting, searching, or deleting), the tree performs a "splay" operation, which moves the node to the root through a series of rotations.
- Splay trees don't require an explicit balance condition like red-black trees or AVL trees. Instead, the splaying operation keeps the tree balanced over time. This is particularly useful when some elements are accessed more frequently than others because frequently accessed elements move closer to the root.
- **Amortized cost**: On average, the cost per operation is **O(log n)** over a sequence of operations.
###### Skip Lists (Pugh)
- A linked list that is augmented with multiple layers of additional pointers, allowing for faster search operations.
- It uses a probabilistic method to build multiple "levels" of linked lists. Each level skips over more elements, allowing search operations to skip over large sections of the list, similar to a binary search.
- It provides expected O(log n) time complexity for search, insert, and delete operations, and it's much simpler to implement than a balanced tree.
___