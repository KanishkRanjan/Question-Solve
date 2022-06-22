Given a Binary Tree, write an iterative function to print the Preorder traversal of the given binary tree.  
Refer to [this](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/) for recursive preorder traversal of Binary Tree. To convert an inherently recursive procedure to iterative, we need an explicit stack. Following is a simple stack based iterative process to print Preorder traversal.   
**1)** Create an empty stack _nodeStack_ and push root node to stack.   
**2)** Do the following while _nodeStack_ is not empty.   
….**a)** Pop an item from the stack and print it.   
….**b)** Push right child of a popped item to stack   
….**c)** Push left child of a popped item to stack  
The right child is pushed before the left child to make sure that the left subtree is processed first.

```
// C++ program to implement iterative preorder traversal
#include <bits/stdc++.h>

using namespace std;

/* A binary tree node has data, left child and right child */
struct node {
	int data;
	struct node* left;
	struct node* right;
};

/* Helper function that allocates a new node with the given data and
NULL left and right pointers.*/
struct node* newNode(int data)
{
	struct node* node = new struct node;
	node->data = data;
	node->left = NULL;
	node->right = NULL;
	return (node);
}

// An iterative process to print preorder traversal of Binary tree
void iterativePreorder(node* root)
{
	// Base Case
	if (root == NULL)
		return;

	// Create an empty stack and push root to it
	stack<node*> nodeStack;
	nodeStack.push(root);

	/* Pop all items one by one. Do following for every popped item
	a) print it
	b) push its right child
	c) push its left child
	Note that right child is pushed first so that left is processed first */
	while (nodeStack.empty() == false) {
		// Pop the top item from stack and print it
		struct node* node = nodeStack.top();
		printf("%d ", node->data);
		nodeStack.pop();

		// Push right and left children of the popped node to stack
		if (node->right)
			nodeStack.push(node->right);
		if (node->left)
			nodeStack.push(node->left);
	}
}

// Driver program to test above functions
int main()
{
	/* Constructed binary tree is
			10
		/ \
		8	 2
	/ \ /
	3	 5 2
*/
	struct node* root = newNode(10);
	root->left = newNode(8);
	root->right = newNode(2);
	root->left->left = newNode(3);
	root->left->right = newNode(5);
	root->right->left = newNode(2);
	iterativePreorder(root);
	return 0;
}

```
