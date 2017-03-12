//多处最优服务次序问题 
#include<stdio.h>
#include<algorithm>
using namespace std;
#define n 10 
#define s 2
int main()
{
	int a[n] = {56,12,1,99,1000,234,33,55,99,812};
	int i;
	int sum = 0;
	int sub[s] = {0};
	sort(a,a + n);
	for(i = 0;i < n;i ++){
		sub[i % s] += a[i];
		sum += sub[i % s];
	}
	printf("%.2f",sum * 1.0 / n);
	return 0;	
} 