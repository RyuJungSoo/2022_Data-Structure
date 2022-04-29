```C
// 스택 - 연결리스트로 푸는 법

#include <stdio.h>
#include <stdlib.h>


typedef struct StackNode
{
	char data;
	struct StackNode *next;

}StackNode;

typedef struct
{
	StackNode* top;
	int size;

}StackType;

void init(StackType* S)
{
	S->top = NULL;
	S->size = 0;
}

int isEmpty(StackType* S)
{
	return S->size == 0;
}


void push(StackType* S, char e)
{
	StackNode* node = (StackNode*)malloc(sizeof(StackNode));
	node->data = e;
	node->next = S->top;
	S->top = node;
	S->size++;

}

char pop(StackType* S)
{
	if (isEmpty(S))
	{
		printf("Stack Empty\n");
		return -1;
	}

	StackNode* p = S->top;
	char e = p->data;
	S->top = p->next;
	free(p);
	S->size--;
	return e;
}

char peek(StackType* S)
{
	if (isEmpty(S))
	{
		printf("Stack Empty\n");
		return -1;
	}

	return S->top->data;

}



void print(StackType* S)
{
	for (StackNode *p =S->top; p != NULL; p=p->next)
	{
		printf("%c", p->data);
	}
	printf("\n");
}

int main()
{
	StackType S;
	init(&S);

	pop(&S);
	getchar();

	push(&S, 'S');
	push(&S, 'T');
	push(&S, 'A');
	push(&S, 'R');
	print(&S);


	printf("POP: %c\n", pop(&S));
	print(&S);
	getchar();

	printf("PEEK: %c\n", peek(&S));
	print(&S);

	return 0;
}
```
