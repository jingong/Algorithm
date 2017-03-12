设有n件工作分配给n个人。将工作i分配给第j个人所需要的费用为cij。试设计一个算法，为每个人分配1件不同的工作，并使总费用达到最小。



#include<stdio.h>
#define n 3
int price[n][n] = {10,2,3,2,3,4,3,4,5};//费用 
int minprice = 10000;
int tempprice;
int a[n];//用于保存哪个人干了哪个工作
bool ok(int t){
	int i;
	for(i = 0;i < t;i ++){
		if(a[t] == a[i]){//表示出现同一个工作分配给了两个人 
			return false; 
		}
	}
	return true;
}
void nfs(int t){//t表示的是当前在为第t个人分配工作 
	int i;
	if(t == n){
		if(tempprice < minprice){
			minprice = tempprice;
		}
		return;
	} 
	for(i = 0;i < n;i ++){
		a[t] = i;
		tempprice += price[t][i];
		if(tempprice < minprice && ok(t)){
			nfs(t + 1); 
		}
		tempprice -= price[t][i];
	}
} 
int main()
{
	nfs(0);
	printf("%d\n",minprice); 
	return 0;	
} 