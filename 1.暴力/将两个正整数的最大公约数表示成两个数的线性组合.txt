#include<stdio.h>
int main()
{
	int a,b,c;
	int m,n;
	printf("请输入两个整数:\n");
	scanf("%d%d",&a,&b);
	m = a;
	n = b;
	c = a % b;
	while(c != 0)
	{
		a = b;
		b = c;
		c = a % b;
	}
	for(int i = 1;i <= b;i ++)
		for(int j = 1;j <= a;j ++)
		{
			if((m * i - n * j) == b) 
				printf("%d*%d-%d*%d = %d\n",m,i,n,j,b);	
			if((n * j - m * i) == b)
				printf("%d*%d-%d*%d = %d\n",n,j,m,i,b);
		} 
	printf("%d\n",b);
	return 0;
} 
