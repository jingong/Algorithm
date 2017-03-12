设有 n=2k个选手要进行网球循环赛。现要设计一个满足以下要求的比赛日程表：
（1）每个选手必须与其他 n-1个选手各赛一次；
（2）每个选手一天只能赛一次；
（3）循环赛一共进行 n-1天。



#include<stdio.h>
#define n 8
int main()
{
	int i,j,k,index,p,q,direction;
	int a[8][8];
	for(i = 0;i < n;i ++){
		a[0][i] = i + 1;
	}
	k = 1;
	index = 1;
	while(k < n){
		direction = 1;
		for(p = index;p < k + index;p ++){
			for(q = 0;q < n;q ++){
				a[p][q] = a[p - k][q + k * direction];
				if((q + 1) % k == 0){
					direction = direction * (-1);
				}
			}
				
		}
		index = index + k;
		k = k * 2;
	}
	
	
	for(i = 0;i < n;i ++){
		for(j = 0;j < n;j ++)
			printf("%2d",a[i][j]);
		putchar('\n');
	}
	return 0;
}