设n是一个正整数，2*n的二维表是由正整数1,2,…,2n组成的2*n数组，该数组的每行从左到右递增，每列从上到下递增。2*n的标准二维表全体记为tab(n)。例如，当n=3时，tab(3)的二维表如下图所示：
1 2 3      1 2 4       1 2 5       1 3 4       1 3 5
4 5 6      3 5 6       3 4 6       2 5 6       2 4 6



//法一（暴力）
//本题相当于对123456每一位进行标记，如果0就放到第一行，如果为1就放到第二行，所以0的个数要和1的个//数相等，又因为123456本身就是一个有序的，所以要想保证列上的递增，0的个数始终要大于等于1的个数。
#include<stdio.h>
#include<math.h>
#define n 3
int main()
{
	int i,j;
	int count0,count1;
	int count = 0;
	int num;
	for(i = 0;i < pow(2,2 * n);i ++){
		num = i;
		count0 = count1 = 0;
		for(j = 0;j < 2 * n;j ++){
			if(num % 2 == 0){
				count0 ++;
			}else{
				count1 ++;
			}
			num = num / 2;
			if(count1 > count0)
				break;
		} 
		if(count1 == count0 && count0 == n)
			count ++;
	}
	printf("%d\n",count);
	return 0;
}
//法二
#include<stdio.h>
int f(int n)
{
	int i;
	int count = 0;
	if(n == 1 || n == 0)
		return 1;
	for(i = 0;i < n;i ++)
		count = count + f(i) * f(n - 1 - i);
	return count;
}
int main()
{
	int n = 3;
	printf("%d\n",f(n));
	return 0;	
} 