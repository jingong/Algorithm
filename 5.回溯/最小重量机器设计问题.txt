设某一机器由n个部件组成，每一种价格都可以从m个不同的供应商处购得。设wij是从供应商j处购得的部件i的重量，cij是相应的价格。
试设计一个算法，给出总价格不超过d的最小重量机器设计。


//回溯
#include<stdio.h>
#define n 3//部件个数 
#define m 3//供应商个数 
int d = 4;//总价格 
int bestx[m],x[m];//记录出最好的供应商 
int price = 0,weight = 0;
int minweight = 10000;
int c[n][m] = {{1,2,3},{3,2,1},{2,2,2}};
int w[n][m] = {{1,2,3},{3,2,1},{2,2,2}};
void nfs(int t){
	int i;
	if(t == n){
		if(price <= d && weight < minweight){
			minweight = weight;
			for(i = 0;i < m;i ++){
				bestx[i] = x[i];
			}
		}
		return;
	}
	for(i = 0;i < m;i ++){
		price += c[t][i];
		weight += w[t][i];
		x[t] = i;
		if(weight <= minweight && price <= d){//减支 
			nfs(t + 1);	
		}
		price -= c[t][i];
		weight -= w[t][i];
	}
}
int main(){
	int i;
	nfs(0);
	printf("the min weight is %d.\n",minweight);
	for(i = 0;i < m;i ++){
		printf("%d ",bestx[i] + 1); 
	}
	putchar('\n');
	return 0;
} 