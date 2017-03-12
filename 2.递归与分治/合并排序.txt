#include<stdio.h>
#define N 9
void merge(int a[],int b[],int left,int mid,int right)
{
	//合并排序，i=left也就是从数组的最左边出发，j从数组右半部份的最左边出发 
	int i = left,j = mid + 1,index = left;//index作为b数组的下标 
	while(i <= mid && j <= right){
		if(a[i] < a[j]) 
		{
			b[index] = a[i];
			index ++;
			i ++;
		}
		else{
			b[index] = a[j];
			index ++;
			j ++;
		}
	}
	//极端情况 
	if(i > mid)
	{
		for(int q = j;q <= right;q ++)
		{
			b[index] = a[q];
			k ++;
		}
	}
	else{
		for(int q = i;q <= mid;q ++)
		{
			b[index] = a[q];
			index ++;
		}
	}
}
void mergepass(int a[],int b[],int s,int n)
{
	int i = 0;
	int j;
	while(i <= n - 2 * s)
	{
		merge(a,b,i,i + s - 1,i + 2 * s - 1);
		i = i + 2 * s;
	}
	if(i + s < n)//(i + s - 1 < n - 1)
		merge(a,b,i,i + s - 1,n - 1);
	else
	{
		for(j = i;j <= n - 1;j ++)
			b[j] = a[j];
	}
}
void mergesort(int a[],int n)
{
	int b[n];
	int s = 1;
	while(s < n)
	{
		mergepass(a,b,s,n);
		s += s;
		mergepass(b,a,s,n);
		s += s;
	}
}
int main()
{
	int i;
	int a[N] = {4,5,2,6,8,1,3,9,7};
	mergesort(a,N);
	for(i = 0;i < N;i ++){
		printf("%d ",a[i]);
	}
	putchar('\n');
	return 0;
}