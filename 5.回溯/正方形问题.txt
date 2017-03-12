Given a set of sticks of various lengths, is it possible to join them end-to-end to form a square??




#include<stdio.h>
#define n 8
#define m 4//正方形的四条边 
int len[n] = {1,8,3,7,5,4,3,5};
int sum[m] = {0};//用于保存每一条边上的木棍的长度的和 
int flag = 0;
int edge = 0;
bool ok(){
	int i;
	for(i = 0;i < m;i ++){
		if(sum[i] != edge){
			return false;
		}
	}
	return true;
}
void nfs(int t){
	int i;
	if(flag)
		return;
	if(t == n){
		if(ok()){
			flag = 1;
		}
		return;
	}
	for(i = 0;i < m;i ++){
		sum[i] += len[t];
		if(sum[i] <= edge){
			nfs(t + 1);
		}
		sum[i] -= len[t];
	} 
}
int main()
{
	int i;
	for(i = 0;i < n;i ++){
		edge += len[i];
	}
	if(edge % m != 0){
		printf("no.\n");
		return 0;
	}
	edge /= m;
	nfs(0);
	if(flag){
		printf("yes.\n");
	}else{
		printf("no.\n");
	}
	return 0;	
}