正整数 x 的约数是能整除x的正整数，其约数的个数记为div(x)，例如div(10)=4。设 a 和 b 是两个正整数，找出 a 和 b 之间约数个数最多的数 x 的约数个数。
样例输入： 1 36 
样例输出： 9

#include<stdio.h>
int prime(int num)//判断这个数是不是素数
{
	int flag = 1;
	for(int i = 2;i < num / 2;i ++)
	{
		if(num % i == 0)
		{
			flag = 0;
			break;
		}
	}
	return flag;
}
int div(int num)
{
	int count;
	int *result = new int[num + 1];
	int temp = num;
	int total = 1;
	for(int i = 0;i < num + 1;i ++){
		result[i] = 0;
	}
	for(int i = 2;i <= num / 2;i ++)
	{
		if(prime(i))
		{
			if(temp % i == 0)
			{
				count = 0;
				while(temp % i == 0)
				{
					count ++;
					temp = temp / i;
				}
				result[i] = count;
			}
		}	
	}
	for(int i = 2;i <= num;i ++)
	{
		if(result[i] != 0)
			total = total * (result[i] + 1); 
	}
	return total; 
}
int main()
{
	int m,n;
	int max = 0;
	int temp;
	printf("please input two num:\n");
	scanf("%d%d",&m,&n);
	for(int i = m;i <= n;i ++)
	{
		temp = div(i);
		if(temp > max){
			max = temp;
		}	
	}
	printf("max is %d.\n",max);
	return 0;
} 
