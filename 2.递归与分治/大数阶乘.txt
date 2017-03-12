#include<stdio.h>
int main()
{
	int i,j;
	int result[100];//记录数据
	result[0] = 1; 
	int length = 1;//目前的长度 
	int n;
	int over;
	int temp; 
	scanf("%d",&n);
	for(i = 1;i <= n;i ++){
		over = 0;
		for(j = 0;j < length;j ++){
			temp = result[j] * i + over;
			result[j] = temp % 10;
			over = temp / 10;
		}
		while(over){
			result[length] = over % 10;
			over = over / 10;
			length ++;
		}
	}
	for(i = length - 1;i >= 0;i --)
		printf("%d",result[i]);
	putchar('\n');
	return 0;
}