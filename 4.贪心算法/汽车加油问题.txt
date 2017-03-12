一辆汽车加满油后可以行驶n公里，旅途中有加油站，设计一个有效算法，指出应在哪些加油站停靠加油，使沿途加油次数最少。
测试用例：
7 7 （n k）
1 2 3 4 5 1 6 6（第k个加油站与第k-1个加油站之间的距离，其中第一个代表起点，最后一个代表终点。）

输出：
4（最少加油次数）





#include<stdio.h>
#define n 7//n表示汽车加满油后可以行使nkm 
int main()
{
	int a[n + 1] = {1,2,3,4,5,1,6,6};
	int k = 7;//k表示途中有k个加油站 
	int rest = 7;//油箱里的剩余油量，在起点时油量是满的
	int count = 0;
	int i = 0;
	while(i < n + 1){
		if(a[i] > rest){
			count ++;
			rest = n;
		}	
		rest -= a[i];
		i ++;
	}
	printf("the mininum is %d.",count);
	return 0;
}