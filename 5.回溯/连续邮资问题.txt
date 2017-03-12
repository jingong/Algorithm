假设某国家发行了n种不同面值的邮票，并且规定每张信封上最多只允许贴m张邮票。连续邮箱问题要求对于给定的n和m，给出邮票面值的最佳设计，在1张信封上贴出从邮资1开始，增量为1的最大连续邮资区间。
例如当n=5，m=4时，面值为1，3，11，15，32的5种邮票可以贴出邮资的最大连续区间是1到70。





//连续邮资问题
#include<stdio.h>
#define n 6
#define m 4
int a[n] = {0,1,3,11,15,32};//增加一个价格为0的邮票，这样就能利用回溯来解决问题，关键
int flag = 1;
int money;
int num; 
void nfs(int t){
	int i;
	if(flag == 0){
		return;
	}
	if(t == m){
		if(money == num)
			flag = 0;
		return;
	}
	for(i = 0;i < n;i ++){
		money += a[i];
		if(money <= num){
			nfs(t + 1);
		}
		money -= a[i];
	}
}
int main()
{
	num = 1;
	while(1){
		flag = 1;
		money = 0;
		nfs(0);
		if(flag)
			break;
		num ++;
	}
	printf("%d.\n",num - 1);
	return 0;	
}  