给定一个自然数 n，由n开始可以依次产生半数集set(n)中的数如下：n<200
（1）n?set(n)；
（2）在 n 的左边加上一个自然数，但该自然数不能超过最近添加数的一半；
（3）按此规则进行处理，直至不能添加自然数为止。
例如，set(6)={6,16,26,126,36,136}。
注意：该半数集是多重集。
要求：对于给定的自然数n，计算半数集set(n)中的元素个数。
样例输入：
	6 
样例输出：
	6



法一：
#include<stdio.h>
#define n 8
int set(int m){
	int sum = 1;
	if(m == 1)
		return 1;
	else{
		for(int i = 1;i <= m / 2;i ++){
			sum = sum + set(i);
		}
		return sum;
	}
}
int main()
{
	int count;
	count = set(n);
	printf("%d\n",count);
	return 0;
}
法二：
#include<stdio.h>
int a[100];
int f(int n)
{
	a[0] = a[1] = 1;
	int i,j;
	for(i = 2;i <= n;i ++){
		a[i] = 0;
		for(j = 0;j <= i / 2;j ++)
			a[i] = a[i] + a[j];
	}
	return a[n];
}
int main()
{
	int n = 6;
	printf("%d\n",f(n));
	return 0;	
} 
法三：
#include<stdio.h>
int f(int n)
{
	if(n == 1)
		return 1;
	return f(n / 2 * 2 - 1) + f(n / 2);
}
int main()
{
	int n = 6;
	printf("%d\n",f(n));
	return 0;	
} 