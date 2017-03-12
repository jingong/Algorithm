在n*n的棋盘上放置彼此不受攻击的n个皇后，按照国际象棋的规则，皇后可以攻击与之处在同一行或同一列或同一斜线上的棋子。n后问题等价于在n*n格的棋盘上放置n个皇后，任何2个皇后不放在同一行或同一列或同一斜线上。




//n皇后问题 （暴力）
#include<stdio.h>
#include<math.h>
#define n 8 
int judge(int *a){
	int i,j;
	for(i = 0;i < n;i ++){
		for(j = i + 1;j < n;j ++){
			if(a[i] == a[j] || abs(i - j) == abs(a[i] - a[j])){
				return 0;
			}
		}
	}
	return 1;
}
int main()
{
	int i,j,k;
	int num;
	int temp;
	int a[n];
	int flag;
	int count = 0;
	for(num = 0;num < pow(n,n);num ++){
		temp = num;
		for(i = 0;i < n;i ++){
			a[i] = temp % n;
			temp /= n;
		}
		if(judge(a)){
			for(i = 0;i < n;i ++){
				printf("%d ",a[i]);
			}
			putchar('\n');
			count ++;
		}
	}
	printf("%d.\n",count);
	return 0; 
}
===========================================================================
//n皇后问题 （回溯）
#include<stdio.h>
#include<math.h>
#define n 8
int count = 0;
int a[n];
int judge(int t){//t表示0~t这个区间上没有发生重复，也就是满足游戏规则 
	int i,j;
	for(i = 0;i <= t;i ++){
		for(j = i + 1;j <= t;j ++){
			if(a[i] == a[j] || abs(i - j) == abs(a[i] - a[j])){
				return 0;
			}
		}
	}
	return 1;
}
void nfs(int m){
	int i;
	if(m == n){
		count ++;
		return;
	}
	for(i = 0;i < n;i ++){
		a[m] = i;
		if(judge(m)){
			nfs(m + 1);
		}
	}
}
int main()
{
	nfs(0);
	printf("%d.\n",count);
	return 0; 
}
