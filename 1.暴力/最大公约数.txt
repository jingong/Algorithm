#include<stdio.h>
int main()
{
	int a,b,c;
	printf("请输入两个整数:\n");
	scanf("%d%d",&a,&b);
	c = a % b;
	while(c != 0)
	{
		a = b;
		b = c;
		c = a % b;
	}
	printf("%d\n",b);
	return 0;
 }