#include<stdio.h>
int main()
{
	int n = 1;
	int count = 0;
	n = n % 2011;
	while(1){
		count ++;
		if(n % 2011 == 0)
			break;
		else
			n = (n % 2011) * 10 + 1;	
	}
	printf("%d",count);
	return 0;
 } 