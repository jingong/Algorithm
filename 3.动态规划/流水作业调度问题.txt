n个作业{0,1,2,…,n}在2台机器上M1和M2组成的流水线上完成加工。每个作业加工的顺序都是先在M1上加工，后在M2上加工。在两台机器上加工的时间分别为ai和bi。
目标：确定这n个作业的加工顺序，使得从第一台作业开始加工，到最后一个作业完成加工所需要的时间最少。

假设要对集合S中的作业进行加工，当M1开始加工时，假设M2正在工作，还需要时间t后才能使用。将这种情况下完成加工的时间记为T(S,t)。则流水作业调度的最优值为T(N,0)。

假设先加工第i个作业，则需要的时间为：
ai+T(N-{i},bi)

作业调度问题的最优解为：
T(N,0) = min{a[i] + T(N - {i},b[i])}
       1<=i<=n

T(S,t) = min{a[i] + T(S - {i},b[i] + max{t,a[i]} - a[i])}
       1<=i<=n

#include<stdio.h>
#define n 4
int a[n]={5,12,4,8};	//m1
int b[n]={6,2,14,7}; //m2
int index[n]={0,1,2,3};//方便全排列 
int work(int i,int t){//work(int i,int t)表示作业i的前一个作业在机器2上用的时间为t 
	if(i == n - 1){
		if(t > a[index[i]]){
			return t - a[index[i]] + a[index[i]] + b[index[i]];
		}else{
			return a[index[i]] + b[index[i]];
		}
	}
	int minvalue;
	int tempvalue,temp;
	int tt;
	int j;
	tt = (t - a[index[i]]) > 0 ? (t - a[index[i]]) : 0;
	minvalue = a[index[i]] + work(i + 1,tt + b[index[i]]);
	for(j = i + 1;j < n;j ++){
		temp = index[i]; 
		index[i] = index[j]; index[j] = temp;
		tt = (t - a[index[i]]) > 0 ? (t - a[index[i]]) : 0; 
		tempvalue = a[index[i]] + work(i + 1,tt + b[index[i]]);
		if(tempvalue < minvalue){
			minvalue = tempvalue;
		}
		temp = index[i]; index[i] = index[j]; index[j] = temp;
	}
	return minvalue;
}
int main()
{
	printf("the min is %d.",work(0,0));
	return 0;	
} 