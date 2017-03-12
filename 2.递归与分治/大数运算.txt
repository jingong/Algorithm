#include<stdio.h>
#include<string.h>
int main()
{
	int i,j;
	int num1[100],num2[100],num3[200];
	int index;
	int over = 0;//over表示要仅为的数值 
	char str1[100],str2[100];
	int temp;
	scanf("%s",str1);
	scanf("%s",str2);
	index = 0;
	for(i = strlen(str1) - 1;i >= 0;i --){
		num1[index] = str1[i] - '0';
		index ++;
	}
	printf("%d\n",strlen(str1));
	index = 0;
	for(i = strlen(str2) - 1;i >= 0;i --){
		num2[index] = str2[i] - '0';
		index ++;
	}
	index = 0;
	while(index < strlen(str1) && index < strlen(str2)){
		temp = num1[index] + num2[index] + over;
		num3[index] = temp % 10;
		over = temp / 10;
		index ++;
	}
	if(index == strlen(str1) && index < strlen(str2)){
		for(j = index;j < strlen(str2);j ++){
			num3[j] = (num2[j] + over) % 10;
			over = (num2[j] + over) / 10;
			index ++;
		}
	}
	if(index == strlen(str2) && index < strlen(str1)){
		for(j = index;j < strlen(str1);j ++){
			num3[j] = (num1[j] + over) % 10;
			over = (num1[j] + over) / 10;
			index ++;
		}
	}
	if(over){
		num3[index] = over;
		index ++;
	}
	for(i = index - 1;i >= 0;i --)
		printf("%d",num3[i]);
	putchar('\n');
	return 0;
} 