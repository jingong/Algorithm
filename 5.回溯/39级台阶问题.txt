小明看完电影《第39级台阶》，离开电影院的时候，他数了数视觉的台阶数，恰好是39级。
?    站在台阶前，他突然又想起一个问题：如果我每一步只能迈上1个或2个台阶，先迈左脚，然后左右交替，最后一步迈右脚，也就是说一共要迈偶数步。那么，上完39级台阶，有多少种不同的上法呢？
?    请利用计算机的优势，帮助小明寻找答案。




//39级台阶问题
#include<stdio.h>
int step = 0;
int foot = 0;
int count = 0;//统计方案 
void nfs(int step){
	if(foot % 2 == 0 && step == 39){
		 count ++;
		 return; 
	}
	//一步一个台阶
	foot ++;
	step ++;
	if(step <= 39)
		nfs(step);
	step --;
	foot --;
	//一步两个台阶 
	foot ++;
	step += 2;
	if(step <= 39)
		nfs(step);
	step -= 2;
	foot --; 
}
int main()
{
	nfs(0);
	printf("%d.\n",count);
	return 0;
}
======================================================================
#include<stdio.h>
int step = 0;
int foot = 0;
int count = 0;//统计方案 
void nfs(){
	if(foot % 2 == 0 && step == 39){
		 count ++;
		 return; 
	}
	//一步一个台阶
	foot ++;
	step ++;
	if(step <= 39)
		nfs();
	step --;
	foot --;
	//一步两个台阶 
	foot ++;
	step += 2;
	if(step <= 39)
		nfs();
	step -= 2;
	foot --; 
}
int main()
{
	nfs();
	printf("%d.\n",count);
	return 0;
}