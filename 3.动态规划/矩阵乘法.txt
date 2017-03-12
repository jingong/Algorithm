#include<stdio.h>

int main()
{
	int i,j,k;
	int a[2][3] = {{1,2,3},{2,1,3}};
	int b[3][2] = {{1,2},{2,1},{1,3}};
	int c[2][2];
	int sum;
	for(i = 0;i < 2;i ++){
		for(j = 0;j < 2;j ++){
			sum = 0;
			for(k = 0;k < 3;k ++){
				sum = sum + a[i][k] * b[k][j];
			}
			c[i][j] = sum;
		}
	}
	for(i = 0;i < 2;i ++){
		for(j = 0;j < 2;j ++){
			printf("%3d",c[i][j]);
		}
		printf("\n");
	}
	return 0;
}