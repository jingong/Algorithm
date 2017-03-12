//给定一个容积为c的背包，去尝试装n个重量为wi、价值为vi的物体，求能装下的物体的最大价值。 
#include<stdio.h>  
#include<math.h>
#define n 5
int main()  
{
	int i,j;
	int weight[n] = {12,2,1,1,4};
	int value[n] = {4,2,2,1,10};
	int num,temp;
	int weight1,value1,maxvalue = 0;
	for(num = 0;num < pow(2,n);num ++){
		weight1 = value1 = 0;
		temp = num;
		for(i = 0;i < n;i ++){
			if(temp % 2){
				weight1 = weight1 + weight[i];
				value1 = value1 + value[i];
			}
			temp = temp / 2;
		}
		if(weight1 <= 15 && maxvalue < value1){
			maxvalue = value1;
		}
	}
	printf("%d\n",maxvalue);	
	return 0;
} 