给定n位正整数a，去掉其中任意k个数字后，剩下的数字按原次序排列组成一个新的正整数。对于给定的n和k，设计一个算法，找出剩下数字组成的新数最小的删数方案。
输入示例：
    178543
输出：
    13



#include<stdio.h>
#include<math.h>
int main(){
	int num,k;
	int n;
	int i,j;
	int temp;
	int m;
	scanf("%d%d",&num,&k);
	n = log10(num) + 1;
	int *a = new int[n];
	int *flag = new int[n];
	for(i = 0;i < n;i ++){
		flag[i] = 1;//设置标志位，1表示没有被使用 
	}
	i = 1;
	temp = num;
	while(i <= n){
		a[n - i] = temp % 10;
		temp /= 10;
		i ++;
	}
	for(i = 0;i < k;i ++){
		j = 0;
		while(flag[j] == 0)
			j ++;
		for(m = j + 1;m < n;m ++){
			if(flag[m] == 1){
				if(a[m] >= a[j]){
					j = m;
				}else{
					break;
				}
			}
		}
		flag[j] = 0;
	} 
	for(i = 0;i < n;i ++){
		if(flag[i] == 1)
			printf("%d",a[i]);
	}
	putchar('\n');
	return 0;
}