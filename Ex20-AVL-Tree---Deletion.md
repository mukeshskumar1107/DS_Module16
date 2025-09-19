# Ex20 AVL Tree - Deletion
## DATE: 23-03-2025
## AIM:
To write a C function to delete an element from an AVL Tree.
## Algorithm
1. Start
2. Search for the node to delete starting from the root. 
3. Delete the node using standard BST rules. 
4. Update the height of the affected nodes. 
5. Calculate the balance factor of each updated node. 
6. Perform rotations if the node is unbalanced. 
7. Continue until the tree is balanced again.
8. End 

## Program:
```c
/*
Create a C program to delete an element from an AVL Tree.
Developed by: MUKESH KUMAR S 
Register Number: 212223240099 
*/

#include <stdio.h>
#include <stdlib.h>

typedef struct node
{
    int data;
    struct node *left, *right;
    int ht;
} node;

node *insert(node *, int);
node *Delete(node *, int);
void preorder(node *);
void inorder(node *);
int height(node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);

int main()
{
    node *root = NULL;
    int x, n, i;
    scanf("%d", &n);
    // printf("\nEnter tree data:");
    root = NULL;
    for (i = 0; i < n; i++)
    {
        scanf("%d", &x);
        root = insert(root, x);
    }
    // printf("\nEnter a data:");
    scanf("%d", &x);
    root = Delete(root, x);
    // printf("\nPreorder sequence:\n");
    preorder(root);
    return 0;
}

node *insert(node *T, int x)
{
    if (T == NULL)
    {
        T = (node *)malloc(sizeof(node));
        T->data = x;
        T->left = NULL;
        T->right = NULL;
    }
    else if (x > T->data) // insert in right subtree
    {
        T->right = insert(T->right, x);
        if (BF(T) == -2)
        {
            if (x > T->right->data)
                T = RR(T);
            else
                T = RL(T);
        }
    }
    else if (x < T->data)
    {
        T->left = insert(T->left, x);
        if (BF(T) == 2)
        {
            if (x < T->left->data)
                T = LL(T);
            else
                T = LR(T);
        }
    }
    T->ht = height(T);
    return (T);
}

node *Delete(node *T, int x)
{
    // type your code here
    node *p;

    if (T == NULL)
    {
        return NULL;
    }
    else if (x > T->data)
    {
        T->right = Delete(T->right, x);

        if (BF(T) == 2)
        {
            if (BF(T->left) >= 0)
            {
                T = LL(T);
            }
            else
            {
                T = LR(T);
            }
        }
    }
    else if (x < T->data)
    {
        T->left = Delete(T->left, x);

        if (BF(T) == -2)
        {
            if (BF(T->right) <= 0)
            {
                T = RR(T);
            }
            else
            {
                T = RL(T);
            }
        }
    }
    else
    {
        if (T->right != NULL)
        {
            p = T->right;
            while (p->left != NULL)
                p = p->left;

            T->data = p->data;
            T->right = Delete(T->right, p->data);

            if (BF(T) == 2)
            {
                if (BF(T->left) >= 0)
                {
                    T = LL(T);
                }
                else
                {
                    T = LR(T);
                }
            }
        }
        else
            return T->left;
    }
    T->ht = height(T);
    return T;
}

int height(node *T)
{
    int lh, rh;
    if (T == NULL)
        return (0);
    if (T->left == NULL)
        lh = 0;
    else
        lh = 1 + T->left->ht;
    if (T->right == NULL)
        rh = 0;
    else
        rh = 1 + T->right->ht;
    if (lh > rh)
        return (lh);
    return (rh);
}

node *rotateright(node *x)
{
    node *y;
    y = x->left;
    x->left = y->right;
    y->right = x;
    x->ht = height(x);
    y->ht = height(y);
    return (y);
}

node *rotateleft(node *x)
{
    node *y;
    y = x->right;
    x->right = y->left;
    y->left = x;
    x->ht = height(x);
    y->ht = height(y);
    return (y);
}

node *RR(node *T)
{
    T = rotateleft(T);
    return (T);
}

node *LL(node *T)
{
    T = rotateright(T);
    return (T);
}

node *LR(node *T)
{
    T->left = rotateleft(T->left);
    T = rotateright(T);
    return (T);
}

node *RL(node *T)
{
    T->right = rotateright(T->right);
    T = rotateleft(T);
    return (T);
}

int BF(node *T)
{
    int lh, rh;
    if (T == NULL)
        return (0);

    if (T->left == NULL)
        lh = 0;
    else
        lh = 1 + T->left->ht;

    if (T->right == NULL)
        rh = 0;
    else
        rh = 1 + T->right->ht;

    return (lh - rh);
}

void preorder(node *T)
{
    if (T != NULL)
    {
        printf("%d(Bf=%d)", T->data, BF(T));
        preorder(T->left);
        preorder(T->right);
    }
}

void inorder(node *T)
{
    if (T != NULL)
    {
        inorder(T->left);
        printf("%d(Bf=%d)", T->data, BF(T));
        inorder(T->right);
    }
}
```

## Output:
<img width="1076" height="258" alt="image" src="https://github.com/user-attachments/assets/d397ab96-a6a7-47e1-ad8d-2ced5e16ea16" />



## Result:
Thus, the C program to delete an element from an AVL Tree is implemented successfully.
