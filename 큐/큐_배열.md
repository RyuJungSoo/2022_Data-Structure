```C
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define N 10

typedef char element;

typedef struct
{
	element queue[N];
	int front, rear;

}QueueType;

void init(QueueType* Q)
{
	Q->rear = Q->front = 0;
}

int isEmpty(QueueType* Q)
{
	return Q->front == Q->rear;
}

int isFull(QueueType* Q)
{
	return Q->front == (Q->rear + 1) % N;
}

void enqueue(QueueType* Q, element e)
{
	if (isFull(Q))
		printf("FULL\n");
	else
	{
		Q->rear = (Q->rear + 1) % N;
		Q->queue[Q->rear] = e;
	}
}

element dequeue(QueueType* Q)
{
	if (isEmpty(Q))
	{
		printf("Empty\n");
		return -1;
	}
	Q->front = (Q->front + 1) % N;
	return Q->queue[Q->front];
}

element front(QueueType* Q)
{
	if (isEmpty(Q))
	{
		printf("Empty\n");
		return -1;
	}
	return Q->queue[(Q->front+1) % N];
}

int size(QueueType* Q)
{
	return (N - Q->front + Q->rear) % N;
}

void print(QueueType* Q)
{
	printf("Front : %d, Rear : %d\n", Q->front, Q->rear);
	int i = Q->front;
	while (i != Q->rear)
	{
		i = (i + 1) % N;
		printf("[%c] ", Q->queue[i]);
	}
	printf("\n");
}

int main()
{
	QueueType Q;
	init(&Q);
	srand(time(NULL));

	for (int i = 0; i < 7; i++)
	{
		enqueue(&Q, rand()%26+65);
	}
	print(&Q); getchar();

	for (int i = 0; i < 3; i++)
		printf("[%c] ", dequeue(&Q));
	printf("\n\n");
	print(&Q); getchar();

	for (int i = 0; i < 6; i++)
	{
		enqueue(&Q, rand() % 26 + 65);
	}
	print(&Q); getchar();

	for (int i = 0; i < 3; i++)
		printf("[%c] ", dequeue(&Q));
	printf("\n\n");
	print(&Q); getchar();

	printf("[%c]\n", front(&Q)); print(&Q);
	printf("[%d]\n", size(&Q));

	return 0;
}
```
