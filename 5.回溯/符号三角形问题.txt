右图所示的三角形中，有14个“+“和14个“-”。2个同号下面是+，两个异号下面是-。
在一般情况下，符号三角形的第一行有n个符号。符号三角形问题，要求对于给定的n，计算有多少个不同的符号三角形，使其所含的“+”和“-”相同。
+ + - + - + +
 + - - - - +
  - + + + -
   - + + -
    - + -
     - -
      +


//暴力
#include<stdio.h>
#include<math.h>
int main(){
	int n;//第一行有几个数 
	int num,temp;
	int i,j,k;
	int sum;
	int count = 0;
	char ch[] = {'+','-'};//0表示+，1表示-
	int **a; 
	scanf("%d",&n);
	if((n * (n + 1)) % 4 != 0){//这里为了保证让+和-的个数相同，所以必须要求 (n * (n + 1)) / 2为偶数 
		printf("输入有误！");
		return 0; 
	}
	//动态申请空间 
	a = new int*[n];
	for(i = 0;i < n;i ++){
		a[i] = new int[n];
	}
	for(int num = 0;num < pow(2,n);num ++){
		sum = 0;
		temp = num;
		for(i = 0;i < n;i ++){
			a[0][i] = temp % 2;
			temp /= 2; 
		}
		for(i = 1;i < n;i ++){
			for(j = 0;j < n - i;j ++){
				a[i][j] = a[i - 1][j] ^ a[i - 1][j + 1];
			}
		}
		for(i = 0;i < n;i ++){
			for(j = 0;j < n - i;j ++){
				sum += a[i][j]; 
			}
		}
		if(sum * 2 == n * (n + 1) / 2){
			count ++;
			printf("********%d********\n",count);
			for(i = 0;i < n;i ++){
				for(j = 0;j < n - i;j ++){
					printf("%c",ch[a[i][j]]);
				}
				putchar('\n');
			}
		}
	}
	printf("the number is %d.",count);
	return 0;
} 
========================================================================================
//回溯
#include<stdio.h>
int n;//第一行有几个数 
int sum = 0;
int count = 0;
char ch[] = {'+','-'};//0表示+，1表示-
int **a;
int half;
void nfs(int t)
{
	int i,j;
	if(t == n){
		if(sum * 2 == n * (n + 1) / 2){
			count ++;
			printf("********%d********\n",count);
			for(i = 0;i < n;i ++){
				for(j = 0;j < n - i;j ++){
					printf("%c",ch[a[i][j]]);
				}
				putchar('\n');
			}
		}
		return;
	}
	for(i = 0;i < 2;i ++){//两次循环表示分别走左右分支 
		a[0][t] = i;
		sum += i;
		for(j = 1;j <= t;j ++){//第一行每增加一个数，从第1~t行的末尾每行也会增加一个数 
			a[j][t - j] = a[j - 1][t - j] ^ a[j - 1][t - j + 1];
			sum += a[j][t - j];	 
		}
		if(sum <= half && ((t + 1) * (t + 2) / 2 - sum)<= half){
			nfs(t + 1);
			for(j = 1;j <= t;j ++){//第一行每增加一个数，从第1~t行的末尾每行也会增加一个数 
				sum -= a[j][t - j];	 
			}
			sum -= i;	
		}
		
	}
}
int main(){
	int i;
	scanf("%d",&n);
	half = n * (n + 1) / 2;
	if((n * (n + 1)) % 4 != 0){//这里为了保证让+和-的个数相同，所以必须要求 (n * (n + 1)) / 2为偶数 
		printf("输入有误！");
		return 0; 
	}
	//动态申请空间 
	a = new int*[n];
	for(i = 0;i < n;i ++){
		a[i] = new int[n];
	}
	nfs(0);
	printf("the number is %d.",count);
	return 0;
} 
