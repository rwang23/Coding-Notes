##API

- Princeton Algorithm offer some APIs

```java
public class StdRandom{
	static void initialize(long seed){}
	static double random(){}
	static int uniform(int N){}
	static int uniform(int lo, int hi){}
	static double uniform(double lo, double hi){}
	static boolean bernoulli(double p){}
	static double gaussian(){}
	static double gaussian(double m, double s){}
	static int discrete(double[] a){}
	static void shuffle(double[] a){}
}

public class StdStats{
	static double max(double[] a){}
	static double min(double[] a){}
	static double mean(double[] a){}
	static double var(double[] a){} // sample variance
	static double stddev(double[] a){} //sample standard deviation
	static double median(double[] a){}
}
```

```java
public class Integer{

	static int parseInt(String s){}
	static String toString(int i){}
}

public class Double{
}
```

```java
public class StdOut{
	static void print(String s){}
	static void println(String s){}
	static void println(){}
	static void printf(String f){}
}
```

```java
public class StdIn{
	static boolean isEmppty(){}
	static int readInt(){}
	static double readDouble(){}
	static float readFloat(){}
	static long readLong(){}
	static boolean readBoolean(){}
	static char readChar(){}
	static byte readByte(){}
	static String readString(){}
	static boolean hasNextLine(){}
	static String readLine(){}
	static String readAll(){}

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
#### 使用StdIn的例子

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


When you declare a variable to be final, you are promising to assign it a value only once, either in an initializer or in the constructor.

#### toString()自动执行的函数

- If an object’s data type does not include an implementation of toString(), then the default implementation in Object is invoked, which is normally not helpful，since it typically returns a string representation of the memory address of the object
- we generally include implementations of toString() that override the default in every class that we develop

#### Wrapper Type

-  Boolean, Byte, Character, Double, Float, Integer, Long, and Short correspond to boolean, byte, char, double, float, int, long, and short

#### Equality

- == means the reference equals
- equals() means the value equals




### 递归
递归代码有以下三个特点，违反了就可能得到错误或低效的代码:

* 递归总有一个最简单的情况
* 递归总是尝试去解决一个规模更小的子问题
* 递归调用的父问题域尝试解决的子问题之间不应该有交集

###扩展库
![Java random API](/Users/Des/Documents/Coding/notes/image/java\ random\ api.png)

###类型转换
#####Java内置了一些类以及其静态转换函数



#### debug的一种方式
*通过assert来实现*

```java
assert index>=0 : "Negative index in method x";
```

#####JAVA可以自动调用任意对象的toString()来进行输出











