#include<stdio.h>
#define n 5
int finish(int *flag){
	for(int i = 0;i < n;i ++){//0表示未安排，1表示安排了 
		if(flag[i] == 0){
			return 0;
		}
	}
	return 1;
}
int main()
{
	int time[n][2] = {
		{1,23},
		{12,28},
		{25,35},
		{27,38},
		{36,50}
	};
	int flag[n] = {0};
	int i,j,k;
	int count = 0;
	int temp;
	int ff; 
	for(i = 0;i < n;i ++){
		for(j = i + 1;j < n;j ++){
			if(time[i][1] > time[j][1]){
				temp = time[i][0]; time[i][0] = time[j][0]; time[j][0] = temp;
				temp = time[i][1]; time[i][1] = time[j][1]; time[j][1] = temp;
			}
		}
	}
	ff = finish(flag);
	while(ff == 0){
		i = 0;
		count ++;
		while(flag[i] == 1)
			i ++;
		flag[i] = 1;
		j = time[i][1];
		for(k = i + 1;k < n;k ++){
			if(flag[k] == 0 && time[k][0] >= j){
				flag[k] = 1;
				j = time[k][1];
			}
		}
		ff = finish(flag);
	} 
	printf("the max is %d.",count);
	return 0;
} 