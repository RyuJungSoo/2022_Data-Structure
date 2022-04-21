```C
#include <stdio.h>

void rhanoi(int n, char from, char aux, char to)
{
	if (n == 1)
	{
		printf("move from %c to %c\n", from, to);
		return;
	}

	rhanoi(n - 1, from, to, aux);
	printf("move from %c to %c\n", from, to);
	rhanoi(n - 1, aux, from, to);
	
}

int main()
{
	int n;
	
	scanf("%d", &n);
	rhanoi(n, 'A', 'B', 'C');
	return 0;

}
```
