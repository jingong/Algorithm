在数据加密和数据压缩中常需要对特殊的字符串进行编码。给定的字母表A由26个小写字母组成。该字母表产生的升序字符串中字母从左到右出现的次序与字母在字母表中出现的次序相同，且每个字符最多出现1次。例如，a,b,ab,bc,xyz等字符串都是升序字符串。现在对字母表中产生的所有长度不超过6的升序字符串，计算它在字典中的编码。
import java.util.Scanner;


public class Test {
	public static void main(String[] args) {
		Test test = new Test();
		Scanner sc = new Scanner(System.in);
		int a = sc.nextInt();
		String str[] = new String[a + 1];
		for (int i = 0; i < str.length - 1; i++) {
			str[i] = sc.next();
		}
		for (int i = 0; i < str.length - 1; i++) {
			System.out.println(test.getResult(str[i]));
		}
	}
	//递归计算以i开始的长度为k的所有数的个数
	private int Amount(int i,int k){
		int sum = 0;
		if (k == 1) {
			return 1;
		}
		else {
			for (int j = i + 1; j <= 26; j++) {
				sum = sum + Amount(i, k - 1);
			}
		}
		return sum;
	}
	//计算组合个数
	private int Zhuhe(int k){
		int sum = 0;
		for (int i = 1; i <= 26; i++) {
			sum = sum + Amount(i, k);
		}
		return sum;
	}
	private int toInt(char c){
		return c - 'a' + 1;
	}
	//计算序列号
	private int getResult(String s){
		int k = s.length();
		int sum = 0,temp = 0;
		//获取1~k-1长度的子字符串数
		for (int i = 1; i < k; i++) {
			sum = sum + Zhuhe(i);
		}
		//小于都一个字母的长度为k的所有组合个数
		for (int i = 1; i < toInt(s.charAt(0)); i++) {
			sum = sum + Amount(i, k);
		}
		//以第一个字母作为开始的字符串组合个数
		temp = toInt(s.charAt(0));
		for (int i = 0; i < s.length(); i++) {
			int t = toInt(s.charAt(i));
			int len = s.length() - i;
			for (int j = temp + 1; j < t; j++) {
				sum = sum + Amount(j, len);
			}
			temp = t;
		}
		return sum + 1;
	}
}



#include<stdio.h>
#include<string.h>
//计算以第i个字符打头，长度为j的字符串的个数 
int f(int i,int j){
	if(j == 1){
		return 1;
	} 
	else{
		int count = 0;
		int k;
		for(k = i + 1;k <= 26 - j + 1;k ++){
			count += f(k,j - 1);
		}
		return count;
	}
	
}  
//计算不超过j的总长度 
int g(int j){
	int i;
	int count = 0;
	for(i = 1;i <= 26;i ++){
		count += f(i,j);
	}
	return count;
}
int main()
{
	char *str = "ab";
	int pos = 0;
	int i,j;
	//printf("%d\n",str[0] - 'a' + 1);
	//计算位数小于字符串长度的字典序个数 
	for(i = 1;i < strlen(str);i ++){
		pos += g(i);
	}
	//计算第一个字符串第一个字母前面的字典序个数
	for(i = 1;i < (str[0] - 'a' + 1);i ++){
		pos += f(i,strlen(str));
	} 
	//处理后续的
	for(i = 1;i < strlen(str);i ++){
		for(j = str[i - 1] - 'a' + 1 + 1;j < str[i] - 'a' + 1;j ++){
			pos += f(j,strlen(str) - i);
		} 	
	}
	printf("The string's position is：%d\n",pos + 1);
	return 0;
}
