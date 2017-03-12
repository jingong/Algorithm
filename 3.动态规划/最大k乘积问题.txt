设I是一个n位十进制整数。如果将I分割为k段，则可得到k个整数。这k个整数的乘积称为I的一个k乘积。试设计一个算法，对于给定的I和k，求出I的最大k乘积。
设w[i][j]表示从第i位到第j位的数字表示的整数，m[i][j]表示前i位分成j段所得到的最大乘积，则
m[i][1] = w[1][i]
m[i][j] = max{m[d][j-1] * w[d+1][i]};
	1<=d<=i



#include<stdio.h>
#include<math.h>
int main()
{
	int num,c;
	int i,j,k,d;
	int n;
	int **m,**w;
	int *a;
	int temp;
	int f;
	int max;
	printf("please input the num of num and c:\n");
	scanf("%d%d",&num,&c);
	n = log10(num) + 1;
	a = new int[n + 1];
	m = new int *[n + 1];
	w = new int *[n + 1];
	for(i = 0;i < n + 1;i ++){
		m[i] = new int[c + 1];
		w[i] = new int[n + 1];
	}
	temp = num;
	i = 0;
	while(i < n){
		a[n - i] = temp % 10;
		temp /= 10;
		i ++;
	}
	//对w[][]打底 
	for(i = 1;i <= n;i ++){
		w[i][i] = a[i];
	}
	for(i = 1;i <= n;i ++){
		for(j = i + 1;j <= n;j ++){
			w[i][j] = w[i][j - 1] * 10 + a[j];
		}
	}
	//对m[][]打底
	for(i = 1;i <= n;i ++){
		m[i][1] = w[1][i];
	}
	
	//m[i][j]表示把前i个分成j段 
	for(i = 2;i <= n;i ++){	
		for(j = 2;j <= c;j ++){
			max = 0;
			for(d = 1;d < i;d ++){//用d控制 m[i][j]的不同情况 
				temp = m[d][j - 1] * w[d + 1][i];
				if(temp > max){
					max = temp;
				} 
			}
			m[i][j] = max;
		}
	}
	printf("the max is %d.",m[n][c]);
	return 0;
} 