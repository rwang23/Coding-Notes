## Basic Idea
Euclid to calculate the gcd

```java
public class Euclid {

	public static void main(String[] arg) {
		int result = gcd(16, 8);
		System.out.printf("the gcd is %d \n", result);
	}


	public static int gcd(int p, int q) {
		if (q == 0) return p;
		int r = p % q;
		return gcd(q, r);
	}
}
```

### 递归
递归代码有以下三个特点，违反了就可能得到错误或低效的代码:

* 递归总有一个最简单的情况
* 递归总是尝试去解决一个规模更小的子问题
* 递归调用的父问题域尝试解决的子问题之间不应该有交集

###扩展库
![Java random API](/Users/Des/Documents/Coding/notes/image/java\ random\ api.png)

###类型转换
#####Java内置了一些类以及其静态转换函数

```java
public class Integer{

	static int parseInt(String s){}
	static String toString(int i){}
}

public class Double{
}
```

##### 普林斯顿算法书提供了stdOut库与stdIn

```java
public class StdOut{
	static void print(String s){}
	static void println(String s){}
	static void println(){}
	static void printf(String f){}
}
```

#### 使用StdOut的例子

```java
public class RandomSeq {
	public static void main(String[] arg) {
		int N = Integer.parseInt(arg[0]);
		double lo = Double.parseDouble(arg[1]);
		double hi = Double.parseDouble(arg[2]);
		for (int i = 0; i < N; i++) {
			double x = StdRandom.uniform(lo, hi);
			StdOut.printf("%.2f\n", x);
		}
	}
}

```

##### 使用StdIn的例子

```java
public class Average {
	public static void main(String[] arg) {
		double sum = 0.0;
		int cnt = 0;
		while (!StdIn.isEmpty()) {
			sum += StdIn.readDouble();
			cnt++;
		}
		double avg = sum / cnt;
		StdOut.printf("Average is %.5f\n,avg");
	}
}
```
#### 使用StdDraw

![StdDraw](/Users/Des/Documents/Coding/notes/image/StdDraw.png)


#### debug的一种方式
*通过assert来实现*

```java
assert index>=0 : "Negative index in method x";
```

#####JAVA可以自动调用任意对象的toString()来进行输出











