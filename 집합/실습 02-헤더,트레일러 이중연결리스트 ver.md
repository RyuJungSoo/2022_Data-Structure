```C
#include <stdio.h>
#include <stdlib.h>

typedef struct ListNode
{
	int elem;
	struct ListNode* next, * prev;
	
}ListNode;

typedef struct
{
	ListNode* H, * T;
	

}ListType;

void init(ListType* L)
{
	ListNode* header, * trailer;

	header = (ListNode*)malloc(sizeof(ListNode));
	trailer = (ListNode*)malloc(sizeof(ListNode));

	header->prev = NULL;
	header->next = trailer;
	trailer->next = NULL;
	trailer->prev = header;

	L->H = header;
	L->T = trailer;
}

void addLast(ListNode* L, int elem)
{
	ListNode* node, * p;
	node = (ListNode*)malloc(sizeof(ListNode));
	node->elem = elem;

	if (L->next->next == NULL)
	{
		node->next = L->next;
		node->prev = L;

		L->next->prev = node;
		L->next = node;
		
	}

	else
	{
		p = L;
		for (; p->next != NULL; )
			p = p->next;

		node->next = p;
		node->prev = p->prev;

		p->prev->next = node;
		p->prev = node;
	}

}

ListNode* unionSet(ListType* A, ListType* B)
{
	ListNode *p1,*p2;

	ListNode* header, * trailer;

	header = (ListNode*)malloc(sizeof(ListNode));
	trailer = (ListNode*)malloc(sizeof(ListNode));

	header->prev = NULL;
	header->next = trailer;
	trailer->next = NULL;
	trailer->prev = header;

	

	p1 = A->H->next;
	p2 = B->H->next;

	while (p1 != A->T && p2 != B->T)
	{
		if (p1->elem < p2->elem)
		{
			addLast(header, p1->elem);
			p1 = p1->next;
		}

		else if (p1->elem > p2->elem)
		{
			addLast(header, p2->elem);
			p2 = p2->next;
		}

		else
		{
			addLast(header, p1->elem);
			p1 = p1->next;
			p2 = p2->next;
		}

	}

	while (p1 != A->T)
	{
		addLast(header, p1->elem);
		p1 = p1->next;
	}

	while (p2 != B->T)
	{
		addLast(header, p2->elem);
		p2 = p2->next;
	}
	return header;
}


ListNode* intersectSet(ListType* A, ListType* B)
{
	ListNode* p1, * p2;

	ListNode* header, * trailer;

	header = (ListNode*)malloc(sizeof(ListNode));
	trailer = (ListNode*)malloc(sizeof(ListNode));

	header->prev = NULL;
	header->next = trailer;
	trailer->next = NULL;
	trailer->prev = header;



	p1 = A->H->next;
	p2 = B->H->next;

	while (p1 != A->T && p2 != B->T)
	{
		if (p1->elem < p2->elem)
		{
			
			p1 = p1->next;
		}

		else if (p1->elem > p2->elem)
		{
			
			p2 = p2->next;
		}

		else
		{
			addLast(header, p1->elem);
			p1 = p1->next;
			p2 = p2->next;
		}

	}

	while (p1 != A->T)
	{
	
		p1 = p1->next;
	}

	while (p2 != B->T)
	{
		
		p2 = p2->next;
	}
	return header;

}

void print(ListNode* L)
{
	ListNode* p;
	int cnt = 0;


	for (p = L->next; p->next != NULL; p = p->next)
	{
		printf(" %d", p->elem);
		cnt++;
	}
	
	if (cnt == 0)
		printf(" 0");
	printf("\n");

}

int main()
{
	ListType A, B;
	int cnt1, cnt2, i, num;
	init(&A); init(&B);

	scanf("%d", &cnt1);
	for (i = 0; i < cnt1; i++)
	{
		scanf("%d", &num);
		addLast(A.H, num);
	}


	scanf("%d", &cnt2);
	for (i = 0; i < cnt2; i++)
	{
		scanf("%d", &num);
		addLast(B.H, num);
	}
	
	print(unionSet(&A, &B));
	print(intersectSet(&A, &B));
	
	return 0;
} 

```
