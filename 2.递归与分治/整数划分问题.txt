将正整数 n 划分为一系列正整数的和： 
n = n1 + n2 + ... + nk
正整数的这种表示称为正整数 n 的划分。不同划分的个数称为正整数 n 的划分数，记为 p(n)。
6=6
6=5+1
6=4+2=4+1+1
6=3+3=3+2+1=3+1+1+1
6=2+2+2=2+2+1+1=2+1+1+1+1
6=1+1+1+1+1+1+1




//法一
#include<stdio.h>
int q(int n,int m){
	if(m == 1 || n == 1){
		return 1;
	}
	if(m > n){
		return q(n,n);
	}
	if(m == n){
		return 1 + q(n,m - 1);
	}
	return q(n,m - 1) + q(n - m,m); 
}
int main()
{
	int n = 6;
	printf("%d",q(6,6)); 
	
	return 0;
}

//法二
#include<stdio.h>
#define n 7
int main()
{
	int *coef = new int[n];
	int *temp = new int[n];
	int i,j,k;
	for(i = 0;i < n;i ++){
		coef[i] = 1;
		temp[i] = 0;
	}
	for(k = 2;k <= n;k ++){
		for(i = 0;i < n + 1;i ++){
			for(j = 0;j < n + 1;j += k){
				if(i + j <= (n - 1)){
					temp[i + j] = temp[i + j] + coef[i];
				}
			}		
		}
		for(int i = 0;i < n + 1;i ++){
				coef[i] = temp[i];
				temp[i] = 0;
		}
	}
	printf("%d",coef[6]);
	return 0;
}