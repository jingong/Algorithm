用两台处理机A和B处理n个作业。设第i个作业交给A处理需要时间ai，交给B处理需要时间bi。由于各作业的特点和机器的性能关系，ai和bi之间没有明确的大小关系。既不有将一个作业分开由2台机器处理，也没有一台机器能同时处理2个作业。设计一个动态规划算法，使得这两台机器处理完这n个作业的时间最短。
测试用例：
6（任务数目）
2 5 7 10 5 2（机器A处理这些任务的时间）
3 8 4 11 3 4（机器B处理这些任务的时间）
输出：15



//暴力
#include<stdio.h>
#include<math.h>
#define n 6
int main()
{
	int a[n] = {2,5,7,10,5,2};
	int b[n] = {3,8,4,11,3,4};
	int i,j,k;
	int num,temp,tempmin;
	int timea,timeb;
	int min = 1000000;
	for(num = 0;num < pow(2,n);num ++){
		timea = timeb = 0;
		temp = num;
		for(i = 0;i < n;i ++){
			if(temp % 2 == 0){
				timea += a[i];
			}
			else{
				timeb += b[i];
			}
			temp /= 2;
		}
		tempmin = timea > timeb ? timea : timeb;
		if(tempmin < min){
			min = tempmin;
		}
	}
	printf("the min time is %d.\n",min);
	return 0;	
}
=======================================================================
//动态规划
#include<stdio.h>
#define n 6
//int p[67][67][7];
int main()
{
	int a[n + 1] = {0,2,5,7,10,5,2};
	int b[n + 1] = {0,3,8,4,11,3,4};
	int i,j,k;
	int m = 0;
	int min = 10000000;
	int opt;
	for(i = 1;i <= n;i ++){
		if(a[i] > m)
			m = a[i];
		if(b[i] > m)
			m = b[i];
	}
	//p[m * n + 1][m * n + 1][n + 1],m * n表示前面n个作业完成可能需要的最大时间，m是单个的最大时间 
	bool ***p;//设布尔量p（i，j，k）表示前k个作业可以在处理机A用时不超过i且处理机B用时不超过j时间内完成
	p = new bool**[m * n + 1];
	for(i = 0;i <= m * n;i ++){
		p[i] = new bool *[m * n + 1];
	}
	for(i = 0;i <= m * n;i ++){
		for(j = 0;j <= m * n;j ++){
			p[i][j] = new bool[n + 1];
		}	
	}
	for(i = 0;i <= m * n;i ++){
		for(j = 0;j <= m * n;j ++){
			p[i][j][0] = true;
			for(k = 1;k < n;k ++)
				p[i][j][k] = false;
		}
	}
	for(k = 1;k <= n;k ++){//k表示前k个作业 
		for(i = 0;i <= m * n;i ++){
			for(j = 0;j <= m * n;j ++){
				if(i - a[k] >= 0)
					p[i][j][k] = p[i - a[k]][j][k - 1];
				if(j - b[k] >= 0)
					p[i][j][k] = p[i][j][k] || p[i][j - b[k]][k - 1];
			}
		}
	}
	for(i = 0;i <= m * n;i ++){
		for(j = 0;j <= m * n;j ++){
			if(p[i][j][n]){
				opt = i > j ? i : j;
				if(opt < min){
					min = opt;
				}
			}
		}
	}
	printf("the min time is %d.\n",min);
	return 0;	
}  