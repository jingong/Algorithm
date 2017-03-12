集合S中有n个元素，其中的元素可能重复，设计一个算法，计算出S的不同排列。
样例输入：
	4
	aacc 
样例输出：
	aacc
	acac
	acca
	caac
	caca
	ccaa
	6



#include <stdio.h>
#include <string.h>

int a[4]={1,1,2,2};

int notExists(int index, int left, int right)
{
	int flag=1;
	for(int i=left;i<index;i++){
		if(a[i]==a[index]){
			flag=0;
			break;
		}
	}
	return flag;
}

void perm(int left, int right)
{
	if (left==right){
		for(int i=0;i<4;i++)
			printf("%d",a[i]);
		printf("\n");
	}
	else{
		for(int i=left;i<=right;i++){
			if(notExists(i,left,right)){
				int temp=a[left];
				a[left]=a[i];
				a[i]=temp;

				perm(left+1,right);
				
				temp=a[left];
				a[left]=a[i];
				a[i]=temp;
			}
		}
	}
}

int main()
{
	perm(0,3);
	return 0;
}