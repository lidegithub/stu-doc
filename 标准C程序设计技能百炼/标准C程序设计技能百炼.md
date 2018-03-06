# 标准C程序设计技能百炼
## li12完全数

```
//一个数如果恰好等于它的因子（自身除外）之和，则称该数为完全数。如6=1+2+3，则6为完全数。
#include <stdio.h>

int main(void)
{
    int i, sum, a;
    a = 2;
    do
    {
        i = 1;
        sum = 0;
        do
        {
            if(a%i==0)
                sum += i;
            i++;
        }while(i <= a/2);
        if(sum == a)
            printf("%4d",a);
        a++;
    }while(a<500);
    putchar('\n');
    return 0;
}
```
## li13寻找负数
```
#include <stdio.h>

int main()
{
    int i, j, num[4][6];
    printf("Enter 24 integers:\n");

    for(i=0; i < 4; i++)
        for(j=0; j < 6; j++)
            scanf("%d",&num[i][j]);
    for(i=0; i < 4; i++)
        for(j=0; j < 6; j++)
            if(num[i][j] < 0) goto found;
    printf("Not found !\n");
    goto done;
    found:
          printf("minus number num[%d][%d]: %d\n", i, j, num[i][j]);
    done:
    return 0;
}
```
## li14天数判断
```
#include <stdio.h>

int main()
{
    int day, month, year, sum, leap;
    printf("Please input year, month, day\n");
    scanf("%d,%d,%d", &year, &month, &day);

    switch(month)
    {
    case 1: sum = 0; break;
    case 2: sum = 31; break;
    case 3: sum = 59; break;
    case 4: sum = 90; break;
    case 5: sum = 120; break;
    case 6: sum = 151; break;
    case 7: sum = 181; break;
    case 8: sum = 212; break;
    case 9: sum = 243; break;
    case 10: sum = 273; break;
    case 11: sum = 304; break;
    case 12: sum = 334; break;
    default: printf("data error !");
    }
    sum += day;
    if(year%400==0||(year%4==0&&year%100!=0))
        leap = 1;
    else 
        leap = 0;
    if(leap==1&&month>2)
        sum ++;
    printf("It is the %dth day.\n", sum);
    return 0;
}
```
## li15猜数字
```
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <time.h>

int main()
{
    int count, number,guess;
    char yes = 'Y';
    printf("Now let us play the game.\nGuess the number:\n");
    while(toupper(yes)=='Y')
    {
        count = 0;
        srand(time(0));
        number = rand()/100+1;
        do
        {
            do
            {
                printf("Input an interger number(1-100):\n");
                scanf("%d", &guess);
            }while(!(guess>=1&&guess<=100));
            if(guess<number)
                printf("Your answer is LOW , try again.\n");
            if(guess>number)
                printf("Yuor answer is HIGH , try again.\n");
             count++;
            if(count == 15)
            {
                printf("This is the %d times ! Think it hard next!\n", count);
                exit(0);
            }
        }while(!(guess == number));
        if(count <= 7)
        {
            printf("You have got it in %d times.\n", count);
            printf("Congretulations!\n");
        }
        else
        {
            printf("You got it in %d times.\n",count);
            printf("I bet you can do it better!\n");
        }
        printf("NEXT?(Y/N):\n");
        scanf(" %c", &yes);
    }
    return 0;
}
```
## li16按位排序
```
#include <stdio.h>

int main()
{
    long int x, y;
    int i, a[5];
    scanf("%ld", &x);
    if((x<10000)||(x>99999))
    {
        printf("This data is error !\n");
        exit(0);
    }
    for(i = 0; i<5; ++i)
    {
        a[i] = x%10;
        x = x/10;
    }
    fun(a);
    y =0;
    for(i = 0; i < 5; ++i)
        y=y*10+a[i];
    printf("%ld", y);
    printf("\n");
    return 0;
}
fun(int a[])
{
    int i, j, k;
    for(i = 0; i < 5; ++i)
        for(j = i; j < 5; ++j)
            if(a[j] < a[i])
            {
                k = a[i];
                a[i] = a[j];
                a[j] = k;
            }
}
```
## li18数组逆转
```
#include <stdio.h>
#define N 20

int main()
{
    int a[N] = {9,6,5,4,1,23,21,22,26,3,2,0,8,7,67,68,34,2,88,34};
    int i, temp;
    printf("original array: \n");
    for(i =0; i < N; i++)
        printf("%4d", a[i]);
    for(i = 0; i < N/2; i++)
    {
        temp = a[i];
        a[i] = a[N-i-1];
        a[N-i-1] = temp;
    }
    printf("sorted array: \n");
    for(i = 0; i < N; i ++)
        printf("%4d", a[i]);
    printf("\n");
    return 0;
}
```
## li19折半查找
```
#include <stdio.h>

void selectsort (int a[], int n)
{
    int i, j, k, num;
    for(i = 0; i < n-1; i ++)
    {
        k = i;
        for(j = i+1; j < n; j ++)
            if(a[j]<a[k])
                k = j;
        if(k!=i)
        {
            num = a[k];
            a[k] = a[i];
            a[i] = num;
        }
    }
    printf("The sorted numbers are:");
    for(i = 0; i < n; i ++)
        printf("%7d", a[i]);
    putchar('\n');
}
void halfind(int a[], int n)
{
    int  k, find = 0, first = 0, last = (n-1), half;
    printf("Input the number to look for: ");
    scanf("%d", &k);
    do
    {
        half = (first + last)/2;
        if(k == a[half])
        {
            printf("Find %d, it is a[%d].\n", k, half);
            find = 1;
        }
        else
            if(k >a[half])
                first = half + 1;
            else
                last = half - 1;
    }while((first<=last)&&(find==0));
    if(find==0)
        printf("%d not been found!\n", k);
}
int main()
{
    int i,n, a[100];
    printf("Input the total number[1~100]:");
    scanf("%d", &n);
    printf("Input %d numbers: \n", n);
    for(i = 0; i < n; i ++)
        scanf("%d", &a[i]);
    printf("The original orders are: ");
    for(i = 0; i < n; i ++)
        printf("%7d", a[i]);
    printf("\n");
    selectsort(a, n);
    halfind(a, n);
    //printf("\n");
    return 0;
}
```
## li22魔方阵
```
#include <stdio.h>
#define N 9

int main()
{
    int i, j, k, a[N][N];
    for(i=0; i<N; i++)
        for(j=0; j<N; j++)
            a[i][j] = 0;
    j = N/2;
    a[0][j] = 1;
    for(k=2; k<=N*N; k++)
    {
        i--;
        j++;
        if(i<0)
            i=N-1; 
		if(j>N-1)
			j=0;
        if(a[i][j]==0)
            a[i][j]=k;
        else
        {
            i=(i+2)%N;
            j=(j-1+N)%N;
            a[i][j]=k;
        }
    }
    printf("\n");
    for(i=0; i<N; i++)
    {
        printf("\t");
        for(j=0; j<N; j++)
            printf("%4d", a[i][j]);
        printf("\n");
    }
    return 0;
}
```
## li25成绩统计
```
#define N 8
#include <stdio.h>

int main()
{
    int x, num[N+1];
    float st[N+1], ave, sum=0;
    for(x=1; x<=N; x++)
        scanf("%d%f",&num[x], &st[x]);
    for(x=1; x<=N; x++)
        sum+=st[x];
    ave=sum/N;
    printf("average is: %f\n", ave);
    for(x=1; x<=N; x++)
        if(st[x]>=ave)
            printf("%d\t%f\n", num[x], st[x]);
    return 0;
}
```
## li26二维数组每行最大值提取
```
#include <stdio.h>

int main()
{
    int x, y, p, t;
    int a[3][4]={{9,8,7,11},{4,6,2,1},{25,3,19,10}};
    //ÌáÈ¡Ã¿ÐÐ×î´óÖµ
    for(x=0; x<=2; x++)
    {
        p=0;
        for(y=1; y<=3; y++)
            if(a[x][y]>a[x][p])
                p=y;
        t=a[x][0];
        a[x][0]=a[x][p];
        a[x][p]=t;
    }
    for(x=0; x<=2; x++)
    {
        for(y=0; y<=3; y++)
            printf("%d\t", a[x][y]);
        printf("\n");
    }
    return 0;
}
```
## li27汉诺塔问题
```
#include <stdio.h>

hanio(int n, char x, char y, char z)
{
    if(n==1)
        printf("%c->%c\n", x, z);
    else
    {
        hanio(n-1, x, z, y);
        printf("%c->%c\n", x, z);
        hanio(n-1, y, x, z);
    }
}

int main()
{
    int m;
    printf("input the number of diskes:");
    scanf("%d", &m);
    printf("The step to moving %3d diskes:", m);
    hanio(m, 'a', 'b', 'c');
    return 0;
}
```
## li29学生成绩检查
```
#include <stdio.h>

int main()
{
    void search(float(*p)[4], int m);
    static float score[5][4]={{65,80,78,90},{98,89,100,83},{92,56,78,70},{78,63,80,70},{64,55,70,81}};
    search(score, 5);
    return 0;
}
void search( float (*p)[4], int m)
{
    int i, j, flag;
    for(i=0; i<m; i++)
    {
        flag = 0; 
        for(j=0; j<4; j++)
        {
            if( *( *(p+i)+j )<60 )
                flag=1;
            if(flag==1)
            {
                printf("Np.%d is flunked, score are:\n", i+1);
                for(j=0; j<4; j++)
                    printf("%5.1f", *(*(p+i)+j) );
                printf("\n");
            }
        }
    }
}
```
## li30奇偶函数调用
```
#include <stdio.h>

int main()
{
    float peven(), podd(), dcall();
    float sum;
    int n;
    while(1)
    {
        scanf("%d", &n);
        if(n>1) break;
    }
    if(n%2==0)
    {
        printf("Even=");//1/2+1/4+1/6+...
        sum=dcall(peven, n);
    }
    else
    {
        printf("Odd=");
        sum=dcall(podd, n);//1/1+1/3+1/5+...
    }
    printf("%f\n", sum);
    return 0;
}

float peven(int n)
{
    float s;
    int i;
    s=1;
    for(i=2; i<=n; i+=2)
        s+=1/(float)i;
    return (s);
}

float podd(n)
int n;
{
    float s;
    int i;
    s=0;
    for(i=1; i<=n; i+=2)
        s+=1/(float)i;
    return (s);
}

float dcall(fp, n)
float (*fp)();
int n;
{
    float s;
    s=(*fp)(n);
    return (s);
}
```
## li31万年历
```
#include <stdio.h>

int IsLeapYear(int);
int main()
{
    int i, day, year, temp,temp_i;
    long int Year_days=0;
    int Year_Start=1;
    int Per_Year_Days;
    int month_day[]={31,28,31,30,31,30,31,31,30,31,30,31,29};
    printf("Please enter the year: ");
    scanf("%d", &year);
    while(Year_Start < year)
    {
        if(IsLeapYear(Year_Start))
            Per_Year_Days=366;
        else
            Per_Year_Days=365;
        //输入年份的起始天数，用于确定第一天是星期几
        Year_days=Year_days+Per_Year_Days;
        Year_Start++;
    }
    for(temp=1; temp<=12; temp++)
    {
        switch( temp )
        {
        case 1: printf("    February(%d)\n", year); break;
        case 2: printf("    February(%d)\n", year); break;
        case 3: printf("    March(%d)\n", year); break;
        case 4: printf("    April(%d)\n", year); break;
        case 5: printf("    May(%d)\n", year); break;
        case 6: printf("    June(%d)\n", year); break;
        case 7: printf("    July(%d)\n", year); break;
        case 8: printf("    August(%d)\n", year); break;
        case 9: printf("    September(%d)\n", year); break;
        case 10: printf("    October(%d)\n", year); break;
        case 11: printf("    November(%d)\n", year); break;
        case 12: printf("    December(%d)\n", year); break;
        }
        i=Year_days%7;
        printf("Mon Tue Wed Thu Fri Sat Sun\n");
        if(i!=0)
            for(temp_i=0; temp_i<i; temp_i++)
                printf("    ");
        day=1;
        if(IsLeapYear(year)&&temp==2)
            while(day<=month_day[12])
            {
                if( day > 1 )
                    if(Year_days%7==0)
                        printf("\n");
                if(day >= 10)
                    printf("%d  ", day);
                else
                    printf("%d   ", day);
                Year_days++;
                day++;
            }
            else
                while(day<=month_day[temp-1])
                {
                    if(day>1)
                        if(Year_days%7==0)
                            printf("\n");
                    if(day>=10)
                        printf("%d  ", day);
                    else
                        printf("%d   ", day);
                    Year_days++;
                    day++;
                }
                printf("\n");
                if(getch()=='q')
                    exit(0);
    }
    return 0;
}

int IsLeapYear(int year)
{
    if(((year%4==0)&&(year%100!=0))||(year%400==0))
        return 1;
    else 
        return 0;
}
```
## li32汉诺塔
```
#include <stdio.h>

hanio(int n, char x, char y, char z)
{
    if(n==1)
        printf("%c->%c\n", x, z);
    else
    {
        hanio(n-1, x, z, y);
        printf("%c->%c\n", x, z);
        hanio(n-1, y, x, z);
    }
}

int main()
{
    int m;
    printf("input the number of diskes:");
    scanf("%d", &m);
    printf("The step to moving %3d diskes:", m);
    hanio(m, 'a', 'b', 'c');
    return 0;
}
```
## li33求最小值
```
#include <stdio.h>

int main()
{
    int a, b, c, m;
    int min3();
    printf("input three intergers:");
    scanf("%d %d %d", &a, &b, &c);
    m=min3(a,b,c);
    printf("min is %d\n", m);
    return 0;
}

int min2(int x, int y)
{
    int z;
    z=x<y?x:y;
    return z;
}
int min3(int x, int y, int z)
{
    int w;
    w=min2(x, y);
    w=min2(w, z);
    return w;
}
```
## li34求三角函数
```
#include <stdio.h>
#include <math.h>
#include <string.h>

int main()
{
    char ch[20];
    int i, j=1;
    double(*f) ();
    printf("input sin or cos or tan: ");
    scanf("%s", ch);
    if(!strcmp(ch, "sin"))
        f=sin;
    else 
        if(!strcmp(ch, "cos"))
            f=cos;
        else
            if(!strcmp(ch, "tan"))
                f=tan;
            else j=0;
    if(j==0)
        printf("input error!");
    else
        for(i=0; i<5; i++)
            printf("\n%3d%8.3f", (i+1)*10, (*f)(3.1415*(i+1)/18));
    printf("\n");
    return 0;
}
```
## li35求阶乘倒数之和
```
#include <stdio.h>

int main()
{
    int n;
    float e, p;
    e=p=1.0;
    for(n=1; n<=10; n++)
    {
        p*=n;
        e+=1.0/p;
    }
    printf("e=%10.7f\n", e);
    return 0;
}
```
## li36求一元二次方程的根
```
#include <stdio.h>
#include <math.h>

int main()
{
    float a, b, c, p, x1, x2, t1, t2;
    scanf("%f,%f,%f", &a, &b, &c);
    if(a==0&&b==0)
        printf("unsolvable.\n");
    else
        if(a==0&&b!=0)
            printf("the single root is %f\n", -c/b);
        else
            if(a!=0)
            {
                p=b*b-4*a*c;
                t1=-b/(2*a);
                t2=sqrt(fabs(p))/(2*a);
                if(p<0)
                {
                    printf("complex root:\n");
                    printf("%8.4f+%8.4fi\n", t1, t2);
                    printf("%8.4f-%8.4fi\n", t1, t2);
                }
                else
                {
                    x1=t1+t2;
                    x2=t1-t2;
                    printf("realroot:\n");
                    printf("%8.4f and %8.4f\n", x1, x2);
                }
            }
    return 0;
}
```
## li37加法练习
```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int a, b, c, x=0;
    while(x<5)//和在100以内的加法，连对5次通过
    {
        a=rand( )%100;
        b=rand( )%100;
        if((a+b)>100)
            continue;
        printf("\n%d+%d=?  ", a, b);
        scanf("%d", &c);
        if(c==a+b)
        {
            printf("The answer is right ");
            x++;
        }
        else
        {
            printf("The answer is wrong !");
            x=0;
        }
    }
    printf("\nProgram is over.\n");
    return 0;
}
```
## li38检查系统鼠标
```
#include <stdio.h>
#include <stdlib.h>//包含库函数exit()
#include <string.h>
void loadmous(void);

int main(void)
{
    loadmous();
    return 0;
}

void loadmous()
{
    char *p;
    if((p=getenv("MOUSE"))!=NULL)//调用系统变量函数判断有无鼠标
    {
        if(!strcmp(p, "YES"))
            printf("Mouse is OK\n");
    }
    else
    {
        printf("\n No mouse\n");
    }
}
```
## li40转置矩阵
```
#include <stdio.h>
#define N 5

void transp(int a[][N], int n)
{
    int i, j, k;
    for(i=0; i<n; i++)
        for(j=0; j<i; j++)
        {
            k=a[i][j]; 
            a[i][j]= a[j][i];
            a[j][i]=k;
        }
}
int main()
{
    int n, i, j;
    int x[N][N];
    printf("input n:");
    scanf("%d", &n);
    for(i=0; i<n; i++)
        for(j=0; j<n; j++)
            scanf("%d", &x[i][j]);
    transp(x,n);
    for(i=0; i<n; i++)
    {
        for(j=0; j<n; j++)
            printf("   %d", x[i][j]);
        printf("\n");
    }
    return 0;
}
```
## li41pc信息显示
```
#include <stdio.h>
#include <conio.h>
#include <ctype.h>
#include <stdlib.h>

void main()
{
    char letter;
    do
    {
        printf("A Display directory listing \n");
        printf("B Display disk information\n");
        printf("C Change system date\n");
        printf("Q Quit\n");
        printf("Chioce:");
        letter=getchar();
        letter=toupper(letter);
        switch(letter)
        {
        case'A': system("DIR"); break;
        case'B': system("CHKDSK"); break;
        case'C': system("DATE"); break;
        }
    }while(letter!='Q');
}
```
## li42正整数个数统计
```
#include <stdio.h>
#include <conio.h>
#define MAX 100
int xx[MAX];
int totnum=0;
int totcnt=0;
double totpjz=0.0;
int readdat(void);
void writedat(void);
void calvalue(void)
{
    int i;
    int j;
    long val=0;
    for(i=0; i<MAX; i++)
        if(xx[i]) totnum++;    //正整数个数统计
    for(i=0; i<totnum; i++)
    {
        j=(xx[i]>>1);          //所有数右移一位
        if(j%2==0)
        {
            totcnt++;       //经处理后其中偶数个数统计
            val+=xx[i];
        }
    }
    totpjz=(double)val/totcnt;  //求这些偶数平均值
}

int main(void)
{
    if(readdat())
    {
        printf("the file cann't open!\007\n");
        return 0;
    }
    calvalue();
    printf("the totnum is %d\n", totnum);
    printf("the totcnt is %d\n", totcnt);
    printf("the totpjz is %.2lf\n", totpjz);
    writedat();
    return 0;
}

int readdat(void)
{
    FILE *fp;
    int i=0;
    if((fp=fopen("in.txt", "r"))==NULL)
        return 1;
    while(!feof(fp))
    {
        fscanf(fp, "%d", &xx[i++]);
    }
    fclose(fp);
    return 0;
}

void writedat(void)
{
    FILE *fp;
    fp=fopen("my4.txt", "w");
    fprintf(fp, "%d\n%d\n%.2lf\n", totnum, totcnt, totpjz);
    fclose(fp);
}
```
## li43电报处理
```
#include <stdio.h>
#define CHANGE 1

int main()
{
    char str[100];
    char c;
    int i=0;
    printf("please input some word:");
    scanf("%s", &str);
    while((c=str[i])!='\0')
    {
        i++;
#if CHANGE
        if((c>='A'&&c<'Z')||c>='a'&&c<'z')
            c++;
        if((c=='Z')||(c=='z'))
            c=c-25;
#endif 
        printf("%c", c);
    }
    printf("\n");
    return 0;
}
```
## li44字符串统计
```
#include <stdio.h>
#define N 100

int main()
{
    int up=0, low=0, digit=0, space=0, other=0;
    char *p, s[N];

    printf("the string:\n");
    p=s;
    gets(p);
    while(*p!='\0')
    {
        if((*p>='A')&&(*p<='Z'))
            up++;
        else if((*p>='a')&&(*p<='z'))
            low++;
        else if(*p==' ')
            space++;
        else if((*p>='0')&&(*p<='9'))
            digit++;
        else
            other++;
        p++;
    }
    printf("up letter:%d\nlow letter:%d\nspace letter:%d\nother letter:%d\n", up, low, space, other);
    return 0;
}
```
## li45数字排序
```
#include <stdio.h>
#define N 20

int main()
{
    int i, j;
    float a[N], temp, *p;
    p=a;
    printf("Input %d numbers\n", N);

    for(i=0; i<N; i++)
        scanf("%f", p+i);
    for(i=0; i<N-1; i++)
        for(j=i+1; j<N; j++)
            if(*(p+i)<*(p+j))
            {
                temp=*(p+i);
                *(p+i)=*(p+j);
                *(p+j)=temp;
            }
    for(i=0; i<N; i++)
    {
        if(i%5==0)
            printf("\n");
        printf("%8.3f", *(p+i));
    }
    printf("\n");
    return 0;
}
```
## li46数字插入
```
#include <stdio.h>
#define N 10

int main()
{
    int a[12], p, x, *t;
    for(t=a+1; t<=a+N; t++)
        scanf("%d", t);
    scanf("%d", &x);
    t=a; 
    p=1; 
    while(x>*(t+p)&&p<=N)
        p++;
    for(t=a+N; t>=a+p; t--)
        *(t+1)=*t;
    t=a+p;
    *t=x;
    for(t=a+1; t<=a+N+1; t++)
        printf("%5d",*t);
    printf("\n");
    return 0;
}
```
## li47求矩阵最值
```
#include <stdio.h>
#define N1 3
#define N2 4

int main()
{
    int a[N1][N2], max, min, (*ap)[N2];
    int i, j, row1, row2, column1, column2;
    ap=a;
    row1=row2=column1=column2=0;

    for(i=0; i<N1; i++)
        for(j=0; j<N2; j++)
            scanf("%d", *(ap+i)+j);
    max=min=a[0][0];
    for(i=0; i<N1; i++)
        for(j=0; j<N2; j++)
        {
            if(max<*(*(ap+i)+j))
            {
                max=*(*(ap+i)+j);
                row1=i;
                column1=j;
            }
            if(min>*(*(ap+i)+j))
            {
                min=*(*(ap+i)+j);
                row2=i;
                column2=j;
            }
        }
    printf("max=%d\trow1=%4d column1=%4d\n", max, row1+1, column1+1);
    printf("min=%d\trow2=%4d column2=%4d\n", min, row2+1, column2+1);
    return 0;
}
```
## li48优秀学生统计
```
#include <stdio.h>
#define N 4   //科目数
#define M 5   //学生数
void search(int (*p)[N])
{
    int i, j, flag;
    for(i=0; i<M; i++)
        for(j=0; j<N; j++)
        {
            flag=0;
            if(*(*(p+i)+j)>=90)
                flag=1;
            if(flag==1)
            {
                printf("No.%d is excellence, score are:", (i+1));
                for(j=0; j<N; j++)
                    printf("%5.1d", (*(*(p+i)+j)));
                printf("\n");
            }
        }
}

int main()
{
    int i, j;
    int score[M][N];
    for(i=0; i<M; i++)
    {
        printf("Input %d score of No.%d:\n", N, i+1);
        for(j=0; j<N; j++)
            scanf("%d", &score[i][j]);
    }
    search(score);
    return 0;
}
```
## li49字符串排序
```
#include <stdio.h>
#include <string.h>
#define LENGTH 30
#define N 10
void  sort(char **p)
{
    int i, j;
    char *pstr;

    for(i=0; i<N; i++)
        for(j=i+1; j<N; j++)
            if(strcmp(*(p+i),*(p+j))>0)
            {
                pstr=*(p+j);
                *(p+j)=*(p+i);
                *(p+i)=pstr;
            }
}

int main()
{
    int i;
    char *pstr[N];
    char s[N][LENGTH];
    for(i=0; i<N; i++)
        pstr[i]=s[i];
    printf("Input %d strings:\n", N);
    for(i=0; i<N; i++)
        gets(pstr[i]);
    sort(pstr);
    printf("The sorted string are:\n");
    for(i=0; i<N; i++)
        puts(pstr[i]);
    return 0;
}
```
## li50计算定积分
```
#include <stdio.h>
#define N 10000

int main()
{
    float y;
    float fbds(float);
    float jifen(float, float, float(*fun)(float));
    y=jifen(0.0, 2.0, fbds);
    printf("y= %6.2f\n", y);
    return 0;
}

float fbds(float x)
{
    return (1.0+x+x*x*x);
}
float jifen(float a, float b, float(*fun)(float))
{
    int i;
    float h, s;
    h=(b-a)/N;
    s=((*fun)(a)+(*fun)(b))/2.0;
    for(i=0; i<N; i++)
        s+=(*fun)(a+i*h);
    return (s*h);
}
```
## li53师生信息储存
```
#include <stdio.h>
#define N 5
#define M 20

int main()
{
    struct
    {
        char name[M];
        int age;
        char sex;
        char job;
        union
        {
            int class;
            char office[M];
        }depart;
    }info[N];
    int i;
    for(i=0; i<N; i++)
    {
        printf("Input name:\n");
        gets(info[i].name);
        printf("Input age:\n");
        scanf("%d", &info[i].age);
        getchar();
        printf("Input sex(m/w):");
        info[i].sex=getchar();
        getchar();
        printf("Input jobs(s/t):");
        info[i].job=getchar();
        getchar();
        if(info[i].job=='s')
        {
            printf("Input class:\n");
            scanf("%d", &info[i].depart.class);
            getchar();
        }
        else if(info[i].job=='t')
        {
            printf("Input office:");
            gets(info[i].depart.office);
        }
        else
        {
            printf("Input wrong job, return!");
            i--;
        }
    }
    printf("\n name \t\t age \t sex \t job \tdepart ");
    for(i=0; i<N; i++)
    {
        if(info[i].job=='s')
            printf("\n %-15s %-3d \t %c \t %-6c %-20d", info[i].name, info[i].age,
            info[i].sex, info[i].job, info[i].depart.class);
        else
            printf("\n %-15s %-3d \t %c \t %-6c %-20s", info[i].name, info[i].age,
            info[i].sex, info[i].job, info[i].depart.office);
    }
    printf("\n");
    return 0;
}
```
## li54创建链表
```
#include <stdio.h>
#include <string.h> 
#include <stdlib.h>
#define LEN sizeof(struct grade)
struct grade
{
    char no[7];
    int score;
    struct grade *next;
};
struct grade *create(void)
{
    struct grade *head=NULL, *new, *tail;
    int count=0;
    for(;;)
    {
        new=(struct grade *)malloc(LEN);
        printf("Input the number of student No.%d(6 bytes): ", count+1);
        scanf("%6s", new->no);
        if(strcmp(new->no, "000000")==0)
        {
            free(new);
            break;
        }
        printf("Input the score of the student No.%d: ", count+1);
        scanf("%d", &new->score);
        count++;
        new->next=NULL;
        if(count==1)
            head=new;
        else
            tail->next=new;
        tail=new;
    }
    return (head);
}

int main()
{
    struct grade *head;
    head=create();
    return 0;
}
```
## li55整数统计
```
#include <stdio.h>
#include <stdlib.h>
#define LENGTH sizeof(struct number)
struct number
{
    long key;
    int count; 
    struct number *next;
};
struct number *add(long k, struct number *head)
{
    int flag=1;
    struct number *p=head;
    while(p!=NULL&&flag==1)
    {
        if(p->key==k)
            flag=0;
        else 
            p=p->next;
    }
    if(flag==0)
        p->count++;
    else
    {
        p=head;
        head=(struct number *)malloc(LENGTH);
        head->key=k;
        head->count=1;
        head->next=p;
    }
    return(head);
}
void list(struct number *p)
{
    printf("The result are:\n");
    while(p!=NULL)
    {
        printf("%16ld %6d\n", p->key, p->count);
        p=p->next;
    }
}

int main()
{
    struct number *head=NULL;
    long k;
    printf("Input natural number,-1 to end:\n");
    scanf("%ld", &k);
    while(k>=0)
    {
        head=add(k, head);
        scanf("%ld", &k);
    }
    list(head);
    return 0;
}
```
## 报数游戏
```
#define N 18
#define M 3
#include <stdio.h>

int main()
{
    int a[N], k=0, i, j;
    printf("The original orders are: \n");
    for(i=0; i<N; i++)
    {
        a[i] = i+1;
        printf("%3d", a[i]);
    }
    printf("\n");
    for(i=0; k<N*M; i++)
    {
        if(a[i%N]!=-1)
        {
            k++;
            if(k%3==0)
            {
                a[i%N]=-1;
                printf("\n%2d is out!", (i%N+1));
                if(k!=N*3)
                    printf("The new order is:");
                else 
                    printf("The game is over!");
                for(j=0; j<N; j++)
                {
                    if(a[j]!=-1)
                        printf("%3d", a[j]);
                }
            }
        }
    }
    return 0;
}
```
## 猜座位
```
# include <stdio.h>

int main(void)
{
    int i,j,k,m,p;
    char xwei[5],side[10];
    char ch[10]={'B','A','C','E','A','B','D','C','E','D'};
    xwei[0]='A';
    for(i=1;i<=5;i++)
    {
        xwei[i]='B';
        for(j=1;j<5;j++)
            if(j!=i)
            {
                xwei[j] = 'C';
                for(k=1;k<5;k++)
                if(k!=i&&k!=j)
                {
                    xwei[k]='D';
                    xwei[10-i-j-k]='E';
                    for(p=0;p<5;p++)
                    {
                        side[2*p]=xwei[(p+1)%5];
                        side[2*p+1]=xwei[(p+4)%5];
                    }
                    for(p=0,m=0;p<10;p+=2)
                    {
                        if((side[p]==ch[p])+(side[p+1]==ch[p+1])==1)
                            m++;
                    }
                    if(m==5)
                    {
                        printf("The order is:");
                        for(p=0;p<5;p++)
                            printf("%2d %c",(p+1),xwei[p]);
                    }
                }

            }
    }
    printf("\n");
    return 0;
}
```
## 打印菱形图案
```
#include <stdio.h>

int main(void)
{
    int i,j;
    for(i=0;i<4;i++)
    {
        for(j=0;j<4-i;j++)
            printf(" ");
        for(j=0;j<i;j++)
            printf("*");
        printf("\n");
    }
    for(i=0;i<4;++i)
    {
        for(j=0;j<i;j++)
            printf(" ");
        for(j=0;j<4-i;j++)
            printf("*");
        printf("\n");
    }
    return 0;
}
```
## 打印孪生素数
```
#include <stdio.h>

int main(void)
{
    int k,n,isprime(int);
    n=0;
    k=2;
    while(n<15)
    {
        if(isprime(k)&&isprime(k+2))
        {
            n=n+1;
            printf("%d,%d\n",k,k+2);
        }
        k=k+1;
    }
    return 0;
}
int isprime (int a)
{
    int k,j;
    j=1;
    k=2;
    while((k<=a/2)&&j)
    {
        if(a%k==0)
            j=0;
        else 
            k=k+1;
    }
    return(j);
}
```
## 个人所得税计算
```
#include <stdio.h>

int main(void)
{
    float a,b;
    int i;
    printf("input one number:");
    scanf("%f",&a);
    if(a>=4000)
        i=4;
    else
        i=a/1000;
    switch(i)
    {
    case 0:b=a*0.0;break;
    case 1:b=a*0.05;break;
    case 2:b=a*0.10;break;
    case 3:b=a*0.15;break;        
    case 4:b=a*0.20;break;
    }
    printf("%f\n",b);
    return 0;
}
```
## 奖金发放问题
```
#include <stdio.h>

int main(void)
{
    long int i;
    int bonus1,bonus2,bonus4,bonus6,bonus10,bonus;
    printf("Please input company's income： ");
    scanf("%ld",&i);
    bonus1=100000*0.1;
    bonus2=bonus1+100000*0.075;
    bonus4=bonus2+200000*0.05;
    bonus6=bonus4+200000*0.03;
    bonus10=bonus6+400000*0.015;
    if(i<=100000)
        bonus=i*0.1;
    else
        if(i<=200000)
            bonus=bonus1+(i-100000)*0.075;
        else
            if(i<=400000)
                bonus=bonus2+(i-200000)*0.05;
            else
                if(i<=600000)
                    bonus=bonus4+(i-400000)*0.03;
                else
                    if(i<=1000000)
                        bonus=bonus6+(i-600000)*0.015;
                    else
                        bonus=bonus10+(i-1000000)*0.01;
    printf("bonus=%d\n",bonus);
    return 0;
}
```
## 欧几里得(Euclid)算法
```
#include <stdio.h>

int main(void)
{
    int a,b,x,y,gcd,r,t;
    scanf("%d,%d",&a,&b);
    if(a<b)
    {
        t=a;
        a=b;
        b=t;
    }
    x=a;
    y=b;
    if(y==0) gcd=x;
    else
    {
        do
        {
            r=x%y;
            x=y;
            y=r;
        }
        while(y!=0);
        gcd=x;
    }
    printf("%d,%d的最大公约数为%d\n",a,b,gcd);
    return 0;
}
```
## 求素数
```
#include <stdio.h>
#include <math.h>
#define N 101

int main(void)
{
    int i,j,line,a[N];
    for(i=2;i<N;i++)
        a[i]=i;
    for(i=2;i<sqrt(N);i++)
        for(j=i+1;j<N;j++)
        {
            if(a[i]!=0&&a[j]!=0)
                if(a[j]%a[i]==0)
                    a[j]=0;
        }
    printf("\n");
    for(i=2,line=0;i<N;i++)
    {
        if(a[i]!=0)
        {
            printf("%5d",a[i]);
            line++;
        }
        if(line==10) 
        {printf("\n");
         line=0;
        }
    }
    printf("\n");
    return 0;
}
```
## 数据加密
```
#include <stdio.h>

int main(void)
{
    int a,i,t,aa[4];
    scanf("%d",&a);
    aa[0]=a%10;
    aa[1]=a%100/10;
    aa[2]=a%1000/100;
    aa[3]=a/1000;
    for(i=0;i<=3;i++)
    {
        aa[i]+=5;
        aa[i]%=10;
    }
    for(i=0;i<=3/2;i++)
    {
        t=aa[i];
        aa[i]=aa[3-i];
        aa[3-i]=t;
    }
    for(i=3;i>=0;i--)
        printf("%d",aa[i]);
    printf("\n");
    return 0;
}
```
## 数据解密
```
#include <stdio.h>

int main(void)
{
    int a,i,t,aa[4];
    scanf("%d",&a);
    aa[0]=a%10;
    aa[1]=a%100/10;
    aa[2]=a%1000/100;
    aa[3]=a/1000;
    for(i=0;i<=3/2;i++)
    {
        t=aa[i];
        aa[i]=aa[3-i];
        aa[3-i]=t;
    }
    for(i=0;i<=3;i++)
    {
        aa[i]+=10;
        aa[i]-=5;
    }
    for(i=3;i>=0;i--)
        printf("%d",aa[i]);
    printf("\n");
    return 0;
}
```
## 数据转换
```
#include <stdio.h>

int main(void)
{
    int a = 0, b = 8, k = 1;
    long xa = 0, xb = 0, x1 = 0, x2 = 0;
    printf("Please input the number: \n");
    scanf("%ld", &xa);
    x1 = xa;
    while(x1 != 0)
    {
        x2 += (x1 % 10) * k;
        x1 /= 10;
        k *= a;
    }
    k = 1;
    x1 = x2;
    while(x1 != 0)
    {
        xb += (x1 % b) * k;
        x1 /= b;
        k *= 10;
    }
    printf("%ld(%d)=%ld(%d)=%ld(%d)\n", xa,a,x2,10,xb,b);
    return 0;
}
```
## 水仙花数
```
//水仙花数是指一个三位数，其各位数字的立方和等于该数本身。
#include <stdio.h>

int main(void)
{
    int i,j,k,n;
    printf("water flower'number is:");
    for(n=100;n<1000;n++)
    {
        i=n/100;
        j=n/10%10;
        k=n%10;
        if(i*100+j*10+k==i*i*i+j*j*j+k*k*k)
        {
            printf("%-5d",n);
        }
        //printf("\n");
    }
    printf("\n");
    return 0;
}
```
## 随机数
```
#include <stdio.h>
#define N 10

static unsigned long k = -1;
void startnum(unsigned int seed)
{
    k = seed;
}
unsigned randnum(long n)
{
    k = ((k * 159 + 23) % n) + 1;
    return k;
}

int main(void)
{
    register unsigned int i;
    long n = 0;
    while(!(n>0&&(k>0&&k<65536)))
    {
        printf("Please input two number between 1 and 65535\n");
        scanf("%ld%ld", &k, &n);
        if(n<=0)
            printf("wrong seed!\n");
        if(k<=0||k>=65536)
            printf("wrong max random!\n");
    }
    startnum(n);
    for(i=0;i<N;i++)
        printf("%6u\n",randnum(n));
    return 0;
}
```
## 杨辉三角
```
#include <stdio.h>
#define N 15

int main()
{
    int i, j, n, a[N][N];
    do
    {
        printf("Input n[1-12]:");
        scanf("%d", &n);
    }while(n<1||n>12);
    for(i=0; i<=n; i++)
    {
        a[i][0] = 1;
        a[i][i] = 1;
    }
    for(i=2; i<=n; i++)
        for(j=1; j<i; j++)
            a[i][j]=a[i-1][j-1]+a[i-1][j];
    printf("\n");
    for(i=0; i<=n; i++)
    {
        for(j=0; j<(70-6*i)/2; j++)
            printf(" ");
        for(j=0; j<=i; j++)
            printf("%6d", a[i][j]);
        printf("\n");
    }
    printf("\n");
    return 0;
}
```
## 最大公约数
```
#include <stdio.h>

int main(void)
{
    int x,y,z;
    int gcd(int,int);
    printf("input two integers:\n");
    scanf("%d,%d",&x,&y);
    z=gcd(x,y);
    printf("greatest common divisor is %d\n",z);
    return 0;
}
int gcd(int a,int b)
{
    int t,c;
    if(a<b)
    {
        t=a;
        a=b;
        b=t;
    }
    c=a%b;
    while(c!=0)
    {
        a=b;
        b=c;
        c=a%b;
    }
    return b;
}
```