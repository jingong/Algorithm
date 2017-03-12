给定k个排好序的序列s1,s2,…,sk，用2路合并算法将这k个序列合并成一个序列。假设所采用的2路合并算法合并两个长度分别为m和n的序列需要m+n-1次比较。试设计一个算法确定合并这个序列的最优合并顺序，使所需要的总比较次数最少。


#include<stdio.h>
#define n 4
int min(int *a){
	int b[n];
	int i,j,k;
	int result = 0;
	int count = n;
	int temp;
	for(i = 0;i < n;i ++){
		b[i] = a[i];
	}
	
	while(count > 1){
		for(i = 0;i < count;i ++){
			for(j = i + 1;j < count;j ++){
				if(b[i] > b[j]){
					temp = b[i];b[i] = b[j];b[j] = temp;
				}
			}
		}	
		b[0] = b[1] + b[0];
		result += b[0] - 1;
		for(i = 1;i < count - 1;i ++){
			b[i] = b[i + 1];
		}
		count --;
	}
	return result;
}
int max(int *a){
	int b[n];
	int i,j,k;
	int result = 0;
	int count = n;
	int temp;
	for(i = 0;i < n;i ++){
		b[i] = a[i];
	}
	
	while(count > 1){
		for(i = 0;i < count;i ++){
			for(j = i + 1;j < count;j ++){
				if(b[i] < b[j]){
					temp = b[i];b[i] = b[j];b[j] = temp;
				}
			}
		}	
		b[0] = b[1] + b[0];
		result += b[0] - 1;
		for(i = 1;i < count - 1;i ++){
			b[i] = b[i + 1];
		}
		count --;
	}
	return result;
}
int main()
{
	int a[n] = {5,12,11,2};
	printf("the minimum is %d.",min(a));
	printf("the maximum is %d.",max(a));
	return 0;
} 