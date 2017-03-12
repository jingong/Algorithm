//如何对一组数实现全排列
#include<stdio.h>
#define n 3
void perm(int *b,int t){
	int i,j,k;
	int temp;
	if(t == n){
		for(i = 0;i < n;i ++){
			printf("%d ",b[i]);
		}
		putchar('\n');
		return;
	}
	for(i = t;i < n;i ++){
		temp = b[i];b[i] = b[t];b[t] = temp;
		perm(b,t + 1);
		temp = b[i];b[i] = b[t];b[t] = temp;
	}
}
int main()
{
	int a[n] = {1,2,3};
	perm(a,0);
	return 0;	
}
==================================================================
//批处理作业调度（回溯）
#include<stdio.h>
#define n 3//作业的数量 
#define s 2//机器数
int M[n + 1][s] = {{0,0},{2,1},{3,1},{2,3}}; //申请一个(n + 1) * s的矩阵，这里为了方便读取和理解，第一行空出来
int x[n + 1];//借助此数组实现对n个作业的全排列 
int bestx[n + 1];//用于保存最佳的作业调度方案 
int best=100000;//保存最少的作业调度时间 
int f1 = 0,f2[n + 1] = {0};//f1表示0`t作业在机器1上所用的时间，f2数组用于保存每一个作业的在机器2上的结束时间
int temp; 
int f = 0;
void nfs(int t){
	int i;
	if(t == n + 1){	
		if(best > f){
			for(i = 1;i <= n;i ++)
				bestx[i] = x[i];
			best = f;
		}	
		return;
	}
	if(f < best){
		for(i = t;i <= n;i ++){//x的全排列 
			f1 += M[x[i]][0];
			f2[t] = (f2[t - 1] > f1 ? f2[t - 1] : f1) + M[x[i]][1];
			f += f2[t];
			temp = x[i];x[i] = x[t];x[t] = temp;
			nfs(t + 1);
			temp = x[i];x[i] = x[t];x[t] = temp;
			f -= f2[t];
			f1 -= M[x[i]][0];	
		}	
	} 
	
}
int main()
{
	int i;
	for(i = 1;i <= n;i ++){
		x[i] = i;
	}
	nfs(1);
	for(i = 1;i <= n;i ++){
		printf("%d ",bestx[i]);
	}
	putchar('\n');
	printf("%d",best);
	return 0;	
} 