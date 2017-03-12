//小李的店里专卖其它店中下架的样品电视机，可称为：样品电视专卖店。其标价都是4位数字（即千元不等）。小李为了标价清晰、方便，使用了预制的类似数码管的标价签，只要用颜色笔涂数字就可以了。  

    这种价牌有个特点，对一些数字，倒过来看也是合理的数字。如：1 2 5 6 8 9 0 都可以。这样一来，如果牌子挂倒了，有可能完全变成了另一个价格，比如：1958 倒着挂就是：8561，差了几千元啊!!      当然，多数情况不能倒读，比如，1110 就不能倒过来，因为0不能作为开始数字。    有一天，悲剧终于发生了。某个店员不小心把店里的某两个价格牌给挂倒了。并且这两个价格牌的电视机都卖出去了!    庆幸的是价格出入不大，其中一个价牌赔了2百多，另一个价牌却赚了8百多，综合起来，反而多赚了558元。    请根据这些信息计算：赔钱的那个价牌正确的价格应该是多少？答案是一个4位的整数，请通过浏览器直接提交该数字。9088 
#include<stdio.h>
int reverse(int n)
{
	if(n == 6)
		return 9;
	if(n == 9)
		return 6;
	return n;
}
int main()
{
	int i,j;
	int sum1,sum2,sum3,sum4;
	int num[7] ={1,2,5,6,8,9,0};
	for(int a = 0;a < 6;a ++)
		for(int b = 0;b < 7;b ++)
			for(int c = 0;c < 7;c ++)
				for(int d = 0;d < 6;d ++)
				{
					sum1 = num[a] * 1000 + num[b] * 100 + num[c] * 10 + num[d];
					sum2 = reverse(num[a]) + reverse(num[b]) * 10 + reverse(num[c]) * 100 + reverse(num[d]) * 1000;
					if((sum1 - sum2) > 200 && (sum1 - sum2) < 300 ){
						for(int e = 0;e < 6;e ++)
							for(int f = 0;f < 7;f ++)
								for(int g = 0;g < 7;g ++)
									for(int h = 0;h < 6;h ++)
									{
										sum3 = num[e] * 1000 + num[f] * 100 + num[g] * 10 + num[h];
										sum4 = reverse(num[e]) + reverse(num[f]) * 10 + reverse(num[g]) * 100 + reverse(num[h]) * 1000;
										if((sum4 - sum3) > 800 && (sum4 - sum3) < 900){
											if((sum4 - sum3 - sum1 + sum2) == 558)
											
											{
												printf("%d %d\n",sum1,sum3);
											}
										}
									}
					}
				}
	return 0;
 }