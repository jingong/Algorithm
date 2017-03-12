给定 n 个实数，求这n个实数在数轴上相邻2个数之间的最大差值，设计解最大间隙问题的线性时间算法。

#include<stdio.h>
#define N 5
int main()
{
	float num[N] = {1.1,3.2,2.2,6.8,5.4};
	float length = 0,temp,t1,t2;
	for(int i = 0;i < N - 1;i ++){
		for(int j = i;j < N;j ++)
		{
			temp = (num[i] - num[j]) * (num[i] - num[j]);
			if(temp > length)
			{
				length = temp;
				t1 = num[i];
				t2 = num[j];
			}	
		}
	}
	printf("%.2f %.2f",t1,t2);
	return 0;
}
=========================================================================
#include<stdio.h>
#define n 5
int main()
{
	double number[n] = {2.3,3.1,7.5,1.5,6.3};
	double max,min;
	double maxgap = 0;
	double low[n],high[n];
	double left;
	int i;
	int count[n];
	max = number[0];
	min = number[0];
	for(i = 1;i < n;i ++)
	{
		if(max < number[i])
		{
			max = number[i];
		}
		if(min > number[i])
		{
			min = number[i];
		}
	}
	//n-2个元素分配到n-1个桶中
	for(i = 0;i < n - 1;i ++)
	{
		count[i] = 0;
		low[i] = max;
		high[i] = min;
	 } 
	//把元素分配到桶中，只对上下界和个数进行更新
	for(i = 0;i < n;i ++){
		int bucket = (int)((number[i] - min) / ((max - min) / (n - 1)));
		count[bucket] ++;
		
		if(low[bucket] > number[i])
		{
			low[bucket] = number[i];
		}
		if(high[bucket] < number[i])
		{
			high[bucket] = number[i];
		}
	} 
	//求最大间距
	left = high[0];
	for(i = 1;i < n - 1;i ++)
	{
		if(count[i])
		{
			double gap = low[i] - left;
			if(gap > maxgap)
				maxgap = gap;
			left = high[i];	
		}
		
	}
	printf("max gap is:%.2lf\n",maxgap);
	return 0;
} 