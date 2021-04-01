# code-arrangement
对以前未上传的代码整理

1、捕鱼分鱼：
#include <stdio.h>
 
int TakeFish(int n);
 
int main(int argc,char const*argv[])
{
    printf("The total number of fish is:%d\n",TakeFish(5));
    return 0;
}
//递归法分鱼 
int TakeFish(int n)
{
	static int i=0;
	
	if(n==1)
	{
		do
		{
			i++;
		} while (i % 5 != 0);
		return (i+1);	
	}
	else
	{
		int a;		
		do
		{
			a = TakeFish(n-1);
		} while (a % 4 != 0);
		return (a / 4 * 5 + 1);
	}
}

2、猜数游戏
#include<stdio.h>
#include<stdlib.h>
#include<time.h>

int main(int argc,char const*argv[])
{
	srand(time(NULL));			//为函数rand()设置随机数种子 
	
	int number = rand() % 100+1;
	int count = 0;
	int a = 0;
	int ret;					//用于保存函数scanf()的返回值 
	
	printf("我已经想好了一个1到100之间的数。");
	do {
		printf("请猜这个1到100之间数：");
		ret = scanf("%d", &a);
		while(ret!=1)			//若输入非法，则重新输入 
		{
			while(getchar()!='\n');		//清除输入缓冲区的非法字符 
			printf("请猜这个1到100之间数：");
			ret = scanf("%d", &a);
		}
		if ( a > number ) {
			printf("你猜的数大了。");
		} else if ( a < number ) {
			printf("你猜的数小了。");
		}
		count ++;
	} while (a != number);
	
	printf("太好了，你用了%d次就猜到了答案。\n", count);
	return 0;
}

3、春季赛晋级规则（内含组合数计算）
#include<stdio.h>
#define TN 17      			//teamnumber=17

unsigned long long C(unsigned int n,unsigned int m); 
unsigned long long Fact(unsigned int n);	

int main(int argc,char const*argv[])
{
	int leastnumber;
	unsigned int m = TN;
	unsigned int k = 2;	
	unsigned long long totalnumber;
	
	totalnumber = C(m,k);	 
	printf("The total number of games is:%llu\n",totalnumber);
	
	int tn=totalnumber;		
	int i;
	
	for(i=TN-1 ; i>(tn/TN) ; i--)
	{
		if(2*i >= ((tn-9*i)-(tn-9*i)/8*6))
		leastnumber=i;
	}
	printf("The least number of winning games is:%d\n",leastnumber);
	return 0;
}

unsigned long long C(unsigned int n,unsigned int m)		
{
	return Fact(n) / (Fact(m)*Fact(n-m));
}

unsigned long long Fact(unsigned int n)		 
{
   if (n == 1 || n == 0)
   return 1;
   else
   return (n*Fact(n-1));
}

4、错将本地变量地址返回案例
#include <stdio.h>

int* f(void);
void g(void);

int main(int argc, char const *argv[])
{
	int *p = f();
	printf("*p = %d\n", *p);
	g();
	printf("*p = %d\n", *p);
	return 0;
}

int* f(void)
{
	int i = 12;
	return &i;
}

void g(void)
{
	int k = 24;
	printf("k = %d\n", k);
}

5、
