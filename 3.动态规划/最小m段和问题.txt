给定n个整数组成的序列，现在要求将序列分割为m段，每段子序列中的数在原序列中连续排列。如何分割才能使这m段子序列的和的最大值达到最小？
设f(i,j)表示将前i个数分成j段时，得到的最大最小值。则
f(i,j)=min{max{f(i,1)-f(k,1),f(k,j-1)}}
          1<=k<=i


#include<stdio.h>
#define n 9
#define m 3
int max(int p,int q){
	return p > q ? p : q;
}
int main()
{
	int i,j,k;
	int minvalue;
	int temp;
	int a[n + 1] = {0,9,8,7,6,5,4,3,2,1};
	int f[n + 1][m + 1];
	f[1][1] = a[1];
	for(i = 2;i < n + 1;i ++){
		f[i][1] = f[i - 1][1] + a[i]; 
	}
	for(i = 1;i <= n;i ++){
		for(j = 2;j <= m;j ++){
			minvalue = 100000000;
			for(k = 1;k < i;k ++){
				temp = max(f[k][j - 1],f[i][1] - f[k][1]);
				if(temp < minvalue){
					minvalue = temp;	
				}
			}
			f[i][j] = minvalue;
		}	
	}
	printf("the min is %d.",f[n][m]);
	return 0;	
} 