长江俱乐部在长江设置了n个游艇出租站1,2,…n，游客可在这些游艇出租站租用游艇，并在下游的任何一个游艇出租站归还游艇。游艇出租站i到游艇出租站j之间的租金为r(i,j)，设计一个算法，计算出从出租站1到出租站n所需要的最少租金。
测试用例：
3（站数）
5 15（第一站到其他相应各站的租金）
7（第二站到其他相应各站的租金）
输出：
12



#include<stdio.h>
#define n 4
int main()
{
	int rent[n - 1][n] = {{0,1,3,4},{0,0,1,5},{0,0,0,1}};
	int m[n];//表示从第1站到第n站的最少费用
	int i,j,k;
	int max,min;
	for(k = 1;k < n;k ++){
		m[k] = rent[0][k];
		for(i = 1;i < k;i ++){
			if(m[i] + rent[i][k] < m[k]){
				m[k] = m[i] + rent[i][k];
			}
		}
	}
	printf("the minimum charge is %d.\n",m[n - 1]);
	return 0;
}