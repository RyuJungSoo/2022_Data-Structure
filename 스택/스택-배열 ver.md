```C
// 스택 - 배열로 풀기
// 듀플리케이트 - peek하고 push해도 되고 pop하고 두 번 push 해도 됨

#include <stdio.h>
#include <stdlib.h>

#define N 100

typedef struct  
{
	char data[N];
	int top;

}StackType;

void init(StackType* S)
{
	S->top = -1;
}

int isEmpty(StackType* S)
{
	return S->top == -1;
}

int isFull(StackType* S)
{
	return S->top == N - 1;
}

void push(StackType *S, char e)
{
	if (isFull(S))
	{
		printf("Stack Full\n");
	}

	else
	{
		S->top++;
		S->data[S->top] = e;
	}
}

char pop(StackType*S)
{
	if (isEmpty(S))
	{
		printf("Stack Empty\n");
		return -1;
	}
	
	char e = S->data[S->top];
	S->top--;
	return e;
}

char peek(StackType* S)
{
	if (isEmpty(S))
	{
		printf("Stack Empty\n");
		return -1;
	}

	return S->data[S->top];

}


void duplicate(StackType* S)
{
	char temp = peek(S);
	if (temp != -1)
		push(S, temp);
}

void upRotate(StackType* S, int n)
{
	int t = S->top;
	if (n <= t + 1)
	{
		char temp = S->data[t];
		for (int i = 1; i < n; i++)
		{
			S->data[t] = S->data[t - 1];
			t--;
		}
		S->data[t] = temp;
	}
}

void downRotate(StackType* S, int n)
{
	int t = S->top;
	if (n <= t + 1)
	{
		char temp = S->data[t - n + 1];
		for (int i = t - n + 1; i < t; i++)
			S->data[i] = S->data[i + 1];

		S->data[t] = temp;
	}
}

void print(StackType*S)
{
	for (int i = S->top; i >= 0; i--)
	{
		printf("%c", S->data[i]);
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
	getchar();

	upRotate(&S, 3);
	print(&S);
	getchar();

	duplicate(&S);
	print(&S);

	printf("POP: %c\n", pop(&S));
	print(&S);
	getchar();

	printf("PEEK: %c\n", peek(&S));
	print(&S);

	return 0;
}
```
