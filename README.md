# Ex. No : 12	
# IMPLEMENTATION OF HEAP STORAGE ALLOCATION STRATEGY 
## Register Number : 212223040236
## Date : 25/04/2024

## AIM   
To write a program to implement heap storage allocation strategy.

## ALGORITHM
1.	Start the program.
2.	Define a function create( ) to create a list of allocated node. This function returns a pointer to head of list.
3.	Define a function display(node) to display the list of allocated nodes.
4.	Define a function search(node,key) to search for the element in list.
5.	Define a function insert(node) to insert element into the list.
6.	Define a function get_prev(node,value) to look for the previous element in the list.
7.	Define a function delete() to remove an element from the list.
8.	Stop the program.

## PROGRAM
## exp12.c:
```
#include<stdio.h>
#include<stdlib.h>

#define TRUE 1
#define FALSE 0

typedef struct Heap {
    int data;
    struct Heap *next;
} node;

node *create();
void display(node *);
node *search(node *, int);
node *insert(node *);
void dele(node **);
node *get_node();
node *insert_head(node *);
void insert_last(node *);

int main() {
    int choice;
    node *head = NULL;

    do {
        printf("\nProgram to perform various operations on heap using dynamic memory management");
        printf("\n1. Create");
        printf("\n2. Display");
        printf("\n3. Insert an element in the list");
        printf("\n4. Delete an element from the list");
        printf("\n5. Quit");
        printf("\nEnter your choice (1-5): ");
        scanf("%d", &choice);

        switch(choice) {
            case 1:
                head = create();
                break;
            case 2:
                display(head);
                break;
            case 3:
                head = insert(head);
                break;
            case 4:
                dele(&head);
                break;
            case 5:
                exit(0);
            default:
                printf("Invalid choice, try again\n");
        }
    } while(choice != 5);

    return 0;
}

node *create() {
    int val;
    char ans;
    node *New, *head = NULL;

    do {
        printf("\nEnter the element: ");
        scanf("%d", &val);
        New = get_node();

        if(New == NULL)
            printf("\nMemory is not allocated");
        else {
            New->data = val;
            New->next = NULL;

            if(head == NULL)
                head = New;
            else {
                New->next = head;
                head = New;
            }
        }

        printf("\nDo you want to enter more elements? (y/n): ");
        scanf(" %c", &ans);
    } while(ans == 'y');

    printf("\nThe list is created\n");
    return head;
}

node *get_node() {
    node *temp;
    temp = (node*)malloc(sizeof(node));
    if(temp == NULL)
        printf("\nMemory is not allocated\n");
    return temp;
}

void display(node *head) {
    node *temp;
    temp = head;

    if(temp == NULL) {
        printf("\nThe list is empty\n");
        return;
    }

    printf("List elements: ");
    while(temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

node *search(node *head, int key) {
    node *temp;
    int found;
    temp = head;

    if(temp == NULL) {
        printf("\nThe linked list is empty\n");
        return NULL;
    }

    found = FALSE;
    while(temp != NULL && found == FALSE) {
        if(temp->data != key)
            temp = temp->next;
        else
            found = TRUE;
    }

    if(found == TRUE) {
        printf("\nThe element is present in the list\n");
        return temp;
    } else {
        printf("\nThe element is not present in the list\n");
        return NULL;
    }
}

node *insert(node *head) {
    int choice;

    printf("\n1. Insert a node as a head node");
    printf("\n2. Insert a node as a last node");
    printf("\nEnter your choice for insertion of node: ");
    scanf("%d", &choice);

    switch(choice) {
        case 1:
            head = insert_head(head);
            break;
        case 2:
            insert_last(head);
            break;
    }
    return head;
}

node *insert_head(node *head) {
    node *New, *temp;
    New = get_node();

    printf("\nEnter the element which you want to insert: ");
    scanf("%d", &New->data);

    if(head == NULL)
        head = New;
    else {
        temp = head;
        New->next = temp;
        head = New;
    }

    return head;
}

void insert_last(node *head) {
    node *New, *temp;
    New = get_node();

    printf("\nEnter the element which you want to insert: ");
    scanf("%d", &New->data);

    if(head == NULL)
        head = New;
    else {
        temp = head;
        while(temp->next != NULL)
            temp = temp->next;
        temp->next = New;
    }
}

void dele(node **head) {
    int val;
    node *temp, *prev;
    temp = *head;

    if(temp == NULL) {
        printf("\nThe list is empty\n");
        return;
    }

    printf("\nEnter the value to be deleted: ");
    scanf("%d", &val);

    prev = NULL;
    if(temp != NULL && temp->data == val) {
        *head = temp->next;
        free(temp);
        printf("\nElement deleted successfully\n");
        return;
    }

    while(temp != NULL && temp->data != val) {
        prev = temp;
        temp = temp->next;
    }

    if(temp == NULL) {
        printf("\nElement not found in the list\n");
        return;
    }

    prev->next = temp->next;
    free(temp);
    printf("\nElement deleted successfully\n");
}
```
## OUTPUT 
![image](https://github.com/vijaygowdu/19CS409-Compiler-Design-Lab/assets/147473788/117d994e-a838-4dff-8792-07fbb571a957)

## RESULT
The heap storage allocation strategy is implemented successfully, and the output is verified.
