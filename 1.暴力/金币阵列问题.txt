有m*n枚金币在桌面上排成一个金币阵列。每一个金币正面朝上，或背面朝上，分别用0和1表示。         
金币阵列游戏的规则是：
（1）每次可将任一行金币翻过来放在原来的位置上；
（2）每次可任选2列，交换这2列金币的位置。         
给定金币的初始状态和目标状态，计算按金币游戏规则，将金币阵列从初始状态变换到目标状态所需的最少变换次数。

//自己最初的想法
#include<stdio.h>  
#include<malloc.h>
int main()  
{
	int m,n;//行数和列数 
	int i,j;
	int p,q;
	int **a,**b;
	int *c;
	int lie;
	int change = 0;//改变的次数 
	int temp;
	printf("请输入金币的行数和列数:\n");
	scanf("%d%d",&m,&n);
	a = (int **)malloc(sizeof(int *) * m);
	b = (int **)malloc(sizeof(int *) * m);
	c = (int *)malloc(sizeof(int) * n);
	for(i = 0;i < m;i ++){
		a[i] = (int *)malloc(sizeof(int) * n);
		b[i] = (int *)malloc(sizeof(int) * n);
	}
	printf("请输入原矩阵：\n");
	for(i = 0;i < m;i ++){
		for(j = 0;j < n;j ++){
			scanf("%d",&a[i][j]);
		}
	}
	printf("请输入目标矩阵矩阵：\n");
	for(i = 0;i < m;i ++){
		for(j = 0;j < n;j ++){
			scanf("%d",&b[i][j]);
		}
	}
	for(i = 0;i < m;i ++){
		lie = 0;
		for(j = 0;j < n;j ++){ 
			if(a[i][j] == b[i][j]){
				
			}
			else
			{
				c[lie] = j;
				lie ++;
			}
		}
		if(lie == n){
			for(p = 0;p < n;p ++){
				a[i][p] = (a[i][p] - 1) * (a[i][p] - 1);
			}
			change ++;
		}
		if(lie == 2){
			for(q = 0;q < m;q ++){
				temp = a[q][c[0]];
				a[q][c[0]] = a[q][c[1]];
				a[q][c[1]] = temp;
			}
			change ++;
		} 
	}
	if(change == 0){
		printf("无法通过变化得到！\n");
	}
	else{
		printf("%d\n",change);
	} 
	
	
	
	
	
	
	for(i = 0;i < m;i ++){
		for(j = 0;j < n;j ++){
			printf("%d ",a[i][j]);
		}
		printf("\n");
	}
	return 0;
}  
===================================================================
//老师的思路
#include<stdio.h>
#include<string.h>
#define m 4
#define n 3
int a[m][n] = {{1,0,1},{0,0,0},{1,1,0},{1,0,1}};
int b[m][n] = {{1,0,1},{1,1,1},{0,1,1},{1,0,1}};
int temp[m][n];
int count;
//对某一行进行反转，这里是第col行 
void trans1(int col){
	for(int i = 0;i < n;i ++)
		temp[col][i] = 1 - temp[col][i];
	count ++;
}
//交换第col1列和第col2列 
void trans2(int col1,int col2){
	int t;
	for(int i = 0;i < m;i ++){
		t = temp[i][col1];
		temp[i][col1] = temp[i][col2];
		temp[i][col2] = t;
	}
	if(col1 != col2)
		count ++;
}
//判断临时数组的第i列和目标数组的第j列是否相等 
bool same(int i,int j)
{
	bool flag = true;
	for(int k = 0;k < m;k ++)
	{
		if(temp[k][i] != b[k][i]){
			flag = false;
			return flag;
		}
	}
	return flag;
}
int main()
{
	int i,j,k;
	int answer = 999999;
	for(k = 0;k < n;k ++){
		count = 0;
		//数组复制
		for(i = 0;i < m;i ++){
			for(j = 0;j < n;j ++)
				temp[i][j] = a[i][j];
		}
		trans2(0,k);
		//比较第一列的所有元素，不相等就进行行变换 
		for(i = 0;i < m;i ++)
			if(temp[i][0] != b[i][0])
				trans1(i);
		bool found;
		//检查每一列是否满足条件 
		for(i = 0;i < n;i ++){
			found = false;
			if(same(i,i)){//第一个i是temp数组的，第二个是目标b数组的
				found = true;
				continue;			
			}
			for(j = i + 1;j < n;j ++)
				if(same(i,j)){
					trans2(i,j);
					found = true;
					break;
				}
			if(found == false)
				break;
		} 
		if(found == true)
			answer = count;
	} 
	if(answer != 999999)
	printf("%d",answer);
	
	return 0;
}
