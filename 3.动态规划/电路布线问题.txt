制作电路板时，将n条连线分布到若干绝缘层上。在同一层的连线不相交。电路布线问题就是要确定将哪些连线安排到第一层上，使该层上有尽可能多的连线。


//递归
#include<stdio.h>
#define n 10
int p[n] = {7,6,3,1,4,0,8,2,9,5};
int f(int i,int j)
{
	int a,b;
	//i = 1的情况 
	if(i == 0)
	{
		if(j < p[i])
			return 0;
		else
			return 1;
	}
	//i > 1的情况 
	if(j < p[i])//j < p[i]说明当前的这跟接线接入会引起导线的交叉 
		return f(i - 1,j);
	a = f(i - 1,p[i] - 1) + 1;//导线接入的情况 
	b = f(i - 1,j);//导线不接入 
	return a > b ? a : b;//导线接入或者不接入，取两者的最优解 
}
int main()
{
	printf("%d.\n",f(n,n));
	return 0;	
} 
===========================================================================
//备忘录
#include<stdio.h>
#define n 10
int p[n] = {8,7,4,2,5,1,9,3,10,6};
//int p[n] = {7,6,3,1,4,0,8,2,9,5};
int s[n + 1][n + 1];
int f(int i,int j)
{
	int a,b;
	int result;
	if(s[i][j] > 0)
		return s[i][j];
	if(i == 1)
	{
		if(j < p[i])
			result = 0;
		else
			result = 1;
	}
	else
	{
		if(j < p[i])
			result = f(i - 1,j);
		else
		{
			a = f(i - 1,p[i] - 1) + 1;
			b = f(i - 1,j);
			result = a > b ? a : b;
		}
		
	}
	s[i][j] = result;
	return result;
}
int main()
{
	int i,j;
	for(i = 0;i < n + 1;i ++)
		for(j = 0;j < n + 1;j ++)
			s[i][j] = 0;
	printf("%d.\n",f(n,n));
	for(i = 0;i < n + 1;i ++)
	{
		for(j = 0;j < n + 1;j ++)
		{
			printf("%d\t",s[i][j]);
		}
		putchar('\n');
	}
	return 0;	
}
===========================================================================
//动态规划
#include<stdio.h>
#define n 10
int p[n + 1] = {0,8,7,4,2,5,1,9,3,10,6};
void traceback(int i,int j,int **s)
{
	if(i == 0)
		return;
	if(s[i][j] > s[i - 1][j])
	{
		printf("(%d,%d)\t",i,p[i]);
		traceback(i - 1,p[i] - 1,s);
	}
	else{
		traceback(i - 1,j,s);
	}
}
int main()
{
	int **s;
	int i,j;
	s = new int *[n + 1];
	for(i = 0;i < n + 1;i ++)
		s[i] = new int[n + 1];
	for(i = 0;i < n + 1;i ++)//对矩阵的第一行进行初始化 
	{
		if(i < p[1])
			s[0][i] = 0;//0代表不能接入 
		else
			s[0][i] = 1;//1代表能接入 
	} 
	for(i = 1;i < n + 1;i ++)
	{
		for(j = 0;j < n + 1;j ++)
		{
			if(j < p[i])
				s[i][j] = s[i - 1][j];
			else
			{
				s[i][j] = (s[i - 1][p[i] - 1] + 1) > s[i - 1][j] ? (s[i - 1][p[i] - 1] + 1) : s[i - 1][j];
			}	
		}	
	} 
	printf("%d.\n",s[n][n]);
	traceback(n,n,s);
	return 0;	
} 