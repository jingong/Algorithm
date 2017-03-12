n个元素有n!个不同的排列。将这n!个不同的排列按字典序排列，并编号为0,1,2,…,n!-1。给定n个元素及一个排列，计算出这个排列的字典序值，同时给出字典序排列的下一个排列。
样例输入：
	8
	2 6 4 5 8 1 7 3 
样例输出：
	8227
	2 6 4 5 8 3 1 7



#include<stdio.h>
#define n 8 
int fact(int m){
	if(m == 0)
		return 1;
	return m * fact(m - 1);
}
int main()
{
	int a[n] = {2,6,4,5,8,1,7,3};
	int i,j;
	int count = 0;
	for(i = 0;i < n;i ++){
		count = count + (a[i] - 1) * fact(n - i - 1); 
		for(j = i + 1;j < n;j ++){//因为a[i]后面的数不能跟前面的重复，所以循环剪掉大于a[i]的数 
			if(a[j] > a[i]){
				a[j] --;
			}
			
		}
	}
	printf("%d",count);
	return 0;
}