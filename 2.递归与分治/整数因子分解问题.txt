大于1的正整数n可以分解为不同的因子相乘，例如n=12时，有
12=12		12=3*2*2
12=6*2		12=2*6
12=4*3		12=2*3*2
12=3*4		12=2*2*2
要求：给定正整数n，计算n共有多少种不同的分解形式。
样例输入：
12
样例输出：
8



#include<stdio.h>
int solve(int n){
	int count = 0;
	int i;
	if(n == 1)
		return 1;
	for(i = 2;i <= n;i ++){
		if(n % i == 0){
			count = count + solve(n / i);
		}
	}
	return count;
}
int main()
{
	int n = 12;
	printf("%d\n",solve(n));
	return 0;
}