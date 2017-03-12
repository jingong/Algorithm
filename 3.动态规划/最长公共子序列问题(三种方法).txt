一个给定序列的子序列是在该序列中删去若干元素后得到的序列。
问题：给定两个序列X和Y，找出二者的最长公共子序列。



//递归
#include<stdio.h>
#include<string.h>
int s(char *x,char *y,int m,int n)
{
	int a,b;
	if(m < 0 || n < 0)
		return 0;
	if(x[m] == y[n])
		return s(x,y,m - 1,n - 1) + 1;
	a = s(x,y,m - 1,n);
	b = s(x,y,m,n - 1);
	return a > b ? a : b;
}
int main()
{
	char *x = "abcbdab";
	char *y = "bcdb";
	int lenx = strlen(x);
	int leny = strlen(y);
	
	printf("%d\n",s(x,y,lenx - 1,leny - 1));
	return 0;	
}
==========================================================================
//备忘录
#include<stdio.h>
#include<string.h>
char *x = "abcbdab",*y = "bdcaba";
int **s;
int f(int m,int n)
{
	int a,b;
	int result;
	if(m == 0 || n == 0)
		return 0;
	if(s[m][n] > 0)
		return s[m][n];
	if(x[m - 1] == y[n - 1])
		result =  f(m - 1,n - 1) + 1;
	else{
		a = f(m - 1,n);
		b = f(m,n - 1);
		result = a > b ? a : b;
	}
	s[m][n] = result;
	return result;
}
int main()
{
	int i,j;
	int lenx = strlen(x);
	int leny = strlen(y);
	//申请数组 
	s = new int *[lenx + 1];
	for(i = 0;i < lenx + 1;i ++)
		s[i] = new int[leny + 1];
	//把数组的所有元素都给赋初值为0 
	for(i = 0;i < lenx + 1;i ++)
		for(j = 0;j < leny + 1;j ++)
			s[i][j] = 0;
	
	printf("%d\n",f(lenx,leny));
	for(i = 0;i < lenx + 1;i ++)
	{
		for(j = 0;j < leny + 1;j ++)
			printf("%d ",s[i][j]);
		putchar('\n');
	}	
	return 0;	
} 
==================================================================================
//动态规划
#include<stdio.h>
#include<string.h>
void traceback(int m,int n,char *x,int **b)
{
	switch(b[m][n])
	{
		case 1:
			traceback(m - 1,n - 1,x,b);
			printf("%c",x[m - 1]);
			break;
		case 2:
			traceback(m - 1,n,x,b);
			break;
		case 3:
			traceback(m,n - 1,x,b);
			break;
	}
}
int main()
{
	int i,j;
	char *x = "abcbdab",*y = "bdcaba";
	int **s;
	int **b;
	int lenx = strlen(x);
	int leny = strlen(y);
	//申请数组 
	s = new int *[lenx + 1];
	b = new int *[lenx + 1];
	for(i = 0;i < lenx + 1;i ++)
	{
		s[i] = new int[leny + 1];
		b[i] = new int[leny + 1];
	}
	for(i = 0;i < lenx + 1;i ++)
		s[i][0] = 0;
	for(i = 0;i < leny + 1;i ++)
		s[0][i] = 0;
	for(i = 1;i <= lenx;i ++)
		for(j = 1;j <= leny;j ++)
		{
			if(x[i] == y[j])
			{
				s[i][j] = s[i - 1][j - 1] + 1;
				b[i][j] = 1;
			}
			else{
				if(s[i - 1][j] > s[i][j - 1])
				{
					s[i][j] = s[i - 1][j];
					b[i][j] = 2;
				}
				else{
					s[i][j] = s[i][j - 1];
					b[i][j] = 3;
				}
			}
		}
	printf("%d.\n",s[lenx][leny]);
	traceback(lenx,leny,x,b);
	return 0;	
} 