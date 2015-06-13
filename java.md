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
- x.equals(null) returns false


### 递归
递归代码有以下三个特点，违反了就可能得到错误或低效的代码:

* 递归总有一个最简单的情况
* 递归总是尝试去解决一个规模更小的子问题
* 递归调用的父问题域尝试解决的子问题之间不应该有交集

#### debug的一种方式
*通过assert来实现*

```java
assert index>=0 : "Negative index in method x";
```

###Generics

- 声明 public class FixedCapacityStack<Item>，之后相关类型都是Item
- 但是generics里因为语法原因不能构造数组，如 a = new Item[cap]
- 解决办法是 a = (Item[]) new Object[cap]

###Iterator

- import java.util.Iterator

###Comparable
!(http://www.digizol.com/2008/07/java-sorting-comparator-vs-comparable.html)

- 使用Comparable去定义输入参数的时候，表明这个方法，能支持Comparable的primitive variable都支持
- Example: Comparable里边的compareTo帮助class在进行collection.sort(List)自动排序
- 测试的时候，使用Collections.sort(coll)

```java
public class Employee implements Comparable<Employee>{
	private int empid;
	private String name;
	private int age;
	public int compareTo(Employee o){
		return this.empid - o.empid;
	}
}
```
- 如果想对其他项进行排序，就是用Comparator
- 测试的时候，使用Colletions.sort(coll, new EmpSortByName())

```java
public class EmpSortByName implements Comparator<Employee>{
	public int compare(Employee o1, Employee o2){
		return o1.getName().compareTo(o2.getName());
	}
}
```

## Stack

###数组实现的Stack
####固定长度的Stack+resize
```java
public class FixedCapacityStack<Item> {

	private Item[] stack;
	private int N = 0;

	public FixedCapacityStack(int capacity) {
		stack = (Item[]) new Object[capacity];
	}

	public int size() {
		return N;
	}

	/**
	 * [resize the stack]
	 * @param max [the new length]
	 */
	private void resize(int max) {
		Item[] temp = (Item[]) new Object[max];
		for (int i = 0; i < N; i++) {
			temp[i] = stack[i];
		}
		stack = temp;
	}

	public boolean isEmpty() {
		return N == 0;
	}

	/**
	 * [push, and can resize according to the length]
	 * @param item [description]
	 */
	public void push(Item item) {
		if (N == stack.length) {
			resize(2 * stack.length);
		}
		stack[N++] = item;
	}

	public Item pop() {
		return stack[--N];
	}

}
```

###Linked list实现stack

- The difference is that it is easier to insert items into the sequence and to remove items from the sequence with linked lists.

```java
private class Node{
	Item item;
	Node next;
}
```
- 头部添加新node

```java
Node oldFirst = first;
first = new Node();
first.item = "xx";
first.next = oldFirst;
```

- 头部删除node

```java
first.next = first;
```

- 尾部添加Node

```java
Node oldLast = last;
last = new Node();
last.item = "xx";
oudLast.next = last;
```
- 遍历node

```java
for(Node x =first; x!=null; x=x.next){
}
```

##算法分析
###时间测量
```java
public class Stopwatch {
	private final long start;
	public Stopwatch() {
		start = System.currentTimeMillis();
	}
	public double elapsedTime() {
		long now = System.currentTimeMillis();
		return (now - start) / 1000.0;
	}
}

```

##排序

- 模板

```java
public class Example {
	public static void sort(Comparable[] a) {

	}

	public static boolean less(Comparable v, Comparable w) {
		return v.compareTo(w) < 0;
	}

	private static void exch(Comparable[] a, int i, int j) {
		Comparable t = a[i];
		a[i] = a[j];
		a[j] = t;
	}

	private static void show(Comparable[] a) {
		for (int i = 0; i < a.length; i++) {
			StdOut.print(a[i] + " ");
		}
		StdOut.println();
	}

	public static boolean isSorted(Comparable[] a) {
		for (int i = 1; i < a.length; i++) {
			if (less(a[i], a[i - 1])) {
				return false;
			}
			return true;
		}
	}

	public static void main(String[] args) {
		String[] a = In.readStrings();
		sort(a);
		assert isSorted(a);
		show(a);
	}


}

```
###选择排序

- Running time is insensitive to input. 如果已经排好序，再进行选择排序，将花费一样的时间
- Data movement is minimal. 数据只交换了N次

```java
	public static void selectSort(Comparable[] a) {
		int N = a.length;
		for (int i = 0; i < N; i++) {
			int min = i;
			for (int j = i+1; j < N; j++) {
				if (less(a[j], a[min]))
					min = j;
			}
			exch(a, i, min);
		}
	}
```

###插入排序

- 基本比选择排序快一倍

```java
	public static void insertSort(Comparable[] a) {
		int N = a.length;
		for (int i = 1; i < N; i++) {
			for (int j = i ; j > 0 && less(a[j], a[j - 1]); j--) {
				exch(a, j, j - 1);
			}
		}
	}
```

###希尔排序

```java
	public static void shellSort(Comparable[] a) {
		int h = 1;
		int N = a.length;
		while (h < n / 3) {
			h = h * 3 + 1;
		}
		while (h >= 1) {
			for (i = h; i < N; i = i++) {
				for (j = i; j >= h && less(a[j], a[j - h]); j = j - h) {
					exch(a, j, j - h);
				}
				h = h / 3;
			}
		}
	}
```

###归并排序

- 复杂度为NlgN

```java
	private static Comparable[] aux;
	public static void merge(Comparable[] a, int lo, int mid, int hi) {
		int i = lo;
		int j = mid + 1;
		for (int k = lo; k <= hi; k++) {
			aux[k] = a[k];
		}
		for (int k = lo; k <= hi; k++) {
			if (i > mid) a[k] = aux[j++];
			else if (j > hi) a[k] = aux[i++];
			else if (less(aux[i], aux[j])) a[k] = aux[i++];
			else a[k] = aux[j++];
		}
	}
	public static void toMergeSort(Comparable[] a) {
		aux = new Comparable[a.length];
		mergeSortUB(a, 0, a.length);
	}
	public static void mergeSortUB(Comparable[] a, int lo, int hi) {
		if (hi <= lo) return;
		int mid = (lo + hi) / 2;
		mergeSortUB(a, lo, mid);
		mergeSortUB(a, mid + 1, hi);
		merge(a, lo, mid, hi);
	}
	public static void mergeSortBU(Comparable[] a) {
		int N = a.length;
		aux = new Comparable[N];
		for (int sz = 1; sz < N; sz = sz + sz) {
			for (int lo = 0; lo < N - sz; lo += sz + sz)
				merge(a, lo, lo + sz + 1, Math.min(lo + sz + sz - 1, N - 1));
		}
	}
```

###快速排序

- 原地切分

```java
	public static void toQuicksort(Comparable[a]) {
		StdRandom.shuffle(a);
		quickSort(a, 0, a.length - 1);
	}
	private static void quickSort(Comparable[a], int lo, int hi) {
		if (hi <= lo) return;
		int j = partition(a, lo, hi);
		quickSort(a, lo, j - 1);
		quickSort(a, j + 1, hi);
	}
	private static int partition(Comparable[a], int lo, int hi) {
		int i =lo;
		int j=hi+1;
		Comparable v = a[lo];
		while(true){
			while(less(a[++i],v)) if(i==hi) break;
			while(less(v,a[--j])) if(j==lo) break;
			if(i>=j) break;
			exch(a,i,j);
		}
		exch(a,lo,j);
		return j;
	}
```


