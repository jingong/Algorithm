//备忘录算法 
#include<stdio.h>
#define n 6//矩阵的数量 
int recurMatrix(int *p,int i,int j,int **s,int **m)
{
	int k;
	int minValue;
	if(m[i][j] > 0){
		return m[i][j];
	}
	if(i == j)
		return 0;	
	minValue = recurMatrix(p,i,i,s,m) + recurMatrix(p,i + 1,j,s,m) + p[i - 1] * p[i] * p[j];
	s[i][j] = i;
	for(k = i + 1;k < j;k ++){
		int temp = recurMatrix(p,i,k,s,m) + recurMatrix(p,k + 1,j,s,m) + p[i - 1] * p[k] * p[j];
		if(temp < minValue)
		{
			minValue = temp;
			s[i][j] = k;
		}
	}
	m[i][j] = minValue;
	return minValue;
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
	for(i = 1;i <= n;i ++)
		for(j = i;j <= n;j ++)//只存在由低到高的记录，不存放由高到低的记录，所以不用全部赋值 
			m[i][j] = 0;
	printf("%d\n",recurMatrix(p,1,n,s,m));
	traceback(1,n,s);
	return 0;
}