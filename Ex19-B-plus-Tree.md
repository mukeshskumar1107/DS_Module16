# Ex19 B+ Tree
## DATE: 25-03-2025
## AIM:
To write a C function to traverse the elements in a B+ Tree.

## Algorithm
1. Start 
2. Iterate through each element in the node's data array. 
3. If the node is not a leaf, recursively call traverse on the current child pointer. 
4. Print the current data element. 
5. After the loop, if the node is not a leaf, traverse the last child pointer. 
6. Return after completing the traversal. 
7. End    

## Program:
```c
/*
Program to traverse the elements in a B+ Tree.
Developed by: MUKESH KUMAR S 
Register Number: 212223240099 
*/

#include <stdio.h>
#include <stdio.h>
#include <stdlib.h>

struct B_TreeNode
{
    int *data;
    struct B_TreeNode **child_ptr;
    int leaf;
    int n;
};
struct B_TreeNode *root = NULL, *np = NULL, *x = NULL;
struct B_TreeNode *init()
{
    int i;
    np = (struct B_TreeNode *)malloc(sizeof(struct B_TreeNode));
    np->data = (int *)malloc(5 * sizeof(int));
    np->child_ptr = (struct B_TreeNode **)malloc(6 * sizeof(struct B_TreeNode **));
    np->leaf = 1;
    np->n = 0;
    for (i = 0; i < 6; i++)
    {
        np->child_ptr[i] = NULL;
    }
    return np;
}
void traverse(struct B_TreeNode *p)
{
    // type your code here
    int i;
    for (i = 0; i < p->n; i++)
    {
        if (p->leaf == 0)
        {
            traverse(p->child_ptr[i]);
        }
        printf("%d ", p->data[i]);
    }
    if (p->leaf == 0)
    {
        traverse(p->child_ptr[i]);
    }
}
void sort(int *p, int n)
{
    int i, j, temp;
    for (i = 0; i < n; i++)
    {
        for (j = i; j <= n; j++)
        {
            if (p[i] > p[j])
            {
                temp = p[i];
                p[i] = p[j];
                p[j] = temp;
            }
        }
    }
}
int split_child(struct B_TreeNode *x, int i)
{
    int j, mid;
    struct B_TreeNode *np1, *np3, *y;
    np3 = init();
    np3->leaf = 1;
    if (i == -1)
    {
        mid = x->data[2];
        x->data[2] = 0;
        x->n--;
        np1 = init();
        np1->leaf = 0;
        x->leaf = 1;
        for (j = 3; j < 5; j++)
        {
            np3->data[j - 3] = x->data[j];
            np3->child_ptr[j - 3] = x->child_ptr[j];
            np3->n++;
            x->data[j] = 0;
            x->n--;
        }
        for (j = 0; j < 6; j++)
        {
            x->child_ptr[j] = NULL;
        }
        np1->data[0] = mid;
        np1->child_ptr[np1->n] = x;
        np1->child_ptr[np1->n + 1] = np3;
        np1->n++;
        root = np1;
    }
    else
    {
        y = x->child_ptr[i];
        mid = y->data[2];
        y->data[2] = 0;
        y->n--;
        for (j = 3; j < 5; j++)
        {
            np3->data[j - 3] = y->data[j];
            np3->n++;
            y->data[j] = 0;
            y->n--;
        }
        x->child_ptr[i + 1] = y;
        x->child_ptr[i + 1] = np3;
    }
    return mid;
}
void insert(int a)
{
    int i, temp;
    x = root;
    if (x == NULL)
    {
        root = init();
        x = root;
    }
    else
    {
        if (x->leaf == 1 && x->n == 5)
        {
            temp = split_child(x, -1);
            x = root;
            for (i = 0; i < (x->n); i++)
            {
                if ((a > x->data[i]) && (a < x->data[i + 1]))
                {
                    i++;
                    break;
                }
                else if (a < x->data[0])
                {
                    break;
                }
                else
                {
                    continue;
                }
            }
            x = x->child_ptr[i];
        }
        else
        {
            while (x->leaf == 0)
            {
                for (i = 0; i < (x->n); i++)
                {
                    if ((a > x->data[i]) && (a < x->data[i + 1]))
                    {
                        i++;
                        break;
                    }
                    else if (a < x->data[0])
                    {
                        break;
                    }
                    else
                    {
                        continue;
                    }
                }
                if ((x->child_ptr[i])->n == 5)
                {
                    temp = split_child(x, i);
                    x->data[x->n] = temp;
                    x->n++;
                    continue;
                }
                else
                {
                    x = x->child_ptr[i];
                }
            }
        }
    }
    x->data[x->n] = a;
    sort(x->data, x->n);
    x->n++;
}
int main()
{
    int i, n, t;
    scanf("%d", &n);
    for (i = 0; i < n; i++)
    {

        scanf("%d", &t);
        insert(t);
    }
    // cout<<"traversal of constructed tree\n";
    traverse(root);
}
```

## Output:
<img width="864" height="302" alt="image" src="https://github.com/user-attachments/assets/aea03a4f-d137-4aec-b4a7-5b696d970548" />



## Result:
Thus, the function to traverse the elements in a B+ Tree is implemented successfully.
