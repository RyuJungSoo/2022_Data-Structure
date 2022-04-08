# 이중 연결리스트ver3
![캡처0](https://user-images.githubusercontent.com/81175672/162357758-d2588b1d-12a4-4a23-b101-206bb3907140.JPG)

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct DListNode
{
	char data;
	struct DListNode* prev, * next;

}DListNode;

typedef struct
{
	DListNode* H;
	DListNode* T;


}DListType;


void init(DListType* DL)
{
	DL->H = DL->T = NULL;
	
}

void insertFirst(DListType* DL, char e)
{
	DListNode* node = (DListNode*)malloc(sizeof(DListNode));
	DListNode* p = DL->H;
	node->data = e;
	node->prev = node->next = NULL;

	if (p == NULL) // 첫번째 노드일때
		DL->H = DL->T = node;
	else
	{
		node->next = p;
		p->prev = node;
		DL->H = node;
	}

}

void insertLast(DListType* DL, char e)
{
	DListNode* node = (DListNode*)malloc(sizeof(DListNode));
	DListNode* p = DL->T;
	node->data = e;
	node->prev = node->next = NULL;

	if (p == NULL) // 첫번째 노드일때
		DL->H = DL->T = node;
	else
	{
		node->prev = p;
		p->next = node;
		DL->T = node;

	}

}

void insert(DListType* DL, int pos, char e)
{
	DListNode* node = (DListNode*)malloc(sizeof(DListNode));
	DListNode* p = DL->H;

	if (pos == 1)
		insertFirst(DL, e);
	else
	{
		for (int i = 1; i < pos - 1; i++)
		{
			p = p->next;
		}
		node->data = e;
		node->prev = p;
		node->next = p->next;

		if (p->next == NULL)
		{
			p->next = node;
			DL->T = node;
		}

		else
		{
			p->next->prev = node;
			p->next = node;
		}

	}
}

char deleteFirst(DListType* DL)
{
	DListNode* p = DL->H;
	char c = p->data;

	if (p->next == NULL)
	{
		DL->H = DL->T = NULL;
	}
	else
	{
		p->next->prev = NULL;
		DL->H = p->next;
	}
	free(p);
	return c;
}

char deleteLast(DListType* DL)
{
	DListNode* p = DL->T;
	char c = p->data;

	if (p->prev == NULL)
	{
		DL->H = DL->T = NULL;
	}
	else
	{
		p->prev->next = NULL;
		DL->T = p->prev;
	}
	free(p);
	return c;
}

char delete(DListType* DL, int pos)
{
	DListNode* p = DL -> H;
	char c;

	if (pos == 1)
		c = deleteFirst(DL);
	else
	{
		for (int i = 1; i < pos; i++)
			p = p->next;
		if (p->next == NULL)
			c = deleteLast(DL);
		else
		{
			c = p->data;
			p->prev->next = p->next;
			p->next->prev = p->prev;
			free(p);
		}
	}
	return c;

}

void printForward(DListType*DL)
{
	for (DListNode* p = DL->H; p != NULL; p = p->next)
	{
		printf("[%c] <=> ", p->data);
	}
	printf("\b\b\b\b	\n");
}

void printBackward(DListType* DL)
{
	for (DListNode* p = DL->T; p != NULL; p = p->prev)
	{
		printf("[%c] <=> ", p->data);
	}
	printf("\b\b\b\b	\n");
}

int main()
{
	DListType DL;
	init(&DL);

	insertFirst(&DL, 'A'); insertLast(&DL, 'B');
	insertLast(&DL, 'C'); insertFirst(&DL, 'D');
	printForward(&DL); printBackward(&DL);
	getchar();

	insert(&DL, 2, 'E'); insert(&DL, 4, 'F'); insert(&DL, 1, 'G');
	printForward(&DL); 

	deleteFirst(&DL); deleteLast(&DL); printForward(&DL); getchar();

	return 0;
}

```
