//0-1背包问题 
#include<stdio.h>
#define n 3
int w[n] = {40,5,40};
int c = 50;
int flag[n],best[n];
int temp;
int max;
int rest; 
void nfs(int m)
{
	int i;
	if(m == n){
		if(temp > max){//if(temp >= max)这样会输出最后满足条件的，也就是5 40 
			max = temp;
			for(i = 0;i < n;i ++){
				best[i] = flag[i];
			}
		}
		return;
	}
	if(temp + rest > max){//rest是剩余的所有没加的，如果temp + rest <= max的话，可以提前结束当前分支 
		if(temp + w[m] <= c){
			temp += w[m];
			flag[m] = 1;
			rest -= w[m];
			nfs(m + 1);
			rest += w[m]; 
			temp -= w[m];	
		}
		rest -= w[m];
		flag[m] = 0;
		nfs(m + 1);
		rest += w[m];
	}
	 
}
int main()
{
	int i;
	temp = 0;
	rest = 0;
	for(i = 0;i < n;i ++)
		rest += w[i]; 
	nfs(0);
	printf("the max is %d.\n",max);
	for(i = 0;i < n;i ++){
		if(best[i] == 1){
			printf("%d  ",w[i]);	
		}
	}
	putchar('\n');	
	return 0;	
} 