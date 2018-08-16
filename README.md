# KMP

#include<stdio.h>
#include<stdlib.h>
#include<string.h>
/*KMP*/


int * Next_Array(char *ch);//下标从0开始的数组
int *Optimized_Next_Array(char *ch);
//优化后的Next数组
int KMP_search(char *text, char *ch);
//在主串text中匹配ch
//若ch存在，返回ch在text中的下标
//若不存在，返回-1


int main()
{
	char text[] = "dbcdbdbdddadbaasdd";
	char ch[] = "dbaasdd";
	int flag = 0;
	if ((flag=KMP_search(text, ch)) != -1)
		printf("\nyes[%d]",flag);
	else printf("\nno");
	system("pause");
}

int * Next_Array(char *ch)//下标从0开始的数组
//建立next数组，返回next数组的地址
{
	int i = 0,j=-1;
	int len=strlen(ch);
	int *next = (int *)malloc(sizeof(int)*len);
	if (!next)exit(-1);
	next[0] = -1;
	while (i<len)
	{
		if (j==-1||ch[j]==ch[i])
		{
			++i;
			++j;
			next[i] = j;
		}//if
		else
		{
			j = next[j];
		}//else
	}//while
	for (int i = 0; i < len; ++i)
	{
		printf(" %d", next[i]);
	}//for
	putchar(10);
	return next;
}//Next_Array

int *Optimized_Next_Array(char *ch)
//优化后的Next数组
{
	{
		int i = 0, j = -1;
		int len = strlen(ch);
		int *next = (int *)malloc(sizeof(int)*len);
		if (!next)exit(-1);
		next[0] = -1;
		while (i<len)
		{
			if (j == -1 || ch[j] == ch[i])
			{
				++i;
				++j;
				if (ch[i] == ch[j])
					next[i] = next[j];
				else next[i] = j;
			}//if
			else
			{
				j = next[j];
			}//else
		}//while
		for (int i = 0; i < len; ++i)
		{
			printf(" %d", next[i]);
		}//for
		putchar(10);
		return next;
	}//Next_Array




}

int KMP_search(char *text,char *ch)
//在主串text中匹配ch
//若ch存在，返回ch在text中的下标
//若不存在，返回-1
{
	Next_Array(ch);//test
	int *next = Optimized_Next_Array(ch);
	int i = 0, j = 0;
	int len_ch = strlen(ch);
	int len_text = strlen(text);
	while (j<len_ch&&i<len_text)
	{
		if (text[i] == ch[j]||j==-1)
		{
			++i;
			++j;
		}//if
		else
		{
				j = next[j];
		}
	}//while
	if (j >= strlen(ch))
		return i - j;
	else return - 1;


}
