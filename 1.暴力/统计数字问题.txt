给定一本书，其中包含n页，计算出书的全部页码中用到了多少个数字0…9。
144 255 255 255 251 245 244 190 144 144
//方法一
#include<stdio.h>  
#include<math.h>
int main()  
{
	int i,j,k;
	int n = 745;
	int temp,len;
	int higher,rest; 
	int count[10] = {0};
	temp = n;
	len = log10(n);
	//从000~745，算出0~9每个数字所用的次数 
	for(i = 0;i <= len;i ++){
		higher = temp / pow(10,len - i); //高位 
		rest = temp % (int)pow(10,len - i);//除了高位剩余的部分 
		count[higher] = count[higher] + rest + 1;//先算出最高的位最大的那个数用到的次数，745的话就是7 
		for(j = 0;j < higher;j ++){
			count[j] = count[j] + pow(10,len - i);//0~6所用到的次数 
			for(k = 0;k < 10;k ++){
				count[k] = count[k] + (len - i) * pow(10,len - i - 1);//00~99所用到的次数 
			} 
		} 
		temp = rest;
	}
	//去掉多余的0 
	for(i = 0;i <= len;i ++){
		count[0] = count[0] - pow(10,len - i);
	}		
	for(i = 0;i < 10;i ++){
		printf("%4d",count[i]);
	}
	putchar('\n');
	return 0;
} 
//方法二
#include<stdio.h>  
#include<math.h>
int main()  
{
	int n = 745;//假设是745页的数 
	int i,j;
	int count[10] = {0};
	int len;
	int temp;
	int high,low,num;
	len = log10(n);
	for(i = 0;i <= len;i ++){
		temp = n;
		high = temp / pow(10,len - i + 1);
		low = temp % (int)pow(10,len - i);
		num = (temp % (int)pow(10,len - i + 1))/ (int)pow(10,len - i);
		count[num] = count[num] + low + 1;
		for(j = 0;j < num;j ++){
			count[j] = count[j] + (high + 1) * pow(10,len - i);
		} 
		for(j = num;j < 10;j ++){
			count[j] = count[j] + high *  pow(10,len - i);
		}
	}	 
	//去掉多余的0 
	for(i = 0;i <= len;i ++){
		count[0] = count[0] - pow(10,len - i);
	}		
	for(i = 0;i < 10;i ++){
		printf("%4d",count[i]);
	}
	putchar('\n');
	return 0;
} 