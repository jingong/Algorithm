//递归
#include<stdio.h>
#define n 5
int w[n] = {2,2,6,5,4};//表示每个物品的重量 
int v[n] = {6,3,5,4,6};//每个物品的价值 
int m(int i,int j)
{
	int a,b;
	if(i == n - 1)
	{
		if(j >= w[i])
			return v[i];
		else
			return 0;
	}
	if(j < w[i])
		return m(i + 1,j);
	a = m(i + 1,j - w[i]) + v[i];
	b = m(i + 1,j);
	return a > b ? a : b;
}
int main()
{
	int c = 10;
	printf("%d.",m(0,c));
	return 0; 
}
==========================================================
//备忘录
#include<stdio.h>
#define n 5
#define c 10
int w[n] = {2,2,6,5,4};//表示每个物品的重量 
int v[n] = {6,3,5,4,6};//每个物品的价值
int s[n][c + 1];
int m(int i,int j)
{
	int a,b;
	int result;
	if(s[i][j] >= 0)
		return s[i][j];
	if(i == n - 1)
	{
		if(j < w[i])
			result = 0;
		else
			result = v[i];
	}else if(j < w[i]){
		result = m(i + 1,j);
	}
	else{
		a = m(i + 1,j);
		b = m(i + 1,j - w[i]) + v[i];
		result = a > b ? a : b;
	} 
	s[i][j] = result;
	return result;
}
int main()
{
	int i,j;
	for(i = 0;i < n;i ++)
		for(j = 0;j <= c;j ++)
			s[i][j] = -1;
	printf("%d\n",m(0,c));
	j = c;
	for(i = 0;i < n - 1;i ++)//先输出前n-1个物品中哪个放入了包中 
	{
		if(s[i][j] != s[i + 1][j]){
			printf("%d\t",i);
			j = j - w[i];
		}		
	}
	if(j >= w[n - 1])//判断最后一个物品是否放入了包里 
		printf("%d\n",n - 1);
	return 0;
}
==========================================================================================
// 动态规划
#include<stdio.h>
#define n 5
#define c 10
int main()
{
	int i,j;
	int w[n] = {2,2,6,5,4};//表示每个物品的重量 
	int v[n] = {6,3,5,4,6};//每个物品的价值
	int s[n][c + 1];
	for(i = 0;i < n;i ++)
		for(j = 0;j <= c;j ++)
			s[i][j] = -1;
	for(j = 0;j <= c;j ++)
	{
		if(j < w[n - 1])
			s[n - 1][j] = 0;
		else{
			s[n - 1][j] = v[n - 1];
		}
	}
	for(i = n - 2;i >= 0;i --){
		for(j = 0;j <= c;j ++){
			if(j < w[i])
				s[i][j] = s[i + 1][j];
			else{
				int a = s[i + 1][j - w[i]] + v[i];
				int b = s[i + 1][j];
				s[i][j] = a > b ? a : b;
			}
		}	 
	}
	
	for(i = 0;i < n;i ++){
		for(j = 0;j <= c;j ++)
			printf("%3d",s[i][j]);
		putchar('\n');
	}
	printf("%d\n",s[0][c]);
	j = c;
	for(i = 0;i < n - 1;i ++)//先输出前n-1个物品中哪个放入了包中 
	{
		if(s[i][j] != s[i + 1][j]){
			printf("%d\t",i);
			j = j - w[i];
		}		
	}
	if(j >= w[n - 1])//判断最后一个物品是否放入了包里 
		printf("%d\n",n - 1);
	return 0;
} 