```C
#include <stdio.h>

int quotient(int a, int b)
{
	if (a < b)
		return 0;

	else
		return 1+quotient(a-b,b);
}

int main()
{
	int a, b;

	scanf("%d %d", &a, &b);

	printf("%d\n",quotient(a, b));
	return 0;
}
```
