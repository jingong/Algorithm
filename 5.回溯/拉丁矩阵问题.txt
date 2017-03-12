现有n种不同形状的宝石，每种宝石有足够多颗。欲将这些宝石排列成m行n列的一个矩阵，m<=n，使矩阵中每一行和每一列的宝石都没有相同的形状。试设计一个算法，计算出对于给定的m和n，有多少种不同的宝石排列方案。



#include<stdio.h>
#define m 3
#define n 3
int a[m][n];
int count = 0;
bool ok(int x,int y){
	int i;
	for(i = 0;i < x;i ++){
		if(a[i][y] == a[x][y]){
			return false;
		}
	}
	return true;
}
void nfs(int x,int y){//用xy表示走到第几行第几列了 
	int i;
	int temp;
	for(i = y;i < n;i ++){
		temp = a[x][y];
		a[x][y] = a[x][i];
		a[x][i] = temp;
		
		if(ok(x,y)){//因为每一行的数都是0~n-1,所以行上不会重复，只需要在列上判断每一列是否出现了相同的元素，有相同的则需要停止当前分支 
			if(x == m - 1){
				if(y == n - 1){
					count ++;
					return;
				}else{
					nfs(x,y + 1);
				}
			} else{
				if(y == n - 1){
					nfs(x + 1,0);
				}else{
					nfs(x,y + 1);
				}
			}
		}
		
		temp = a[x][y];
		a[x][y] = a[x][i];
		a[x][i] = temp; 
	}
}
int main()
{
	int i,j;
	for(i = 0;i < m;i ++){
		for(j = 0;j < n;j ++){
			a[i][j] = j + 1;
		}
	}
	nfs(0,0);
	printf("%d\n",count);
	return 0;	
} 