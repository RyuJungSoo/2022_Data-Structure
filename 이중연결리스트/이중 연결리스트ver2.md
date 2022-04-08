# 이중 연결리스트ver2
![이중연결리스트 ver2](https://user-images.githubusercontent.com/81175672/162357585-e23b9ae0-3d67-4a8f-9ae9-a7207c408b4c.JPG)                                   
ver2 코드는 헤더 트레일러 이중연결리스트를 만들어 사용하는 코드이다. 필자는 연결리스트 실습문제 1번을 풀 때 이 방법을 사용했으며 **문제설명에서도 권하는 방법**이다.        
필자는 함수를 초기화할 때(init 함수) 헤더, 트레일러를 동적할당했으나 이 글에 있는 교수님 코드는 **main 함수**에서 헤더, 트레일러를 할당했다.        

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct DListNode
{
	char data;
	struct DListNode* prev, * next;

}DListNode;



void init(DListNode* H, DListNode*T)
{
	H->next = T;
	T->prev = H;
}


void insert(DListNode* H, int pos, char e)
{
	DListNode* p = H;
	for (int i = 1; i < pos; i++)
		p = p->next;

	DListNode* node = (DListNode*)malloc(sizeof(DListNode));
	node->data = e;
	node->prev = p;
	node->next = p->next;
	p->next->prev = node;
	p->next = node;
	
}

char delete(DListNode* H, int pos)
{
	DListNode* p = H;
	for (int i = 1; i <= pos; i++)
		p = p->next;
	
	char e = p->data;
	p->prev->next = p->next;
	p->next->prev = p->prev;
	free(p);
	return e;
}

void print(DListNode* H, DListNode *T)
{
	for (DListNode* p = H->next; p != T; p = p->next)
	{
		printf("[%c] <=> ", p->data);
		
	}
	printf("\b\b\b\b	\n");
}

int main()
{
	DListNode* H = (DListNode*)malloc(sizeof(DListNode));
	DListNode* T = (DListNode*)malloc(sizeof(DListNode));
	init(H,T);



	insert(H, 1, 'A'); print(H,T);
	insert(H, 1, 'B'); print(H,T);
	insert(H, 2, 'C'); print(H,T);
	insert(H, 4, 'D'); print(H,T);
	insert(H, 3, 'E'); print(H,T);
	getchar();

	printf("Node position : ");
	int pos;
	scanf("%d", &pos);
	printf("[%c] is deleted.\n", delete(H, pos));
	print(H, T);



	return 0;
}

```
