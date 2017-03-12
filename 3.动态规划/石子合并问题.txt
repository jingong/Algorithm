在一个圆形操场的四周摆放着n堆石子。现要将石子有次序地合并成一堆。规定每次只能选择相邻的两堆石子合并成新的一堆，并将新的一堆石子数记为该次合并的得分。试设计一个算法，计算出将n堆石子合并成一堆的最小得分和最大得分。
测试用例：
4（石子的堆数）
4 4 5 9（每一堆的石子数目）
输出：
    43
    54




#include<stdio.h>
#define n 4
int minScore(int *a){
	//定义二维数组m[i][j]来记录i到j的合并过成中最少石子数目  
	int m[n][n];
	int i,j,k,r;
	int sum;
	int t;
	for(i = 0;i < n;i ++)//当一个单独合并时，m[i][i]设为0，表示没有石子  
		m[i][i] = 0;
	for(r = 2;r <= n;r ++){//r用来控制目前有几堆石子
		for(i = 0;i <= n - r;i ++){
			j = i + r - 1;//j表示此时是几个石子一堆 
			sum = 0;
			for(k = i;k <= j;k ++){
				sum += a[k];
			}
			m[i][j] = m[i][i] + m[i + 1][j] + sum;//其中的一种情况
			for(k = i + 1;k < j;k ++){
				t = m[i][k] + m[k + 1][j] + sum;
				if(t < m[i][j]){
					m[i][j] = t;
				} 
			}
		}
	}
	return m[0][n - 1];
}
int maxScore(int *a){
	int m[n][n];
	int i,j,k,r;
	int sum;
	int t;
	for(i = 0;i < n;i ++)
		m[i][i] = 0;
	for(r = 2;r <= n;r ++){
		for(i = 0;i <= n - r;i ++){
			j = i + r - 1;//j表示此时是几个石子一堆 
			sum = 0;
			for(k = i;k <= j;k ++){
				sum += a[k];
			}
			m[i][j] = m[i + 1][j] + sum;
			for(k = i + 1;k < j;k ++){
				t = m[i][k] + m[k + 1][j] + sum;
				if(t > m[i][j]){
					m[i][j] = t;
				} 
			}
		}
	}
	return m[0][n - 1];
}
int main()
{
	int a[n] = {4,4,5,9};
	int temp;
	int opt;
	int i,j,k;
	int min = 1000000,max = 0;
	for(i = 0;i < n;i ++){
		temp = a[0];
		for(j = 0;j < n - 1;j ++)
			a[j] = a[j + 1];
		a[n - 1] = temp;
		opt = minScore(a);
		if(opt < min)
			min = opt;
		opt = maxScore(a);
		if(opt > max)
			max = opt;
	}
	printf("the min is %d,the max is %d.\n",min,max);
	return 0;
}