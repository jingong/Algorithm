给定含有 n 个元素的多重集合 S，每个元素在 S 中出现的次数称为该元素的重数。多重集S中重数最大的元素称为众数。例如，S={1,2,2,2,3,5}，其众数为2，其重数为3。
要求：对给定的 n 个自然数组成的多重集S，计算 S 的众数及其重数。
样例输入：
	6
	1
	2
	2
	2
	3
	5
样例输出：
	2
	3




#include<stdio.h>
#define n 8 
int num;
int largest = 1;
void sort(int a[]){//对数组进行排序 
	int i,j;
	int temp;
	for(i = 0;i < n;i ++){
		for(j = 0;j < n - i - 1;j ++){
			if(a[j + 1] < a[j]){
				temp = a[j];
				a[j] = a[j + 1];
				a[j + 1] = temp; 
			}
		}
	}
}
int compute(int a[],int left,int right){
	int mid = (left + right) / 2;
	int median = a[mid];
	int l1,r1;//mid左边的数记为l1,mid右边的数记为r1 
	l1 = r1 = mid;
	while(a[l1] == median)
		l1 --;
	while(a[r1] == median)
		r1 ++;
	if(r1 - l1 - 1 > largest){
		num = median;
		largest = r1 - l1 - 1;
	}
	if(l1 - left + 1 > largest){
		compute(a,left,l1);
	}
	if(right - r1 + 1 > largest){
		compute(a,r1,right);
	}
	return 0;
}
int main()
{
	int i;
	int a[n] = {1,2,3,3,4,3,3,5};
	sort(a);
	compute(a,0,n - 1);
	printf("%d %d",num,largest);
	putchar('\n');
	return 0;
}