今有7对数字：两个1，两个2，两个3，...两个7，把它们排成一行。
要求，两个1间有1个其它数字，两个2间有2个其它数字，以此类推，两个7之间有7个其它数字。如下就是一个符合要求的排列：
17126425374635
当然，如果把它倒过来，也是符合要求的。
请你找出另一种符合要求的排列法，并且这个排列法是以74开头的。
注意：只填写这个14位的整数，不能填写任何多余的内容，比如说明注释等。
74****4*7*******




#include<stdio.h>
#define n 7
int x[n + 1];//x[i]表示数字i放到了 x[i]号位上 
int arr[n * 2] = {0};//表示这个整数 
int judge(int arr[]){
	int i;
	for(i = 0;i < 2 * n;i ++){
		if(arr[i] == 0){
			return 0;
		}
	}
	return 1;
}
void nfs(int t){
	int i;
	if(t == (n + 1)){
		if(x[7] == 0 && x[4] == 1 && judge(arr)){
			for(i = 0;i < 2 * n;i ++)
				printf("%d",arr[i]);
		} 
		return;
	} 
	//x + t + 1 < 2n化简得到下限为2n - t - 1 
	for(i = 0;i < 2 * n - t - 1;i ++){
		x[t] = i;
		if(arr[i] == 0 && arr[i + t + 1] == 0){
			arr[i] = t;
			arr[i + t + 1] = t;
			nfs(t + 1);
			arr[i] = 0;
			arr[i + t + 1] = 0;	
		} 	
	}
} 
int main(){
	nfs(1);
	return 0;
} 