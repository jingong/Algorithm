设有n个顾客同时等待一项服务，顾客i所需要的服务时间为ti，应如何安排顾客的服务次序，才能使平均等待时间最短？平均等待时间是n个顾客等待服务时间的总和除以n。
测试用例：
10（顾客数）
56 12 1 99 1000 234 33 55 99 812（所有顾客的服务时间）
输出：
532（最小平均等待时间）




#include<stdio.h>
#include<algorithm>
using namespace std;
#define n 10
int main()
{
	int i;
	int a[n] = {56,12,1,99,1000,234,33,55,99,812};
	float sum = 0.;
	sort(a,a + n);
	for(i = 0;i < n;i ++){
		sum += (n - i) * a[i];
	} 
	printf("%.2f",sum / n);
	return 0;
}