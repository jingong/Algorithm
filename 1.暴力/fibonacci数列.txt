#include<stdio.h>
int f(int n)
{
    if (n == 1 || n == 2) 
        return 1;
    else
        return f(n-1)+f(n-2);
}

int main()
{
	int num;
	num = f(20);
	printf("%d",num);
	return 0;
}