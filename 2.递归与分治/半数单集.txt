针对半数集set(n)中存在重复的问题，计算半数单集，与半数集的区别在于：不能向集合中添加已有的元素。例如，
set(6)={6,16,26,126,36,136}。
注意：该半数单集不是多重集。
要求：对于给定的自然数n，计算半数单集set(n)中的元素个数。
样例输入：
	6 
样例输出：
	6



#include<stdio.h>
#define n 48
int a[1000];
int set(int m){
	int sum = 1;
	if(m == 1)
		return 1;
	else{
		for(int i = 1;i <= m / 2;i ++){
			sum = sum + set(i);	
			if(i > 10 && 2 * (i / 10) <= i % 10){
				sum = sum - a[i / 10];
			}
		}
	}
	a[n] = sum;
	return sum;
}
int main()
{
	int count;
	a[1] = 1;
	count = set(n);
	printf("%d\n",count);
	return 0;
}