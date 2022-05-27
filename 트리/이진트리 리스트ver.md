```C
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode
{
	char elem;
	struct TreeNode* parent, * left, * right;
}TreeNode;

TreeNode* root;

TreeNode* makeNode(char elem, TreeNode* parent, TreeNode* left, TreeNode* right)
{
	TreeNode* temp = (TreeNode*)malloc(sizeof(TreeNode));
	temp->elem = elem;
	temp->parent = parent;
	temp->left = left;
	temp->right = right;
	return temp;
}

void inOrder(TreeNode* root)
{
	if (root != NULL)
	{
		inOrder(root->left);
		printf("[%c] ", root->elem);
		inOrder(root->right);
	}
}

void preOrder(TreeNode* root)
{
	if (root != NULL) {
		printf("[%c] ", root->elem);
		preOrder(root->left);
		preOrder(root->right);
	}
}

void postOrder(TreeNode* root)
{
	if (root != NULL) {
		postOrder(root->left);
		postOrder(root->right);
		printf("[%c] ", root->elem);
	}
}


char element(TreeNode* v)
{
	return v->elem;
}

TreeNode* rootNode()
{
	return root;
}

int isRoot(TreeNode* v)
{
	return v == root;
}

TreeNode* parent(TreeNode* v)
{
	return v->parent;
}

TreeNode* leftChild(TreeNode* v)
{
	return v->left;
}

TreeNode* rightChild(TreeNode* v)
{
	return v->right;
}

TreeNode* sibling(TreeNode* v)
{
	TreeNode* p = v->parent;
	if (p->left == v)
		return p->right;
	else
		return p->left;
}

int isExternal(TreeNode* v)
{
	return (v->left == NULL && v->right == NULL);
}

int isInternal(TreeNode* v)
{
	return (v->left != NULL && v->right != NULL);
}

char setElement(TreeNode* v, char e)
{
	v->elem = e;
	return e;
}

void swapElements(TreeNode* v, TreeNode* w)
{
	char tmp = v->elem;
	v->elem = w->elem;
	w->elem = tmp;
	return;
}

int main()
{
	TreeNode* n9 = makeNode('I', NULL, NULL, NULL);
	TreeNode* n8 = makeNode('H', NULL, NULL, NULL);
	TreeNode* n7 = makeNode('G', NULL, NULL, NULL);
	TreeNode* n6 = makeNode('F', NULL, NULL, NULL);
	TreeNode* n5 = makeNode('E', NULL, n8, n9);
	TreeNode* n4 = makeNode('D', NULL, NULL, NULL);
	TreeNode* n3 = makeNode('C', NULL, n6, n7);
	TreeNode* n2 = makeNode('B', NULL, n4, n5);
	TreeNode* n1 = makeNode('A', NULL, n2, n3);

	root = n1;
	n8->parent = n9->parent = n5;
	n6->parent = n7->parent = n3;
	n4->parent = n5->parent = n2;
	n2->parent = n3->parent = root;

    printf("InOrder   : ");  inOrder(root); printf("\n");
	printf("PreOrder  : ");  preOrder(root); printf("\n");
	printf("PostOrder : ");  postOrder(root); printf("\n\n");

	printf("Element of n7 : %c\n", element(n7));
	printf("Element of root : %c\n", element(rootNode()));
	printf("n2 is root node? %s\n", isRoot(n2) ? "Yes" : "No");
	printf("Element of n7's parent : %c\n", element(parent(n7)));
	printf("Element of n2's leftChild : %c\n", element(leftChild(n2)));
	printf("Element of n2's rightChild : %c\n", element(rightChild(n2)));
	printf("Element of n4's sibling : %c\n", element(sibling(n4)));
	printf("Element of n5's sibling : %c\n", element(sibling(n5)));
	printf("n5 is Internode? %s\n", isInternal(n5) ? "Yes" : "No");
	printf("n4 is Internode? %s\n", isInternal(n4) ? "Yes" : "No");
	printf("n5 is Externode? %s\n", isExternal(n5) ? "Yes" : "No");
	printf("n4 is Externode? %s\n", isExternal(n4) ? "Yes" : "No");
	printf("n4 is Externode? %s\n", isExternal(n4) ? "Yes" : "No");
	printf("n7's new element is %c\n", setElement(n7, 'Z'));
	printf("Element of n7 : %c\n", element(n7));

	swapElements(n8, n9);
	printf("n8, n9 elements are swapped\n");
	printf("Element of n8 : %c\n", element(n8));
	printf("Element of n9 : %c\n", element(n9));
}
```
