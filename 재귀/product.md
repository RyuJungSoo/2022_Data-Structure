```C
#include <stdio.h>

int product(int a, int b)
{
	if (b == 1)
		return a;

	else
		return a + product(a,b - 1);
}

int main()
{
	int a, b;

	scanf("%d %d", &a, &b);

	printf("%d\n",product(a, b));
	return 0;
}
```
