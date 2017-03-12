#include<stdio.h>
#define n 8
int a[n][n];
int count = 1;
//col,row棋牌左上角的行号和列号
//td,tc特殊方格的行号和列号 
void checkboard(int col,int row,int td,int tc,int num){
	if(num == 1){
		return;
	}
	//左上 
	if(td < col + num / 2 && tc < row + num / 2){
		a[col + num / 2 - 1][row + num / 2] = count;
		a[col + num / 2][row + num / 2 - 1] = count;
		a[col + num / 2][row + num / 2] = count;
		
		count ++;
		
		checkboard(col,row,td,tc,num / 2);
		checkboard(col,row + num / 2,col + num / 2 - 1,row + num / 2,num / 2);
		checkboard(col + num / 2,row,col + num / 2,row + num / 2 - 1,num / 2);
		checkboard(col + num / 2,row + num / 2,col + num / 2,row + num / 2,num / 2);
	}
	//右上 
	if(td < col + num / 2 && tc > row + num / 2 - 1){
		a[col + num / 2 - 1][row + num / 2 - 1] = count;
		a[col + num / 2][row + num / 2 - 1] = count;
		a[col + num / 2][row + num / 2] = count;
		count ++;
		
		checkboard(col,row,col + num / 2 - 1,row + num / 2 - 1,num / 2);
		checkboard(col,row + num / 2,td,tc,num / 2);
		checkboard(col + num / 2,row,col + num / 2,row + num / 2 - 1,num / 2);
		checkboard(col + num / 2,row + num / 2,col + num / 2,row + num / 2,num / 2);
	}
	//左下 
	if(td > col + num / 2 - 1 && tc < row + num / 2){
		a[col + num / 2 - 1][row + num / 2 - 1] = count;
		a[col + num / 2 - 1][row + num / 2] = count;
		a[col + num / 2][row + num / 2] = count;
		count ++;
		
		checkboard(col,row,col + num / 2 - 1,row + num / 2 - 1,num / 2);
		checkboard(col,row + num / 2,col + num / 2 - 1,row + num / 2,num / 2);
		checkboard(col + num / 2,row,td,tc,num / 2);
		checkboard(col + num / 2,row + num / 2,col + num / 2,row + num / 2,num / 2);
	}
	//右下 
	if(td > col + num / 2 - 1 && tc > row + num / 2 - 1){
		a[col + num / 2 - 1][row + num / 2 - 1] = count;
		a[col + num / 2 - 1][row + num / 2] = count;
		a[col + num / 2][row + num / 2 - 1] = count;
		
		count ++;
		
		checkboard(col,row,col + num / 2 - 1,row + num / 2 - 1,num / 2);
		checkboard(col,row + num / 2,col + num / 2 - 1,row + num / 2,num / 2);
		checkboard(col + num / 2,row,col + num / 2,row + num / 2 - 1,num / 2);
		checkboard(col + num / 2,row + num / 2,td,tc,num / 2);
	}
} 
int main(){
	int i,j;
	a[0][1] = 0;
	checkboard(0,0,0,1,n);
	for(i = 0;i < n;i ++){
		for(j = 0;j < n;j ++){
			printf("%3d",a[i][j]);
		}
		putchar('\n');
	}
	return 0;
}