```C
#include <stdio.h>
#include <stdlib.h>

typedef struct ListNode
{
	int elem;
	struct ListNode* next,*prev;


}ListNode;

typedef struct
{
	ListNode* H,*T;
}ListType;

void init(ListType* L)
{
	ListNode* header, * trailer;
	header = (ListNode*)malloc(sizeof(ListNode));
	trailer = (ListNode*)malloc(sizeof(ListNode));

	header->next = trailer;
	trailer->prev = header;

	L->H = header;
	L->T = trailer;

}

void addLast(ListType* L, int elem)
{
	ListNode* node,*p =L->T;
	node = (ListNode*)malloc(sizeof(ListNode));
	node->elem = elem;

	if (L->H->next == L->T)
	{
		node->next = L->T;
		node->prev = L->H;
		L->H->next = node;
		L->T->prev = node;

	}

	else
	{
		node->next = p;
		node->prev = p->prev;
		p->prev->next = node;
		p->prev = node;
	}
}

int member(ListType* L, int e)
{
	ListNode* p;
	int a;

	if (L->H->next == L->T)
		return 0;

	p = L->H->next;

	while (1)
	{
		a = p->elem;
		if (a < e)
		{
			if (p->next == L->T)
				return 0;
			else
				p = p->next;
		}

		else if (a > e)
			return 0;

		else
			return 1;
	}

}

int subset(ListType* A, ListType* B)
{
	ListNode* p;

	if (A->H->next == A->T)
		return 0;

	p = A->H->next;



	while (1)
	{

		if (member(B, p->elem))
		{


			if (p->next == A->T)
				return 0;
			else
			{
				p = p->next;

			}

		}

		else
		{
			return p->elem;
		}
	}

}

void print(ListType* L)
{
	ListNode* p;

	for (p = L->H->next; p != L->T; p = p->next)
		printf(" %d",p->elem);
	printf("\n");

}

int main()
{
	ListType A, B;
	int cnt1, cnt2, num, i;
	init(&A); init(&B);

	scanf("%d", &cnt1);
	for (i = 0; i < cnt1; i++)
	{
		scanf("%d", &num);
		addLast(&A, num);
	}


	scanf("%d", &cnt2);
	for (i = 0; i < cnt2; i++)
	{
		scanf("%d", &num);
		addLast(&B, num);
	}

	printf("%d\n", subset(&A, &B));
	return 0;

}
```
