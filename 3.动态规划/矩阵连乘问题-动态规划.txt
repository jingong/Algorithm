给定n个矩阵，其中两个相邻的矩阵是可乘的，试求出最佳计算次序，使得总计算量最少。


#include<stdio.h>
#define n 6//矩阵的数量 
void recurMatrix(int *p,int **s,int **m)
{
	int i,j,k,r,t;
	for(i = 0;i < n + 1;i ++)
		m[i][i] = 0;
	for(r = 2;r <= n;r ++)
	{
		for(i = 1;i <= n + 1 - r;i ++)//运算的开始位置
		{
			j = i + r - 1;
			m[i][j] = m[i][i] + m[i + 1][j] + p[i - 1] * p[i] * p[j];//试探一次计算出值 
			s[i][j] = i;
			for(k = i + 1;k < j;k ++)//计算后续的值，并且比较大小，如果比试探的要小，更新s和m数组 
			{
				t = m[i][k] + m[k + 1][j] + p[i - 1] * p[k] * p[j];
				if(t < m[i][j])
				{
					m[i][j] = t;
					s[i][j] = k;
				}
			}		
		} 
	}
}
void traceback(int i,int j,int **s)
{
	if(i == j)
		return;
	traceback(i,s[i][j],s);
	traceback(s[i][j] + 1,j,s);
	printf("A[%d,%d] and A[%d,%d]\n",i,s[i][j],s[i][j] + 1,j);
}
int main()
{
	int i,j;
	int p[n + 1] = {30,35,15,5,10,20,25};//6个矩阵需要7个空间存储矩阵中所有的数据 
	int **s,**m;
	s = new int *[n + 1];//s中用于存放断开点的位置 
	m = new int *[n + 1];//m中用于存放每一层计算后所得到的最小的数，留于以后用到的时候直接拿出来 
	
	for(i = 0;i <= n;i ++){
		s[i] = new int[n + 1];
		m[i] = new int[n + 1];
	}
	recurMatrix(p,s,m);
	printf("%d\n",m[1][n]);
	traceback(1,n,s);
	return 0;
}