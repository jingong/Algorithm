勾股定理，西方称为毕达哥拉斯定理，它所对应的三角形现在称为：直角三角形。已知直角三角形的斜边是某个整数，并且要求另外两条边也必须是整数。求满足这个条件的不同直角三角形的个数。




#include<stdio.h>
#include<math.h>
int main()
{
	int c;
	int a,b;
	int i;
	int count = 0;
	scanf("%d",&c);
	for(i = 1;i < c;i ++){
		a = i * i;
		b = sqrt(c * c - a);
		if((a + b * b) == c *c){
			printf("%d \t %d.\n",i,b);
			count ++;
		}
	}
	printf("%d",count / 2);
	return 0;	
} 