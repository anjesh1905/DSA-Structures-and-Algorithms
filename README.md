# DSA-Structures-and-Algorithms
DSA assignment - Stack and Circular Queue using C
Name :- Anjesh Gaurav 
ID :- BC2025566
Q1) Design and implement a stack using an array without using any built-in stack library.
Perform the following operations:
 PUSH(x)
 POP()
 PEEK()
 DISPLAY()
Your program must handle both Stack Overflow and Stack Underflow conditions.
Additional Task:
Explain the time complexity and space complexity of each operation. Also discuss what 
happens when the stack size is fixed and the user attempts to insert more elements than its 
capacity.
Answers:- 

A stack is a linear data structure in which insertion and deletion of elements take place from only one end, called the TOP.
Stack follows the principle of LIFO (Last In, First Out). This means the element inserted last is removed first.
For example:
PUSH: 10 → 20 → 30

Stack:
30 ← TOP
20
10
If we perform POP(), 30 will be removed first.
Basic Stack Operations
1. PUSH(x):
PUSH is used to insert an element into the stack. Before insertion, we check whether the stack is full.
2. POP():
POP removes the element from the top of the stack. If the stack is empty, Stack Underflow occurs.
3. PEEK():
PEEK returns/displays the top element without removing it.
4. DISPLAY():
DISPLAY shows all the elements present in the stack.
Stack Overflow
When the stack is implemented using a fixed-size array and we try to insert an element when the stack is already full, Stack Overflow occurs.
For an array of size 5:
TOP = MAX - 1
means the stack is full.
Stack Underflow
When we try to remove an element from an empty stack, Stack Underflow occurs.
TOP = -1
means the stack is empty.
C Program
#include <stdio.h>

#define MAX 5

int stack[MAX];
int top = -1;

void push(int x)
{
    if (top == MAX - 1)
    {
        printf("Stack Overflow!\n");
    }
    else
    {
        top++;
        stack[top] = x;
        printf("%d pushed into stack.\n", x);
    }
}

void pop()
{
    if (top == -1)
    {
        printf("Stack Underflow!\n");
    }
    else
    {
        printf("%d popped from stack.\n", stack[top]);
        top--;
    }
}

void peek()
{
    if (top == -1)
    {
        printf("Stack is empty!\n");
    }
    else
    {
        printf("Top element is: %d\n", stack[top]);
    }
}

void display()
{
    int i;

    if (top == -1)
    {
        printf("Stack is empty!\n");
    }
    else
    {
        printf("Stack elements are:\n");

        for (i = top; i >= 0; i--)
        {
            printf("%d\n", stack[i]);
        }
    }
}

int main()
{
    int choice, value;

    while (1)
    {
        printf("\n--- STACK MENU ---\n");
        printf("1. PUSH\n");
        printf("2. POP\n");
        printf("3. PEEK\n");
        printf("4. DISPLAY\n");
        printf("5. EXIT\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                printf("Enter value: ");
                scanf("%d", &value);
                push(value);
                break;

            case 2:
                pop();
                break;

            case 3:
                peek();
                break;

            case 4:
                display();
                break;

            case 5:
                return 0;

            default:
                printf("Invalid choice!\n");
        }
    }

    return 0;
}

Q2. Implement a Circular Queue using an array. The queue should support:
 ENQUEUE(x)
 DEQUEUE()
 FRONT()
 DISPLAY()
The implementation must correctly distinguish between a full queue and an empty queue.
Additional Task:
Compare the circular queue with a simple linear queue and explain:
1. Why a circular queue provides better utilization of memory.
2. Time complexity of ENQUEUE and DEQUEUE.
3. Space complexity of the queue.
4. What problem occurs in a linear queue when REAR reaches the last index even 
though unused positions exist at the beginning.

Answers :- 
A queue is a linear data structure in which insertion takes place from one end called REAR, and deletion takes place from the other end called FRONT.
A queue follows FIFO (First In, First Out) principle. This means the element inserted first is removed first.
A circular queue is a queue in which the last position of the array is connected back to the first position. It allows the queue to reuse previously occupied positions.
Circular Queue Operations
1. ENQUEUE(x):
Adds an element at the REAR of the queue.
2. DEQUEUE():
Removes an element from the FRONT of the queue.
3. FRONT():
Returns/displays the element present at the front.
4. DISPLAY():
Displays all elements currently present in the queue.
Full Condition
The circular queue is full when:
(rear + 1) % MAX == front
Empty Condition
The queue is empty when:
front == -1
C Program
#include <stdio.h>

#define MAX 5

int queue[MAX];
int front = -1;
int rear = -1;

void enqueue(int x)
{
    if ((rear + 1) % MAX == front)
    {
        printf("Queue is Full!\n");
        return;
    }

    if (front == -1)
    {
        front = 0;
        rear = 0;
    }
    else
    {
        rear = (rear + 1) % MAX;
    }

    queue[rear] = x;
    printf("%d inserted into queue.\n", x);
}

void dequeue()
{
    if (front == -1)
    {
        printf("Queue is Empty!\n");
        return;
    }

    printf("%d deleted from queue.\n", queue[front]);

    if (front == rear)
    {
        front = -1;
        rear = -1;
    }
    else
    {
        front = (front + 1) % MAX;
    }
}

void getFront()
{
    if (front == -1)
    {
        printf("Queue is Empty!\n");
    }
    else
    {
        printf("Front element is: %d\n", queue[front]);
    }
}

void display()
{
    int i;

    if (front == -1)
    {
        printf("Queue is Empty!\n");
        return;
    }

    printf("Queue elements are:\n");

    i = front;

    while (1)
    {
        printf("%d ", queue[i]);

        if (i == rear)
            break;

        i = (i + 1) % MAX;
    }

    printf("\n");
}

int main()
{
    int choice, value;

    while (1)
    {
        printf("\n--- CIRCULAR QUEUE MENU ---\n");
        printf("1. ENQUEUE\n");
        printf("2. DEQUEUE\n");
        printf("3. FRONT\n");
        printf("4. DISPLAY\n");
        printf("5. EXIT\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                printf("Enter value: ");
                scanf("%d", &value);
                enqueue(value);
                break;

            case 2:
                dequeue();
                break;

            case 3:
                getFront();
                break;

            case 4:
                display();
                break;

            case 5:
                return 0;

            default:
                printf("Invalid choice!\n");
        }
    }

    return 0;
}
Circular Queue vs Simple Linear Queue
1. Why does a circular queue provide better memory utilization?
In a simple linear queue, after deleting elements from the front, the empty positions at the beginning may not be reused easily. A circular queue solves this problem by connecting the last position back to the first position.
Therefore, the unused positions can be reused.
2. Time Complexity
Operation
Time Complexity
ENQUEUE
O(1)
DEQUEUE
O(1)
FRONT
O(1)
DISPLAY
O(n)
The assignment specifically asks for the complexity of ENQUEUE and DEQUEUE. �
DSA Assignment Structures & Algorithms.docx
3. Space Complexity
The space complexity of a circular queue implemented using an array of size n is:
O(n)
because the queue requires an array capable of storing up to n elements.
4. Problem in a Linear Queue
Suppose the queue has size 5:
[ _ ][ _ ][ 30 ][ 40 ][ 50 ]
  ↑              ↑
 empty          REAR
The first two positions are empty, but REAR has already reached the last index.
In a simple linear queue, another element cannot be inserted because REAR is at the last position. This results in wasted space / false overflow.
A circular queue allows REAR to move back to the beginning:
[ 60 ][ 70 ][ 30 ][ 40 ][ 50 ]
   ↑
 REAR
