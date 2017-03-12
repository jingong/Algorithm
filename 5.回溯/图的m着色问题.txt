给定无向连通图和m种不同的颜色。用这些颜色为图G的各顶点着色，每个顶点着一种颜色。是否有一种着色法使G中每条边的两个顶点有不同的颜色。这个问题是图的m可着色判定问题。若一个图最少需要m种颜色才能使图中每条边相连接的两个顶点着不同颜色，称这个数m为这个图的色数。求一个图的色数m称为图的m可着色优化问题。 
给定一个图以及m种颜色，请计算出涂色方案数。




#include<stdio.h>
//#define n 5//块数
//#define m 3//颜色数 
//int a[n][n] = {
//0,1,1,1,0,
//1,0,1,1,1,
//1,1,0,1,0,
//1,1,1,0,1,
//0,1,0,1,0	
//};
#define n 4
#define m 3
int a[n][n] = {
0,1,0,1,
1,0,1,0,
0,1,0,1,
1,0,1,0
}; 
int color[n];//0表示还没有涂颜色，其他数字表示涂得几号颜色 
int count = 0;
bool ok(int t){
	int i;
	for(i = 0;i < n;i ++){//可以 n的原因的是，nfs中已经对 color[t] = 0进行了赋值，并且当i=t的时候，下面的if是不满足条件的 
		if(color[t] == color[i] && a[i][t] == 1){ 
			return false;
		}
	}
	return true;
}
void nfs(int t){
	int i;
	if(t == n){ 
		count ++;
		return;
	}
	for(i = 1;i <= m;i ++){
		color[t] = i;
		if(ok(t)){//判断当前的所有着色中是不是有相邻的块用了同一种颜色 
			nfs(t + 1);	
		}
		color[t] = 0;
	}
} 
int main()
{
	nfs(0);
	printf("%d\n",count);
	return 0;
}