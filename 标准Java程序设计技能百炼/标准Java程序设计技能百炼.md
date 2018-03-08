# 标准Java程序设计技能百炼
## 1、打印500以内完全数

```
//一个数如果恰好等于它的因子（自身除外）之和，则称该数为完全数。如6=1+2+3，则6为完全数。
public class Test {

	//打印500以内的完全数
	public static void main(String[] args) {

		int i, sum, a;
		int max = 500;
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
	            System.out.printf("%8d",a);
	        a++;
	    }while(a<max);
	    System.out.println();
	}

}
```
## 2、寻找负数
```
package demo;

import java.util.Scanner;

public class Test1 {

	public static void main(String[] args) {
		int i, j;
		int[][] num;
		num = new int[4][6];
	    System.out.printf("Enter 24 integers:\n");
	    Scanner scan = new Scanner(System.in);
	    
	    for(i=0; i < 4; i++)
	        for(j=0; j < 6; j++)
	            num[i][j] = scan.nextInt();
	    scan.close();
	    for(i=0; i < 4; i++)
	        for(j=0; j < 6; j++)
	            if(num[i][j] < 0) {
	            	System.out.printf("minus number num[%d][%d]: %d\n", i, j, num[i][j]);
	            	return;
	            }
	    System.out.printf("Not found !\n");
	}
}
```
## 天数判断
```
package demo;

import java.util.Scanner;

public class Test2 {

	public static void main(String[] args) {
		int day, month, year, sum, leap;
		sum = 0;
	    System.out.printf("Please input year, month, day\n");
	    Scanner scan = new Scanner(System.in);
	    year = scan.nextInt();
	    month = scan.nextInt();
	    day = scan.nextInt();
	    scan.close();
	    
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
	    default: System.out.printf("data error !");
	    }
	    sum += day;
	    if(year%400==0||(year%4==0&&year%100!=0))
	        leap = 1;
	    else 
	        leap = 0;
	    if(leap==1&&month>2)
	        sum ++;
	    System.out.printf("It is the %dth day.\n", sum);
	}
}
```
## 猜数字
```
package demo;

import java.io.IOException;
import java.util.Random;
import java.util.Scanner;

public class Test3 {

	public static void main(String[] args) throws IOException {
		
		int count, number,guess;
	    String yes = "Y";
	    System.out.printf("Now let us play the game.\nGuess the number:\n");
	    Scanner scan = new Scanner(System.in);
	    while(yes.equals("Y") || yes.equals("y"))
	    {
	        count = 0;
	        Random rand = new Random();
	        number = rand.nextInt(100)+1;
	        
	        do
	        {
	            do
	            {
	                System.out.printf("Input an interger number(1-100):\n");
	                guess = scan.nextInt();
	            }while(!(guess>=1&&guess<=100));
	            if(guess<number)
	            	System.out.printf("Your answer is LOW , try again.\n");
	            if(guess>number)
	            	System.out.printf("Yuor answer is HIGH , try again.\n");
	             count++;
	            if(count == 15)
	            {
	            	System.out.printf("This is the %d times ! Think it hard next!\n", count);
	            	break;
	            }
	        }while(!(guess == number));
	        if(count <= 7)
	        {
	        	System.out.printf("You have got it in %d times.\n", count);
	        	System.out.printf("Congretulations!\n");
	        }
	        else
	        {
	        	System.out.printf("You got it in %d times.\n",count);
	        	System.out.printf("I bet you can do it better!\n");
	        }
	        System.out.printf("NEXT?(Y/N):\n");
	        scan.nextLine();
	        yes = scan.nextLine();
	    }
	    scan.close();
    }
}
```
## 按位排序
```
package demo;

import java.util.Scanner;

public class Test4 {

	public static void main(String[] args) {
		long x, y;
	    int i, a[]=new int[5];
	    Scanner scan = new Scanner(System.in);
	    x = scan.nextLong();
	    scan.close();
	    if((x<10000)||(x>99999))
	    {
	        System.out.printf("This data is error !\n");
	        return;
	    }
	    for(i = 0; i<5; ++i)
	    {
	        a[i] = (int) (x%10);
	        x = x/10;
	    }
	    fun(a);
	    y =0;
	    for(i = 0; i < 5; ++i)
	        y=y*10+a[i];
	    System.out.printf("%d", y);
	    System.out.printf("\n");
	}
	static void fun(int a[])
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
}
```
## li18数组逆转
```
package demo;

//li18数组逆转
public class Test5 {

	private static int N = 20;
	
	public static void main(String[] args) {
		
		int a[] = {9,6,5,4,1,23,21,22,26,3,2,0,8,7,67,68,34,2,88,34};
	    int i, temp;
	    System.out.printf("original array: \n");
	    for(i =0; i < N; i++)
	    	System.out.printf("%4d", a[i]);
	    for(i = 0; i < N/2; i++)
	    {
	        temp = a[i];
	        a[i] = a[N-i-1];
	        a[N-i-1] = temp;
	    }
	    System.out.printf("\nsorted array: \n");
	    for(i = 0; i < N; i ++)
	    	System.out.printf("%4d", a[i]);
	    System.out.printf("\n");
	}
}
```
## li19折半查找
```
package demo;

import java.util.Scanner;

//li19折半查找
public class Test6 {

	static Scanner scan = new Scanner(System.in);
	
	public static void main(String[] args) {
		int i,n, a[]=new int[100];
	    System.out.printf("Input the total number[1~100]:");
	    n = scan.nextInt();
	    System.out.printf("Input %d numbers: \n", n);
	    for(i = 0; i < n; i ++)
	    	a[i] = scan.nextInt();
	    
	    System.out.printf("The original orders are: ");
	    for(i = 0; i < n; i ++)
	    	System.out.printf("%7d", a[i]);
	    System.out.printf("\n");
	    selectsort(a, n);
	    halfind(a, n);
	    scan.close();
	}

	static void selectsort (int a[], int n)
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
	    System.out.printf("The sorted numbers are:");
	    for(i = 0; i < n; i ++)
	    	System.out.printf("%7d", a[i]);
	    System.out.println();
	}
	static void halfind(int a[], int n)
	{
	    int  k, find = 0, first = 0, last = (n-1), half;
	    System.out.printf("Input the number to look for: ");
	    k = scan.nextInt();
	    do
	    {
	        half = (first + last)/2;
	        if(k == a[half])
	        {
	        	System.out.printf("Find %d, it is a[%d].\n", k, half);
	            find = 1;
	        }
	        else
	            if(k >a[half])
	                first = half + 1;
	            else
	                last = half - 1;
	    }while((first<=last)&&(find==0));
	    if(find==0)
	    	System.out.printf("%d not been found!\n", k);
	}
}
```
## li22魔方阵
```
package demo;

//li22魔方阵
public class Test7 {

	static int N = 9;
	
	public static void main(String[] args) {
		int i, j, k, a[][]=new int[N][N];
	    for(i=0; i<N; i++)
	        for(j=0; j<N; j++)
	            a[i][j] = 0;
	    j = N/2;
	    a[0][j] = 1;
	    for(k=2; k<=N*N; k++)
	    {
	        i--;
	        j++;
	        if(i<0) {
	        	i=N-1;
	        }

        	if(j>N-1)
                j=0;
        
	        if(a[i][j]==0) {
	            a[i][j]=k;
	        }
	        else
	        {
	            i=(i+2)%N;
	            j=(j-1+N)%N;
	            a[i][j]=k;
	        }
	    }
	    System.out.printf("\n");
	    for(i=0; i<N; i++)
	    {
	    	System.out.printf("\t");
	        for(j=0; j<N; j++)
	        	System.out.printf("%4d", a[i][j]);
	        System.out.printf("\n");
	    }
	}
}
```
## li25成绩统计
```
package demo;

import java.util.Scanner;

public class Test8 {

	static int N = 8;
	static Scanner scan = new Scanner(System.in);
	
	public static void main(String[] args) {
		int x, num[]=new int[N+1];
	    float st[]=new float[N+1], ave, sum=0;
	    for(x=1; x<=N; x++) {
	    	num[x] = scan.nextInt();
	    	st[x] = scan.nextFloat();
	    }
	    for(x=1; x<=N; x++)
	        sum+=st[x];
	    ave=sum/N;
	    System.out.printf("average is: %f\n", ave);
	    for(x=1; x<=N; x++)
	        if(st[x]>=ave)
	            System.out.printf("%d\t%f\n", num[x], st[x]);
	    scan.close();
	}
}
```
## li26二维数组每行最大值提取
```
package demo;

public class Test9 {

	public static void main(String[] args) {
		int x, y, p, t;
	    int a[][]={{9,8,7,11},{4,6,2,1},{25,3,19,10}};
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
	            System.out.printf("%d\t", a[x][y]);
	        System.out.printf("\n");
	    }
	}
}
```
## li27汉诺塔问题
```
package demo;

import java.util.Scanner;

//li27汉诺塔问题
public class Test10 {

	private static Scanner scan = new Scanner(System.in);
	public static void main(String[] args) {
		int m;
	    System.out.printf("input the number of diskes:");
	    m = scan.nextInt();
	    System.out.printf("The step to moving %3d diskes:", m);
	    hanio(m, 'a', 'b', 'c');
	    scan.close();
	}
	
	/**
	 * 
	 * @param n 盘子的数量
	 * @param origin 源座
	 * @param assist 辅助座
	 * @param destination 目的座
	 */
	static void hanio(int n, char origin, char assist, char destination)
	{
	    if(n==1)
	    	System.out.printf("%c->%c\n", origin, destination);
	    else
	    {
	    	//将上面n-1个盘子移动到辅助座
	        hanio(n-1, origin, destination, assist);
	        //将最底层的盘子移动到目的座
	        System.out.printf("%c->%c\n", origin, destination);
	        //将辅助座的n-1个盘子移动到目的座
	        hanio(n-1, assist, origin, destination);
	    }
	}
}
```
## li29学生成绩检查
```
package demo;

//li29学生成绩检查
public class Test11 {
	static float score[][]={{65,80,78,90},{98,89,100,83},{92,56,59,70},{78,63,80,70},{64,55,70,81}};
    
	public static void main(String[] args) {
	    search(score, 5);
	}
	
	static void search( float p[][], int m) {
	    int i, j, flag;
	    for(i=0; i<m; i++)
	    {
	        flag = 0; 
	        for(j=0; j<4; j++)
	        {
	            if( p[i][j]<60 )
	                flag=1;
	            if(flag==1)
	            {
	                System.out.printf("Np.%d is flunked, score are:\n", i+1);
	                for(j=0; j<4; j++)
	                	System.out.printf("%5.1f", p[i][j] );
	                System.out.printf("\n");
	            }
	        }
	    }
	}
}
```
## li30奇偶函数调用
```
package demo;

import java.util.Scanner;

//li30奇偶函数调用，接口与类代替C语言指针来实现函数调用功能。
public class Test12 {

	public interface method {
		public float fun(int n);
	}
	
	public static class peven implements method{

		@Override
		public float fun(int n) {
			float s;
		    int i;
		    s=0;
		    for(i=2; i<=n; i+=2)
		        s+=1/(float)i;
		    return s;
		}
		
	}
	
	public static class podd implements method {

		@Override
		public float fun(int n) {
			float s;
		    int i;
		    s=0;
		    for(i=1; i<=n; i+=2)
		        s+=1/(float)i;
		    return s;
		}	
	}
	
	private static Scanner scan = new Scanner(System.in);
	public static void main(String[] args) {
	    float sum;
	    int n;
	    
	    while(true) {
	        n = scan.nextInt();
	        if(n>1) break;
	    }
	    if(n%2==0)
	    {
	        System.out.printf("Even=");//1/2+1/4+1/6+...
	        sum=dcall(new peven(), n);
	    }
	    else
	    {
	        System.out.printf("Odd=");
	        sum=dcall(new podd(), n);//1/1+1/3+1/5+...
	    }
	    System.out.printf("%f\n", sum);
	    scan.close();
	}
	
	static float dcall(method m, int n) {
	    float s;
	    s=m.fun(n);
	    return s;
	}
}
```
## li31万年历
```
package demo;

import java.util.Scanner;

//li31万年历
public class Test13 {

	private static Scanner scan = new Scanner(System.in);
	
	public static void main(String[] args) {
		int i, day, year, temp,temp_i;
	    long Year_days=0;
	    int Year_Start=1;
	    int Per_Year_Days;
	    int month_day[]={31,28,31,30,31,30,31,31,30,31,30,31,29};
	    System.out.printf("Please enter the year: ");
	    year = scan.nextInt();
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
		        case 1: System.out.printf("    January(%d)\n", year); break;
		        case 2: System.out.printf("    February(%d)\n", year); break;
		        case 3: System.out.printf("    March(%d)\n", year); break;
		        case 4: System.out.printf("    April(%d)\n", year); break;
		        case 5: System.out.printf("    May(%d)\n", year); break;
		        case 6: System.out.printf("    June(%d)\n", year); break;
		        case 7: System.out.printf("    July(%d)\n", year); break;
		        case 8: System.out.printf("    August(%d)\n", year); break;
		        case 9: System.out.printf("    September(%d)\n", year); break;
		        case 10: System.out.printf("    October(%d)\n", year); break;
		        case 11: System.out.printf("    November(%d)\n", year); break;
		        case 12: System.out.printf("    December(%d)\n", year); break;
	        }
	        i=(int) (Year_days%7);
	        System.out.printf("Mon Tue Wed Thu Fri Sat Sun\n");
	        if(i!=0)
	            for(temp_i=0; temp_i<i; temp_i++)
	            	System.out.printf("    ");
	        day=1;
	        if(IsLeapYear(year)&&temp==2) {
	        	while(day<=month_day[12])
	            {
	                if( day > 1 )
	                    if(Year_days%7==0)
	                    	System.out.printf("\n");
	                if(day >= 10)
	                	System.out.printf("%d  ", day);
	                else
	                	System.out.printf("%d   ", day);
	                Year_days++;
	                day++;
	            }
	        } else {
	        	while(day<=month_day[temp-1])
                {
                    if(day>1)
                        if(Year_days%7==0)
                        	System.out.printf("\n");
                    if(day>=10)
                    	System.out.printf("%d  ", day);
                    else
                    	System.out.printf("%d   ", day);
                    Year_days++;
                    day++;
                }
	        }
	                
    		System.out.printf("\n");
            if(scan.nextLine().equals("q"))
                break;
	    }
	    scan.close();
	}
	static boolean IsLeapYear(int year)
	{
	    if(((year%4==0)&&(year%100!=0))||(year%400==0))
	        return true;
	    else 
	        return false;
	}
}
```
## li33求最小值
```
package demo;

import java.util.Scanner;

public class Test14 {

	private static Scanner scan = new Scanner(System.in);
	public static void main(String[] args) {
		int a, b, c, m;
	    System.out.printf("input three intergers:");
	    a = scan.nextInt();
	    b = scan.nextInt();
	    c = scan.nextInt();
	    m=min3(a,b,c);
	    System.out.printf("min is %d\n", m);
	    scan.close();
	}

	static int min2(int x, int y)
	{
	    int z;
	    z=x<y?x:y;
	    return z;
	}
	static int min3(int x, int y, int z)
	{
	    int w;
	    w=min2(x, y);
	    w=min2(w, z);
	    return w;
	}
}
```
## li34求三角函数
```
package demo;

import java.util.Scanner;

//li34求三角函数
public class Test15 {

	private static Scanner scan = new Scanner(System.in);
	
	public interface method {
		public double fun(double data);
	}
	
	public static class sin implements method{

		@Override
		public double fun(double data) {
			return Math.sin(data);
		}
		
	}
	
	public static class cos implements method{

		@Override
		public double fun(double data) {
			return Math.cos(data);
		}
		
	}
	
	public static class tan implements method{

		@Override
		public double fun(double data) {
			return Math.tan(data);
		}
		
	}
	
	public static void main(String[] args) {
		String fun;
		int i, j=1;
	    System.out.printf("input sin or cos or tan: ");
	    fun = scan.nextLine();
	    method m = null;
	    switch(fun) {
		    case "sin": m = new sin();break;
		    case "cos": m = new cos();break;
		    case "tan": m = new tan();break;
		    default: j = 0;break;
	    }
	    
	    if(j==0)
	    	System.out.printf("input error!");
	    else
	        for(i=0; i<5; i++)
	        	System.out.printf("\n%3d%8.3f", (i+1)*10, m.fun(3.1415*(i+1)/18));
	    System.out.printf("\n");
	}

}
```
## li35求阶乘倒数之和
```
package demo;

//li35求阶乘倒数之和
public class Test16 {

	public static void main(String[] args) {
		int n;
	    float e, p;
	    e=(float) 1.0;
	    p=(float) 1.0;
	    for(n=1; n<=10; n++)
	    {
	        p*=n;
	        e+=1.0/p;
	    }
	    System.out.printf("e=%10.7f\n", e);
	
	}

}
```
## li36求一元二次方程的根
```
package demo;

import java.util.Scanner;

//li36求一元二次方程的根
public class Test17 {
	private static Scanner scan = new Scanner(System.in);
	public static void main(String[] args) {
		float a, b, c, p, x1, x2, t1, t2;
	    a = scan.nextFloat();
	    b = scan.nextFloat();
	    c = scan.nextFloat();
	    if(a==0&&b==0)
	        System.out.printf("unsolvable.\n");
	    else
	        if(a==0&&b!=0)
	        	System.out.printf("the single root is %f\n", -c/b);
	        else
	            if(a!=0)
	            {
	                p=b*b-4*a*c;
	                t1=-b/(2*a);
	                t2=(float) (Math.sqrt(Math.abs(p))/(2*a));
	                if(p<0)
	                {
	                	System.out.printf("complex root:\n");
	                	System.out.printf("%8.4f+%8.4fi\n", t1, t2);
	                	System.out.printf("%8.4f-%8.4fi\n", t1, t2);
	                }
	                else
	                {
	                    x1=t1+t2;
	                    x2=t1-t2;
	                    System.out.printf("realroot:\n");
	                    System.out.printf("%8.4f and %8.4f\n", x1, x2);
	                }
	            }
	    scan.close();
	}
}
```
## li37加法练习
```
package demo;

import java.util.Random;
import java.util.Scanner;

//li37加法练习
public class Test18 {
	private static Scanner scan = new Scanner(System.in);
	public static void main(String[] args) {
		int a, b, c, x=0;
	    while(x<5)//和在100以内的加法，连对5次通过
	    {
	    	Random rand = new Random();
	    	a = rand.nextInt(100)+1;
	    	b = rand.nextInt(100)+1;
	        if((a+b)>100)
	            continue;
	        System.out.printf("\n%d+%d=?  ", a, b);
	        c = scan.nextInt();
	        if(c==a+b)
	        {
	        	System.out.printf("The answer is right ");
	            x++;
	        }
	        else
	        {
	        	System.out.printf("The answer is wrong !");
	            x=0;
	        }
	    }
	    System.out.printf("\nProgram is over.\n");
	    scan.close();
	}
}
```
## 获取环境变量和系统属性
```
package demo;

import java.util.Iterator;
import java.util.Map;

//获取环境变量和系统属性
public class Test19 {

	public static void main(String[] args) {
		Map<String, String> mapEnv = System.getenv();//环境变量
		for(Iterator<String> itr = mapEnv.keySet().iterator();itr.hasNext();){
            String key = itr.next();
            System.out.println(key + "=" + mapEnv.get(key));
        }
		
		Map<Object, Object> mapPro = System.getProperties();//系统属性
        for(Iterator<Object> itr = mapPro.keySet().iterator();itr.hasNext();){
            String key = (String) itr.next();
            System.out.println(key + "=" + mapPro.get(key));
        }
	}
}
```
## li40转置矩阵
```
package demo;

import java.util.Scanner;

//li40转置矩阵
public class Test20 {

	private static int N = 5;
	private static Scanner scan = new Scanner(System.in);
	
	public static void main(String[] args) {
		int n, i, j;
	    int x[][] = new int[N][N];
	    System.out.printf("input n:");
	    n = scan.nextInt();
	    for(i=0; i<n; i++)
	        for(j=0; j<n; j++)
	        	x[i][j] = scan.nextInt();
	    transp(x,n);
	    for(i=0; i<n; i++)
	    {
	        for(j=0; j<n; j++)
	        	System.out.printf("   %d", x[i][j]);
	        System.out.printf("\n");
	    }
	    scan.close();
	}
	
	static void transp(int a[][], int n)
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
}
```
## li42正整数个数统计
```
package demo;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

//li42正整数个数统计
public class Test21 {

	private static final int MAX = 100;
	private static int xx[] = new int[MAX];
	private static int totnum = 0;
	private static int totcnt = 0;
	private static double totpjz = 0.0;
	
	public static void main(String[] args) throws IOException {
		if(readdat())
	    {
	        System.out.printf("the file cann't open!\007\n");
	        return;
	    }
	    calvalue();
	    System.out.printf("the totnum is %d\n", totnum);
	    System.out.printf("the totcnt is %d\n", totcnt);
	    System.out.printf("the totpjz is %.2f\n", totpjz);
	    writedat();
	}
	private static void calvalue()
	{
	    int i;
	    int j;
	    long val=0;
	    for(i=0; i<MAX; i++)
	        if(xx[i]>0) totnum++;    //正整数个数统计
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
	private static boolean readdat() throws IOException
	{
	    File file = new File("in.txt");

	    BufferedReader in = new BufferedReader(new FileReader(file));
	    int i=0;

	    String line;
	    while((line=in.readLine()) != null)
	    {
	    	String[] temp = line.split(" ");
	    	for (int j=0; j<temp.length; j++)
	        xx[i++] = Integer.parseInt(temp[j]);
	    }
	    in.close();
	    return false;
	}

	private static void writedat() throws IOException
	{
	    File file = new File("my4.txt");
	    FileWriter out = new FileWriter(file);
	    for (int i=0; i<xx.length; i++)
	    	out.write(xx[i]+" ");
	    out.write("\r\n");
	    out.write("totnum="+totnum+"\ntotcnt="+totcnt+"\ntotpjz="+totpjz);
	    out.close();
	}
}
```
## 二维数组的文件读写
```
package demo;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

//二维数组的文件读写
public class FileRW {

	public static void main(String[] args) throws IOException {
		int array[][] = {{1,2,3},{4,5,6},{7,8,9}};
		//array写入filein.txt
		File file = new File("filein.txt");
		FileWriter out = new FileWriter(file);
		for (int i=0; i<array.length; i++) {
			for (int j=0; j<array[i].length; j++)
				out.write(array[i][j]+"\t");
			out.write("\n");
		}
		out.flush();
		out.close();
		
		BufferedReader br = new BufferedReader(new FileReader(file));
		String line = null;
		int row = 0;
		int arr[][] = new int[3][3];
		while((line=br.readLine()) != null) {
			String[] temp = line.split("\t");
			for (int i=0; i<temp.length; i++)
				arr[row][i] = Integer.parseInt(temp[i]);
			row++;
		}
		br.close();
		System.out.println();
	}
}
```
## li43电报处理
```
package demo;

import java.util.Scanner;

//li43电报处理
public class Test22 {

	private static boolean CHANGE = false;
	private static Scanner scan = new Scanner(System.in);
	
	public static void main(String[] args) {
		String str;
	    char c;
	    int i=0;
	    System.out.printf("please input some word:");
	    str = scan.nextLine();
	    char[] charStr = str.toCharArray();
	    while(i<charStr.length)
	    {
	    	c = charStr[i];
	        i++;
	        if (CHANGE) {
	        	if((c>='A'&&c<'Z')||c>='a'&&c<'z')
		            c++;
		        if((c=='Z')||(c=='z'))
		            c=(char) (c-25);
	        }
	        
			System.out.printf("%c", c);
	    }
	    System.out.printf("\n");
	}
}
```
## li44字符串统计
```
package demo;

import java.util.Scanner;

//li44字符串统计
public class Test23 {

	private static Scanner scan = new Scanner(System.in);
	public static void main(String[] args) {
		int up=0, low=0, digit=0, space=0, other=0;
	    String str;

	    System.out.printf("the string:\n");
	    str = scan.nextLine();
	    char[] p = str.toCharArray();
	    int i = 0;
	    while(i < p.length)
	    {
	        if((p[i]>='A')&&(p[i]<='Z'))
	            up++;
	        else if((p[i]>='a')&&(p[i]<='z'))
	            low++;
	        else if(p[i]==' ')
	            space++;
	        else if((p[i]>='0')&&(p[i]<='9'))
	            digit++;
	        else
	            other++;
	        i++;
	    }
	    System.out.printf("digit letter:%d\nup letter:%d\nlow letter:%d\nspace letter:%d\nother letter:%d\n", digit, up, low, space, other);
		scan.close();
	}
}
```
## 冒泡排序
```
package demo;

import java.util.Scanner;

//li45数字排序
public class Test24 {

	private static Scanner scan = new Scanner(System.in);
	
	public static void main(String[] args) {
		int N = 20;
		int i, j;
	    float a[]=new float[N], temp;
	    int endi = 0;
	    int times = 0;
	    System.out.printf("Input %d numbers\n", N);

	    for(i=0; i<N; i++)
	    	a[i] = scan.nextFloat();
	    boolean isend = false;
	    for (i=N-1; i>0 && !isend; i--) {
	    	isend = true;
	    	for (j=0; j<i; j++) {
	    		if (a[j] > a[j+1]) {
	    			isend = false;
	    			temp = a[j];
	    			a[j] = a[j+1];
	    			a[j+1] = temp;
	    		}
	    		times++;//比较次数
	    	}
	    	endi = i;//已经排好序的数组下标
	    }

	    for(i=0; i<N; i++)
	    {
	        if(i%5==0)
	        	System.out.printf("\n");
	        System.out.printf("%8.3f", a[i]);
	    }
	    System.out.printf("\n");
	    System.out.printf("endi=%d times=%d\n", endi, times);
	    scan.close();
	}
}
/*
 * 有无isend优化的对比，举例
 * 数据集:
1 2 3 4 32
37 5 47 64 86
12 35 8 58 65
77 78 79 80 81
 * 未优化运行结果：
   1.000   2.000   3.000   4.000   5.000
   8.000  12.000  32.000  35.000  37.000
  47.000  58.000  64.000  65.000  77.000
  78.000  79.000  80.000  81.000  86.000
endi=1 times=190
 * 优化后运行结果：
   1.000   2.000   3.000   4.000   5.000
   8.000  12.000  32.000  35.000  37.000
  47.000  58.000  64.000  65.000  77.000
  78.000  79.000  80.000  81.000  86.000
endi=12 times=124
 */
```
## li46数字插入
```
package demo;

import java.util.Scanner;

//li46数字插入
public class Test25 {
	
	private static Scanner scan = new Scanner(System.in);
	
	public static void main(String[] args) {
		int N = 10;
		Integer a[]=new Integer[12];
		int p, x;
		for (int i=1; i<=N; i++)
			a[i] = scan.nextInt();
		x = scan.nextInt();
		BubbleSortUtil.IntegerBubbleSort ibs = new BubbleSortUtil.IntegerBubbleSort();
		ibs.SubSort(a, 1, N);
	    p=1; 
	    while(x>a[p]&&p<=N)
	        p++;
	    for(int i=N; a[i]>=a[p]; i--)
	    	a[i+1] = a[i];
	    a[p] = x;
	    
	    for(int i=1; i<=N+1; i++)
	        System.out.printf("%5d", a[i]);
	    System.out.printf("\n");
	    scan.close();
	}
}
/*
 * 数据集：
32 42 12 23 66 43 77 89 54 6
8
 * 运行结果： 
 endi=1 times=45
    6   12   23   32   33   42   43   54   66   77   89
 * */

```
#### 以上代码调用冒泡排序工具类BubbleSortUtil源码如下。
```
package demo;

public class BubbleSortUtil {
	
	public static class FloatBubbleSort extends BubbleSort<Float> {

		@Override
		boolean compare(Float a, Float b) {
			return (a>b);
		}
		
	}
	
	public static class IntegerBubbleSort extends BubbleSort<Integer> {

		@Override
		boolean compare(Integer a, Integer b) {
			return (a>b);
		}
		
		void SubSort(Integer a[], int left, int right) {
			Integer b[] = new Integer[right-left+1];
			for (int i=left; i<=right; i++)
				b[i-left] = a[i];
			super.sort(b);
			for (int i=left; i<=right; i++)
				a[i] = b[i-left];
		}
		
	}
	
	private static abstract class BubbleSort<T> {
		
		abstract boolean compare(T a, T b);
		
		public void sort(T a[]) {
			boolean isend = false;
			T temp;
			int i, j;
			int times = 0, endi = 0;
		    for (i=a.length-1; i>0 && !isend; i--) {
		    	isend = true;
		    	for (j=0; j<i; j++) {
		    		if (compare(a[j],a[j+1])) {
		    			isend = false;
		    			temp = a[j];
		    			a[j] = a[j+1];
		    			a[j+1] = temp;
		    		}
		    		times++;//比较次数
		    	}
		    	endi = i;//已经排好序的数组下标
		    }
		    System.out.printf("endi=%d times=%d\n", endi, times);
		}
	}
}
```
## li47求矩阵最值
```
package demo;

import java.util.Scanner;

//li47求矩阵最值
public class Test26 {
	
	private static Scanner scan = new Scanner(System.in);

	public static void main(String[] args) {
		int N1 = 3, N2 = 4;
		int a[][] = new int[N1][N2];
		int max, min;
	    int i, j, row1, row2, column1, column2;
	    row1=row2=column1=column2=0;

	    for(i=0; i<N1; i++)
	        for(j=0; j<N2; j++)
	        	a[i][j] = scan.nextInt();
	    max=min=a[0][0];
	    for(i=0; i<N1; i++)
	        for(j=0; j<N2; j++)
	        {
	            if(max<a[i][j])
	            {
	                max=a[i][j];
	                row1=i;
	                column1=j;
	            }
	            if(min>a[i][j])
	            {
	                min=a[i][j];
	                row2=i;
	                column2=j;
	            }
	        }
	    System.out.printf("max=%d\trow1=%4d column1=%4d\n", max, row1+1, column1+1);
	    System.out.printf("min=%d\trow2=%4d column2=%4d\n", min, row2+1, column2+1);
	    scan.close();
	}
}
/*
53 42 4 66
43 7 54 21
6 5 9 28
max=66	row1=   1 column1=   4
min=4	row2=   1 column2=   3 
 * */
```
## li48优秀学生统计
```
package demo;

import java.util.Scanner;

//li48优秀学生统计
public class Test27 {

	private static Scanner scan = new Scanner(System.in);
	private static int M = 5, N = 4;
	
	public static void main(String[] args) {
		
		int i, j;
	    int score[][] = new int[M][N];
	    for(i=0; i<M; i++)
	    {
	        System.out.printf("Input %d score of No.%d:\n", N, i+1);
	        for(j=0; j<N; j++)
	        	score[i][j] = scan.nextInt();
	    }
	    search(score);
	    scan.close();
	}

	private static void search(int[][] score)
	{
	    int i, j, flag;
	    for(i=0; i<M; i++)
	        for(j=0; j<N; j++)
	        {
	            flag=0;
	            if(score[i][j]>=90)
	                flag=1;
	            if(flag==1)
	            {
	                System.out.printf("No.%d is excellence, score are:", (i+1));
	                for(j=0; j<N; j++)
	                	System.out.printf("%5d", score[i][j]);
	                System.out.printf("\n");
	            }
	        }
	}
}
/*
Input 4 score of No.1:
66 77 88 99
Input 4 score of No.2:
71 73 76 79
Input 4 score of No.3:
82 84 85 89
Input 4 score of No.4:
61 72 83 94
Input 4 score of No.5:
99 88 77 66
No.1 is excellence, score are:   66   77   88   99
No.4 is excellence, score are:   61   72   83   94
No.5 is excellence, score are:   99   88   77   66
 * */
```
## li49字符串排序
```
package demo;

import java.util.Scanner;

public class Test28 {

	private static Scanner scan  = new Scanner(System.in);
	private static int N = 10;
	
	public static void main(String[] args) {
		
		int i;
	    String[] s = new String[N];

	    System.out.printf("Input %d strings:\n", N);
	    for(i=0; i<N; i++)
	    	s[i] = scan.nextLine();
	    BubbleSortUtil.StringBubbleSort sbs = new BubbleSortUtil.StringBubbleSort();
	    sbs.sort(s);
	    
	    System.out.printf("The sorted string are:\n");
	    for(i=0; i<N; i++)
	        System.out.println(s[i]);
	    scan.close();
	}
}
/*
Input 10 strings:
lide
chenyan
LiDe
ChenYan
abc
def
ABC
DEF
abcdef
ABCEDF
endi=1 times=45
The sorted string are:
ABC
ABCEDF
ChenYan
DEF
LiDe
abc
abcdef
chenyan
def
lide
 * */
```
#### 在之前冒泡排序工具类BubbleSortUtil中增加String类型的排序类StringBubbleSort 
```
public static class StringBubbleSort extends BubbleSort<String> {

	@Override
	boolean compare(String a, String b) {
		return a.compareTo(b)>0;
	}
	
}
```
## li50计算定积分
```
package demo;

//li50计算定积分
public class Test29 {

	private static int N = 1000;
	
	public static void main(String[] args) {
		double y;
		fbds fun = new fbds();
	    y=Integration(0.0, 2.0, fun);
	    System.out.printf("y= %6.2f\n", y);
	    
	    OneElementTwoOrderPolynomial oetop = new OneElementTwoOrderPolynomial(1.0,0.0,1.0);
	    y=Integration(0.0, 2.0, oetop);
	    System.out.printf("y= %6.2f\n", y);
	}
	
	private static class fbds implements Fun {

		@Override
		public double fun(double x) {
			return (1.0+x+x*x*x);
		}
		
	}
	
	private static class OneElementTwoOrderPolynomial implements Fun {
		
		private double a, b, c;
		
		private OneElementTwoOrderPolynomial(double a, double b, double c) {
			this.a = a;
			this.b = b;
			this.c = c;
		}
		@Override
		public double fun(double x) {
			return (c+b*x+a*x*x);
		}
		
	}
	
	public interface Fun {
		double fun(double x);
	}
	
	private static double Integration(double d, double e, Fun fn)
	{
	    int i;
	    double h, s;
	    h=(e-d)/N;
	    s=(fn.fun(d)+fn.fun(e))/2.0;
	    for(i=0; i<N; i++)
	        s+=fn.fun(d+i*h);
	    return (s*h);
	}
}
```
## li53师生信息储存
```
package demo;

import java.util.Scanner;

//li53师生信息储存
public class Test30 {

	private static final int N = 5;
	private static final Scanner scan = new Scanner(System.in);
	
	public static void main(String[] args) {
		Info[] info = new Info[N];
	    int i;
	    for(i=0; i<N; i++)
	    {
	    	info[i] = new Info();
	        System.out.printf("Input name:\n");
	        info[i].name = scan.nextLine();
	        System.out.printf("Input age:\n");
	        info[i].age = scan.nextInt();
	        System.out.printf("Input sex(m/w):");
	        if(scan.hasNextLine()) scan.nextLine();
	        info[i].sex = scan.nextLine().charAt(0);
	        System.out.printf("Input jobs(s/t):");
	        info[i].job = scan.nextLine().charAt(0);
	        if(info[i].job=='s')
	        {
	        	System.out.printf("Input class:\n");
	        	info[i].depart = new Info.Depart();
	        	info[i].depart.classes = scan.nextInt();
	        }
	        else if(info[i].job=='t')
	        {
	        	System.out.printf("Input office:");
	        	info[i].depart = new Info.Depart();
	        	info[i].depart.office = scan.nextLine();
	        }
	        else
	        {
	        	System.out.printf("Input wrong job, return!");
	            i--;
	        }
	        if(scan.hasNextLine()) scan.nextLine();
	    }
	    System.out.printf("\n name \t\t age \t sex \t job \tdepart ");
	    for(i=0; i<N; i++)
	    {
	        if(info[i].job=='s')
	        	System.out.printf("\n %-15s %-3d \t %c \t %-6c %-20d", info[i].name, info[i].age,
	            info[i].sex, info[i].job, info[i].depart.classes);
	        else
	        	System.out.printf("\n %-15s %-3d \t %c \t %-6c %-20s", info[i].name, info[i].age,
	            info[i].sex, info[i].job, info[i].depart.office);
	    }
	    System.out.printf("\n");
	    scan.close();
	}
	
	private static class Info {
		String name;
        int age;
        char sex;
        char job;
        Depart depart;
        public static class Depart
        {
            int classes;
            String office;
        };
	}
}
/*
Input name:
a1
Input age:
12
Input sex(m/w):m
Input jobs(s/t):s
Input class:
1
Input name:
a2
Input age:
13
Input sex(m/w):w
Input jobs(s/t):t
Input office:o1

Input name:
a3
Input age:
14
Input sex(m/w):m
Input jobs(s/t):s
Input class:
2
Input name:
a4
Input age:
15
Input sex(m/w):m
Input jobs(s/t):s
Input class:
3
Input name:
a5
Input age:
31
Input sex(m/w):w
Input jobs(s/t):t
Input office:o3


 name 		 age 	 sex 	 job 	depart 
 a1              12  	 m 	 s      1                   
 a2              13  	 w 	 t      o1                  
 a3              14  	 m 	 s      2                   
 a4              15  	 m 	 s      3                   
 a5              31  	 w 	 t      o3   
 * *
 */
```
## li54创建链表
```
package demo;

import java.util.Scanner;

import demo.LinkedListUtil.LinkedList;

//li54创建链表
public class Test31 {
	
	private static final Scanner scan = new Scanner(System.in);
	
	public static void main(String[] args) {
	    LinkedList list=create();
	    list.display();
	}
	
	private static class Elements {
		String no;
	    int score;
	    
	    @Override
	    public String toString() {
	    	return "{no:"+no+", score:"+score+"}";
	    }
	}
	
	private static LinkedList create() {
	    LinkedList list = new LinkedList();
	    int count=0;
	    Elements e;
	    for(;;)
	    {
	        System.out.printf("Input the number of student No.%d(6 bytes): ", count+1);
	        e = new Elements();
	        e.no = scan.nextLine();
	        if(e.no.equals("000000"))
	        {
	            break;
	        }
	        System.out.printf("Input the score of the student No.%d: ", count+1);
	        e.score = scan.nextInt();
	        count++;
	        list.insertFirst(e);
	        scan.nextLine();
	    }
	    return list;
	}
}
/*
Input the number of student No.1(6 bytes): 123456
Input the score of the student No.1: 99
Input the number of student No.2(6 bytes): 121212
Input the score of the student No.2: 98
Input the number of student No.3(6 bytes): 000000
{no:121212, score:98}
{no:123456, score:99}
 * *
 */
```
#### li54创建链表引用了自定义链表工具类LinkedList，源码如下
```
package demo;

public class LinkedListUtil {
	private static class Data {
		private Object object;
	   	private Data next = null;
	   	
	   	Data(Object obj) {
	   		this.object = obj;
	   	}
	}
	
	public static class LinkedList {
		private Data first = null;

		public void insertFirst(Object obj) {
			Data data = new Data(obj);
			data.next = first;
			first = data;
		}
		public Object deleteFirst() throws Exception {
			if (first == null)
				throw new Exception("empty!");
			Data data = first;
			first = first.next;
			return data.object;
		}
		public boolean find(Object obj) throws Exception {
			if (first == null)
				throw new Exception("empty!");
			Data cur = first;
			while(cur != null) {
				if (cur.object.equals(obj))
					return true;
				cur = cur.next;
			}
			return false;
		}
		public void remove(Object obj) throws Exception {
			if (first == null)
				throw new Exception("empty!");
			if (first.object.equals(obj)) {
				first = first.next;
			} else {
				Data cur = first.next;
				Data pre = first;
				while( cur != null) {
					if (cur.object.equals(obj)) {
						pre.next = cur.next;
						cur = null;
					}
					pre = cur;
					cur = cur.next;
				}
			}
		}
		public boolean isEmpty() {
			return (first==null);
		}
		public void display() {
			Data cur = first;
			while (cur != null) {
				System.out.println(cur.object.toString());
				cur = cur.next;
			}
		}
	}
}
```
## li55整数统计
```
package demo;

import java.util.Iterator;
import java.util.LinkedList;
import java.util.Scanner;

//li55整数统计
public class Test32 {

	private static final Scanner scan = new Scanner(System.in);
	
	public static void main(String[] args) {
		LinkedList<Elements> list = new LinkedList<Elements>();
	    long k;
	    System.out.printf("Input natural number,-1 to end:\n");
	    k = scan.nextLong();
	    while(k>=0)
	    {
	        add(k, list);
	        k = scan.nextLong();
	    }
	    for (int i=0; i<list.size(); i++) {
	    	System.out.println(list.get(i).toString());
	    }
	}

	public static class Elements {
		long key;
		int count;
		@Override
		public String toString() {
			return "{key:"+key+",count:"+count+"}";
		}
	}
	
	private static void add(long key, LinkedList<Elements> list) {
		if (list.isEmpty()) {
			Elements e = new Elements();
			e.key = key;
			e.count = 1;
			list.add(e);
		} else {
			Iterator<Elements> it = list.iterator();
			int index = 0;
			while(it.hasNext()) {
				Elements e = it.next();
				if (e.key == key) {
					e.count++;
					list.set(index, e);
					break;
				}
				index++;
			}
			if (index == list.size()) {
				Elements e = new Elements();
				e.key = key;
				e.count = 1;
				list.add(e);
			}
		}
		
	}
}
/*
Input natural number,-1 to end:
2
3
4
32
2
5
43
4
3
65
45
76
76
87
56
-1
{key:2,count:2}
{key:3,count:2}
{key:4,count:2}
{key:32,count:1}
{key:5,count:1}
{key:43,count:1}
{key:65,count:1}
{key:45,count:1}
{key:76,count:2}
{key:87,count:1}
{key:56,count:1}
 * *
 */
```
