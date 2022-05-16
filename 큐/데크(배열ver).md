```C
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define N 100



typedef struct
{
	int* element;
	int front, rear;

}Deque;

void init(Deque* D)
{
	D->element = (int*)malloc(sizeof(int) * N);
	D->front = 0;
	D->rear = 0;
}

int isEmpty(Deque* D)
{
	return D->front == D->rear;
}

int isFull(Deque* D)
{
	return (D->rear + 1) % N == D->front;
}

void addRear(Deque* D, char elem)
{
	if (isFull(D))
	{
		printf("FULL\n");
		return;
	}
	D->rear = (D->rear + 1) % N;
	D->element[D->rear] = elem;
}

void addFront(Deque* D, char elem)
{
	if (isFull(D))
	{
		printf("FULL\n");
		return;
	}
	D->element[D->front] = elem;
	D->front = (D->front - 1 + N) % N;
}

int deleteFront(Deque* D)
{
	if (isEmpty(D))
	{
		printf("underflow\n");
		return -1;
	}
	D->front = (D->front + 1) % N;
	return D->element[D->front];
}

int deleteRear(Deque* D)
{
	if (isEmpty(D))
	{
		printf("underflow\n");
		return -1;
	}
	int pos = D->rear;
	D->rear = (D->rear - 1 + N) % N;
	return D->element[pos];
}

void print(Deque* Q)
{
	int i = Q->front;
	while (i != Q->rear)
	{
		i = (i + 1) % N;
		printf(" %d", Q->element[i]);
	}
	printf("\n");
}

int main()
{
	Deque D;
	int n,i, num, flag = 0;
	char order[3];
	

	scanf("%d", &n);
	getchar();
	init(&D);

	for (i = 0; i < n; i++)
	{
		flag = 0;
		scanf("%s", order);
		getchar();

		if (strcmp(order, "AF") == 0)
		{
			scanf("%d", &num);
			getchar();
			addFront(&D, num);
		}

		else if (strcmp(order, "AR") == 0)
		{
			scanf("%d", &num);
			getchar();
			addRear(&D, num);
		}

		else if (strcmp(order, "DF") == 0)
		{
			flag = deleteFront(&D);

			if (flag == -1)
				return 0;
		}

		else if (strcmp(order, "DR") == 0)
		{
			flag = deleteRear(&D);
			if (flag == -1)
				return 0;
		}

		else if (strcmp(order, "P") == 0)
		{
			print(&D);
		}
	}
	return 0;

}
```
