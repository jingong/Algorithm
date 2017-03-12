#include<stdio.h>
#define n 3
void perm(int a[],int begin,int end)
{
	int t;
	if(begin == end)
	{
		for(int i = 0;i < n;i ++)
			printf("%d ",a[i]);
		putchar('\n');
	}
	else{
		for(int i = begin;i < n;i ++){
			t = a[begin];a[begin] = a[i];a[i] = t;
			perm(a,begin + 1,end);
			t = a[begin];a[begin] = a[i];a[i] = t;
		}
	}
}
int main()
{
	int a[n] = {1,2,3};
	perm(a,0,2);
	return 0;
}