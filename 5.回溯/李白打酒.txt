话说大诗人李白，一生好饮。幸好他从不开车。一天，他提着酒壶，从家里出来，酒壶中有酒2斗。他边走边唱：
无事街上走，提壶去打酒。
逢店加一倍，遇花喝一斗。
这一路上，他一共遇到店5次，遇到花10次，已知最后一次遇到的是花，他正好把酒喝光了。 
请你计算李白遇到店和花的次序，可以把遇店记为a，遇花记为b。则：babaabbabbabbbb 就是合理的次序。像这样的答案一共有多少呢？请你计算出所有可能方案的个数（包含题目给出的）。



//李白打酒（暴力） 
#include<stdio.h>
#include<math.h>
int main()
{
	int i,j,k;
	int num,temp;
	int flower,shop,wine;
	int count = 0;
	for(num = 0;num < pow(2,14);num ++){
		flower = 0;shop = 0;wine = 2;
		temp = num;
		for(i = 0;i < 14;i ++){
			if(temp % 2){
				flower ++;
				wine --;
			}else{
				shop ++;
				wine *= 2;
			}
			temp /= 2;
		}
		if(wine == 1 && flower == 9 && shop == 5){
			count ++;
		}
	}	
	printf("%d.\n",count);
	return 0;	
}
//李白打酒（回溯）
#include<stdio.h>
int count = 0;
int flower = 0;
int shop = 0;
int wine = 2;
void nfs(int n){
	if(n == 15){
		if(flower == 9 && shop == 5 && wine == 1){
			count ++;
		} 
		return;
	}
	if(flower <= 9 && shop <= 5){
		flower ++;
		wine --;
		nfs(n + 1);
		wine ++;
		flower --;
	}
	
	
	shop ++;
	wine *= 2;
	nfs(n + 1);
	wine /= 2;
	shop --;
}
int main()
{
	nfs(1);	
	printf("%d.\n",count);
	return 0;	
}   