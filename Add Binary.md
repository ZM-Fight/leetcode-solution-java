####Add Binary

> Given two binary strings, return their sum (also a binary string).
  For example, a = "11" b = "1" Return "100".

题目翻译: 对于给定的两个二进制数字所表达的字符串，我们求其相加所得到的结果， 根据上例便可得到答案.

题目分析: 我认为这道题所要注意的地方涵盖以下几个方面:
1. 对字符串的操作.
2. 对于加法，我们应该建立一个进位单位，保存进位数值.
3. 我们还要考虑两个字符串如果不同长度会怎样.
4. int 类型和char类型的相互转换.
>时间复杂度:其实这就是针对两个字符串加起来跑一遍，O(n) n代表长的那串字符串长度.



import java.util.Scanner;

public class Main{
	
@SuppressWarnings("resource")
public static void main(String args[]){
	Scanner scanner = new Scanner(System.in);
	
	String stringA = scanner.nextLine().trim();
	String stringB = scanner.nextLine().trim();
	int lengthA = stringA.length();
	int lengthB = stringB.length();
	
	if(lengthA == 0){
		System.out.println(stringB);
		return;
	}
	if(lengthB == 0){
		System.out.println(stringA);
		return;
	}
	
	StringBuilder builder = new StringBuilder();
	int index1 = lengthA-1;
	int index2 = lengthB-1;
	int carry = 0;//进位
	int num = 0;//保留
	
	while(index1>=0 && index2>=0){
		num  = stringA.charAt(index1)-'0'  + stringB.charAt(index2)-'0' +carry;
		carry = num/2;
		num = num%2;
		index1--;
		index2--;
		builder.insert(0, num);
	}
	while(index1 >= 0){
		num  = stringA.charAt(index1)-'0' +carry;
		carry = num/2;
		num = num%2;
		index1--;
		builder.insert(0, num);
	}
	while(index2 >= 0){
		num  = stringB.charAt(index2)-'0' +carry;
		carry = num/2;
		num = num%2;
		index2--;
		builder.insert(0, num+'0');
	}
	if(carry != 0){
		builder.insert(0, carry+'0');
	}
	System.out.println(builder.toString());
	return;
}
}