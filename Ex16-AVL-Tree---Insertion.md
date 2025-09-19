# Ex16 AVL Tree - Insertion
## DATE: 25-03-2025
## AIM:
To write a C function to insert the elements in an AVL Tree.

## Algorithm
1. Start 
2. If the node is NULL, create a new node with value x. 
3. Insert x recursively into the left or right subtree based on comparison. 
4. Calculate the balance factor (BF) after insertion. 
5. If BF is -2 or 2, perform appropriate rotations (RR, RL, LL, or LR). 
6. Update the height of the current node. 
7. Return the new root after insertion and balancing.. 
8. End   

## Program:
```c
/*
Program to insert the elements in an AVL Tree
Developed by: MUKESH KUMAR S
Register Number: 212223240099 
*/

/*
typedef struct node
{
    int data;
    struct node *left, *right;
    int ht;
} node;
node *insert(node *, int);
void preorder(node *);
// void inorder(node *);
int height(node *);
node *rotateright(node *);
node *rotateleft(node *);
node *RR(node *);
node *LL(node *);
node *LR(node *);
node *RL(node *);
int BF(node *);
*/

node *insert(node *T, int x)
{
    // type your code here
    if (T == NULL)
    {
        T = (node *)malloc(sizeof(node));
        T->data = x;
        T->right = NULL;
        T->left = NULL;
    }
    else if (x > T->data)
    {
        T->right = insert(T->right, x);

        if (BF(T) == -2)
        {
            if (x > T->right->data)
            {
                T = RR(T);
            }
            else
            {
                T = RL(T);
            }
        }
    }
    else if (x < T->data)
    {
        T->left = insert(T->left, x);

        if (BF(T) == 2)
        {
            if (x < T->left->data)
            {
                T = LL(T);
            }
            else
            {
                T = LR(T);
            }
        }
    }

    T->ht = height(T);
    return T;
}
```

## Output:
<img width="1180" height="191" alt="image" src="https://github.com/user-attachments/assets/15af13b3-cabd-4e8d-ac1a-0b119f076533" />


## Result:
Thus, the function to insert the elements in an AVL Tree is implemented successfully in C programming language.
