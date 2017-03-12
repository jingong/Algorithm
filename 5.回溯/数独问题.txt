//数独 
#include<stdio.h>
#define n 9
int a[n][n] = {
0,0,5,3,0,0,0,0,0,
8,0,0,0,0,0,0,2,0,
0,7,0,0,1,0,5,0,0,
4,0,0,0,0,5,3,0,0,
0,1,0,0,7,0,0,0,6,
0,0,3,2,0,0,0,8,0,
0,6,0,5,0,0,0,0,9,
0,0,4,0,0,0,0,3,0,
0,0,0,0,0,9,7,0,0
}; 
bool ok(int x,int y){
	int x0,y0;//m用来表示当前（x,y）所在的小的九宫格的左上角的坐标
	int i,j;
	//对行进行判断 
	for(i = 0;i < n;i ++){
		if(y != i && a[x][i] == a[x][y]){
			return false;
		}
	}
	//对列进行判断 
	for(i = 0;i < n;i ++){
		if(x != i && a[i][y] == a[x][y]){
			return false;
		}
	}
	x0 = x / 3 * 3;
	y0 = y / 3 * 3;
	//对小九宫格进行判断 
	for(i = x0;i < x0 + 3;i ++){
		for(j = y0;j < y0 + 3;j ++){
			if(a[i][j] == a[x][y] && x != i && y != j){
				return false;
			}
		}
	}
	return true;
}
void nfs(int t){
	int i,j;
	int x,y;
	if(t == n * n){
		for(i = 0;i < n;i ++){
			for(j = 0;j < n;j ++){
				printf("%d\t",a[i][j]);
			}
			putchar('\n');
		}
		return;
	}
	x = t / n;
	y = t % n;
	if(a[x][y] == 0){//应该先进行判断当前位置是否存在数，在不存在的时候再进行往下分支 
		for(i = 1;i <= n;i ++){
			a[x][y] = i;
			if(ok(x,y)){
				nfs(t + 1);	
			}
			a[x][y] = 0;
		}
	}else{
		nfs(t + 1);
	}
}
int main()
{
	nfs(0);
	return 0;	
}

===========================================================================================
//数独，以坐标为t的回溯 
#include<stdio.h>
#define n 9
int x0 = 0,y0 = 0,x1,y1;
int a[n][n] = {
0,0,5,3,0,0,0,0,0,
8,0,0,0,0,0,0,2,0,
0,7,0,0,1,0,5,0,0,
4,0,0,0,0,5,3,0,0,
0,1,0,0,7,0,0,0,6,
0,0,3,2,0,0,0,8,0,
0,6,0,5,0,0,0,0,9,
0,0,4,0,0,0,0,3,0,
0,0,0,0,0,9,7,0,0
}; 
int flag = 0;
bool ok(int x,int y){
	int x0,y0;//m用来表示当前（x,y）所在的小的九宫格的右上角的坐标
	int i,j;
	//对行进行判断 
	for(i = 0;i < n;i ++){
		if(y != i && a[x][i] == a[x][y]){
			return false;
		}
	}
	//对列进行判断 
	for(i = 0;i < n;i ++){
		if(x != i && a[i][y] == a[x][y]){
			return false;
		}
	}
	x0 = x / 3 * 3;
	y0 = y / 3 * 3;
	//对小九宫格进行判断 
	for(i = x0;i < x0 + 3;i ++){
		for(j = y0;j < y0 + 3;j ++){
			if(a[i][j] == a[x][y] && x != i && y != j){
				return false;
			}
		}
	}
	return true;
}
void nfs(int x,int y){//以列优先进行判断 
	int i,j;
	if(flag)
		return;
	if(a[x][y] != 0){//当前位置放数了 
		if(y == n - 1){//最后一列 
			if(x == n - 1){//最后一行 
				flag = 1;
				for(i = 0;i < n;i ++){
					for(j = 0;j < n;j ++){
						printf("%d\t",a[i][j]);
					}
					putchar('\n');
				}
				return;	
				
			}else{//到最后一列了，但是没有到最后一行 
				nfs(x + 1,y);
			}
		}else{//没有到最后一列 
			if(x == n - 1){//到最后一行 
				nfs(0,y + 1);
			}else{//没有到最后一行 
				nfs(x + 1,y);
			}
		} 
	}else{// 当前位置没有放数
		if(y == n - 1){//最后一列 
			if(x == n - 1){//最后一行 
				for(i = 1;i <= n;i ++){
					a[x][y] = i;
					if(ok(x,y)){//判断放进去的数是否符合条件 
						flag = 1;
						for(i = 0;i < n;i ++){
							for(j = 0;j < n;j ++){
								printf("%d\t",a[i][j]);
							}
							putchar('\n');
						}
						return;
					}
					a[x][y] = 0;
				}
			}else{//没有到最后一行 
				for(i = 1;i <= n;i ++){
					a[x][y] = i;
					if(ok(x,y)){
						nfs(x + 1,y);
					}
					a[x][y] = 0;
				}
			}
		}else{//不是最后一列 
			if(x == n - 1){//最后一行 
				for(i = 1;i <= n;i ++){
					a[x][y] = i;
					if(ok(x,y)){
						nfs(0,y + 1);
					}
					a[x][y] = 0;
				}
			}else{//不是最后一行 
				for(i = 1;i <= n;i ++){
					a[x][y] = i;
					if(ok(x,y)){
						nfs(x + 1,y);
					}
					a[x][y] = 0;
				}
			}
		}
	}
}
int main()
{
	nfs(x0,y0);
	return 0;	
} 