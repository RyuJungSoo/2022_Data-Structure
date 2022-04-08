# 이중 연결리스트ver1

![이중연결리스트 ver1](https://user-images.githubusercontent.com/81175672/162357166-bb2cd156-6f62-485d-bd0c-f0b48ed750e4.JPG)                   
ver1 코드는 단일 연결리스트에서 한 방식처럼 연결리스트의 맨 앞을 가리키는 **H**를 따로 지정하고 따로 **포인터 p**를 선언해 초기 위치를 H로 지정하고 p의 포인터 값을 계속 다음으로 옮겨가면서 원소값에 접근하는 코드이다.

```C
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
	DL->H = NULL;
}

void insertFirst(DListType* DL, char e)
{
	DListNode* node = (DListNode*)malloc(sizeof(DListNode));
	DListNode* p = DL->H;
	node->data = e;
	node->prev = NULL;
	node->next = p;
	DL->H = node;

	if (p != NULL) // 기존에 연결된 노드가 있다면
		p->prev = node;

}

void insert(DListType* DL, int pos, char e)
{
	DListNode* node = (DListNode*)malloc(sizeof(DListNode));
	DListNode* p = DL->H;

	if (pos == 1)
		insertFirst(DL, e);
	else
	{
		for (int i = 1; i < pos; i++)
			p = p->next;
		node->data = e;
		node->prev = p->prev;
		node->next = p;

		node->prev->next = node;
		// 또는 p->prev->next = node;
		p->prev = node;
	}
}

void print(DListType* DL)
{
	DListNode* p;
	for (p = DL->H; p != NULL; p=p->next)
		printf("[%c] <=> ", p->data);
	printf("\b\b\b\b	\n");
}

int main()
{
	DListType DL;
	init(&DL);

	insertFirst(&DL, 'A'); print(&DL);
	insertFirst(&DL, 'B'); print(&DL);
	insertFirst(&DL, 'C'); print(&DL);
	getchar();

	insert(&DL, 2, 'D'); print(&DL);
	insert(&DL, 1, 'E'); print(&DL);
	insert(&DL, 3, 'F'); print(&DL);


	return 0;
}
```
