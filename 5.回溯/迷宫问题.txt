给定一个m × n (m行, n列)的迷宫，迷宫中有两个位置，gloria想从迷宫的一个位置走到另外一个位置，当然迷宫中有些地方是空地，gloria可以穿越，有些地方是障碍，她必须绕行，从迷宫的一个位置，只能走到与它相邻的4个位置中，当然在行走过程中，gloria不能走到迷宫外面去。令人头痛的是，gloria是个没什么方向感的人，因此，她在行走过程中，不能转太多弯了，否则她会晕倒的。我们假定给定的两个位置都是空地，初始时，gloria所面向的方向未定，她可以选择4个方向的任何一个出发，而不算成一次转弯。gloria能从一个位置走到另外一个位置吗？ 



#include<stdio.h>
#define m 5
#define n 5
int x0 = 0,y0 = 0,x1 = 2,y1 = 0;
int olddir = 0;//老方向 
int change = 0;
int max = 2;
int flag = 0;
char maze[m][n] = {
'.','.','.','*','*',
'*','.','*','*','*',
'.','.','.','.','.',
'.','.','.','.','.',
'*','.','.','.','.'
};
int a[m][2] = {0,0,-1,0,1,0,0,-1,0,1};//定义数组保存可以选择的方法 
bool ok(int x,int y){
	if(x < 0 || x >= m || y < 0 || y >= n || maze[x][y] == '*'){
		return false;
	}
	return true;
}

void nfs(int x,int y){
	int d;
	int temp;
	if(x == x1 && y == y1){
		flag = 1;
		return;
	}
	if(change <= max){//在这里要注意对程序进行剪枝，要不然会死掉 
		for(d = 1;d <= 4;d ++){
			x += a[d][0];
			y += a[d][1];
			temp = olddir;
			if(ok(x,y)){
				if(d != olddir){//如果和老的方向不一样新的方向说明拐弯了 
					change ++;
				}
				olddir = d;
				nfs(x,y);
				olddir = temp;
				if(d != olddir){
					change --;
				}
			}
			x -= a[d][0];
			y -= a[d][1];
		}	
	}
	
}
int main()
{
	nfs(0,0);
	if(flag)
		printf("yes\n");
	else
		printf("no\n");
	return 0;
}