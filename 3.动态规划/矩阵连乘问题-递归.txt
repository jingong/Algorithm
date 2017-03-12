#include<stdio.h>
#define n 6//矩阵的数量 
int **s;
int recurMatrix(int *p,int i,int j)
{
	int k;
	if(i == j)
		return 0;
	int u;
	u = recurMatrix(p,i,i) + recurMatrix(p,i + 1,j) + p[i - 1] * p[i] * p[j];
	s[i][j] = i;
	for(k = i + 1;k < j;k ++){
		int temp = recurMatrix(p,i,k) + recurMatrix(p,k + 1,j) + p[i - 1] * p[k] * p[j];
		if(temp < u)
		{
			u = temp;
			s[i][j] = k;
		}
	}
	return u;
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
	s = new int *[n + 1];
	
	for(i = 0;i <= n;i ++){
		s[i] = new int[n + 1];
	} 
	printf("%d\n",recurMatrix(p,1,n));
	traceback(1,n,s);
	return 0;
}