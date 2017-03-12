#include<stdio.h>
#define n 9
int partition(int a[],int left,int right)
{
	int num = a[left];
	int i,j;
	int temp;
	i = left + 1;
	j = right;
	while(i < j){
		while(a[i] <= num && i <= right)
			i ++;
		while(a[j] > num)
			j --;
		if(i < j){
			temp = a[i];
			a[i] = a[j];
			a[j] = temp;
		}
	}
	a[left] = a[j];
	a[j] = num;
	return j;
}
void quicksort(int a[],int left,int right)
{
	int pos;
	if(left < right)
	{
		pos = partition(a,left,right);
		quicksort(a,left,pos - 1);
		quicksort(a,pos + 1,right);
	}
}
int main(){
	int i;
	int a[n] = {4,5,2,6,8,1,3,9,7};
	quicksort(a,0,n - 1);
	for(i = 0;i < n;i ++){
		printf("%d ",a[i]);
	}
	putchar('\n');
	return 0;
}