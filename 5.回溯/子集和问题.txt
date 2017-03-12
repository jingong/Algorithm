//子集和问题
#include<stdio.h>
#define n 5
#define c 10
int a[n]={2,2,6,5,4};
int flag[n];
int sum = 0;
void nfs(int t){
	int i;
	if(t == n){
		if(sum == c){
			for(i = 0;i < n;i ++){
				if(flag[i] == 1){
					printf("%d ",a[i]);
				}	
			}
			putchar('\n');
		}
		return;
	}
	sum += a[t];
	flag[t] = 1;
	nfs(t + 1);
	
	sum -= a[t];
	
	flag[t] = 0;
	nfs(t + 1);
}
int main()
{
	nfs(0);
	return 0;	
} 