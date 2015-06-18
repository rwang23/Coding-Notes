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

#### datatype casting

- Implicit casting :A data type of lower size (occupying less memory) is assigned to a data type of higher size

```java
int x = 10; // occupies 4 bytes
double y = x; // occupies 8 bytes
System.out.println(y); // prints 10.0
```

- Explicit casting: A data type of higher size (occupying more memory) cannot be assigned to a data type of lower size.

```java
double x = 10.5; // 8 bytes
int y = x; // 4 bytes ; raises compilation error
```

- Boolean casting: A boolean value cannot be assigned to any other data type. Except boolean, all the remaining 7 data types can be assigned to one another either implicitly or explicitly; but boolean cannot.

- byte –> short –> int –> long –> float –> double

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
###对比

![sort compare](/Users/Des/Documents/Coding/notes/image/sortcompare.png)


### 模板

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

###Priority Queues

- 二叉树
- 能够直接得到最小值最大值，第几大值，因为在建立树的时候已经排好序了，不需要再去遍历查找了

```java

public class MaxPQ<Key extends Comparable<Key>> {

	private Key[] pq;
	private int N = 0;

	public MaxPQ() {
		this(1);
	}

	public MaxPQ(int max) {
		pq = (Key[]) new Comparable[max + 1];

	}

	public MaxPQ(Key[] a) {
		pq = a;
	}


	public boolean isEmpty() {
		return N == 0;
	}

	public int size() {
		return N;
	}

	public boolean less(int i , int j) {
		return pq[i].compareTo(pq[j]) < 0;
	}

	public void exch(int i, int j) {
		Key temp = pq[i];
		pq[i] = pq[j];
		pq[j] = temp;
	}



	public void insert(Key v) {
		pq[++N] = v;
		swim(N);
	}

	public Key max() {
		return pq[1];
	}

	public Key delMax() {
		Key max = pq[1];
		exch(1, N--);
		pq[N + 1] = null;
		sink(1);
		return max;
	}

	public void swim(int k) {

		while (less(k, k / 2) && k > 1) {
			exch(k, k / 2);
			k = k / 2;
		}

	}

	public void sink(int k) {
		while (2 * k <= N) {
			int j = 2 * k;
			if (less(j, j + 1)) {
				j++;
			}
			if (less(k, j)) {
				exch(k, j);
				k = j;
			} else {
				break;
			}
		}

	}

}

```

### HeapSort

```java
public static void sort(Comparable[] a){
	int N = a.length;
	for(int k = N/2; k >= 1; k++) //构造heap,对除了最底层的元素进行sink，最后所有子树都满足父母比孩子大，但是最底层孩子之间不一定有序
		sink(a,k,N);
	while(N>1){ //交换首项与末项再沉淀交换，最终可以把最小的放在首项
		exch(a,1,N--);
		sink(a,1,N);
	}
}
```
- less than 2N*LgN + 2N 次比较
- 图示
![heapsort](/Users/Des/Documents/Coding/notes/image/heapsort.png )


##Searching

###symbol-table implementations compare

![symbol-table implementations compare](/Users/Des/Documents/Coding/notes/image/symbol-table\ implementations.png )



###Simple Table

- value and key pair, like dictionary

#### 判断相等

- if x and y are String values, then x.equals(y) is true if and only if x and y have the same length and are identical in each character position.
- For such client-defined keys, you need to override equals()
- we use equals() (for symbol tables where keys are not Comparable) or compareTo() (for or- dered symbol tables with Comparable keys)

####client
```java
public static void main(String[] args)
  {
     ST<String, Integer> st;
     st = new ST<String, Integer>();
     for (int i = 0; !StdIn.isEmpty(); i++)
     {
        String key = StdIn.readString();
        st.put(key, i);
     }
     for (String s : st.keys())
        StdOut.println(s + " " + st.get(s));
}

```


#### Linked-list Simple Table Implementation
![Linked-list Simple Table Implementation](/Users/Des/Documents/Coding/notes/image/Linked-list\ Simple\ Table\ Implementation.png)

```java
public class SequentialSearchST<Key, Value>
￼{
private Node first;
private class Node
{  // linked-list node
// first node in the linked list
Key key;
Value val;
Node next;
public Node(Key key, Value val, Node next)
{
   this.key  = key;
   this.val  = val;
   this.next = next;
} }
     public Value get(Key key)
     {  // Search for key, return associated value.
        for (Node x = first; x != null; x = x.next)
           if (key.equals(x.key))
              return x.val;    // search hit
        return null;           // search miss
}
     public void put(Key key, Value val)
     {  // Search for key. Update value if found; grow table if new.
        for (Node x = first; x != null; x = x.next)
           if (key.equals(x.key))
           {  x.val = val; return;  }      // Search hit: update val.
        first = new Node(key, val, first); // Search miss: add new node.
     }
}

```

### Binary Search in an ordered array
```java
  public class BinarySearchST<Key extends Comparable<Key>, Value>
  {
     private Key[] keys;
     private Value[] vals;
     private int N;
     public BinarySearchST(int capacity)
     {   // See Algorithm 1.1 for standard array-resizing code.
         keys = (Key[]) new Comparable[capacity];
         vals = (Value[]) new Object[capacity];
     }
     public int size()
     {  return N;  }
     public Value get(Key key)
     {
        if (isEmpty()) return null;
        int i = rank(key);
        if (i < N && keys[i].compareTo(key) == 0) return vals[i];
        else                                      return null;
     }
     public int rank(Key key, int lo, int hi)
  	{
	     if (hi < lo) return lo;
	     int mid = lo + (hi - lo) / 2;
	     int cmp = key.compareTo(keys[mid]);
	     if      (cmp < 0)
	          return rank(key, lo, mid-1);
	     else if (cmp > 0)
	          return rank(key, mid+1, hi);
	     else return mid;
     }
     // See page 381.
     public void put(Key key, Value val)
     {  // Search for key. Update value if found; grow table if new.
        int i = rank(key);
        if (i < N && keys[i].compareTo(key) == 0)
        {  vals[i] = val; return;  }
        for (int j = N; j > i; j--)
        {  keys[j] = keys[j-1]; vals[j] = vals[j-1];  }
        keys[i] = key; vals[i] = val;
        N++;
     }
     public void delete(Key key){
     // See Exercise 3.1.16 for this method.
	 }

	public Key min()
	{
		return keys[0];
	}
	public Key max()
	{
		return keys[N-1];
	}
	public Key select(int k)
	{
		return keys[k];
	}
	public Key ceiling(Key key)
	{
		int i = rank(key);
		return keys[i];
	}

}
```

###Binary Search Tree

- Graph Illustration
![BST](/Users/Des/Documents/Coding/notes/image/BST.png)

- Constructing and Inserting
![BST Constructing and Inserting](/Users/Des/Documents/Coding/notes/image/BST\ Constructing\ and\ Inserting.png )

**Code**

```java
public class BST<Key extends Comparable<Key>, Value> {

	private Node root;

	private class Node {

		private Key key;
		private Node left;
		private Node right;
		private Value val;
		private int N;

		public Node(Key key, Value val, int N) {
			this.key = key;
			this.val = val;
			this.N = N;
		}

		public int size() {
			return size(root);
		}

		public int size(Node x) {
			if (x == null) return 0;
			else return x.N;
		}

		public Value get(Key key) {
			return get(root, key);
		}

		public Value get(Node x, Key key) {
			if (x == null) return null;
			int cmp = key.compareTo(x.key);
			if (cmp < 0) return get(x.left, key);
			else if (cmp > 0) return get(x.right, key);
			else return x.val;
		}

		public void put(Key key, Value val) {
			root = put(root, key, val);
		}

		public Node put(Node x, Key key) {
			if (x == null) return new Node(key, val, 1);
			int cmp = key.compareTo(x.key);
			if (cmp < 0) x.left = put(x.left, key, val);
			else if (cmp > 0) x.right = put(x.right, key, val);
			else x.val = val;
			x.N = size(x.left) + size(x.right) + 1;
			return x;

		}

		public Key min() {
			return min(x).key;
		}

		private Node min(Node x) {
			if (x != null) return min(x.left);
			else return x;
		}

		public Key floor(Key key) {
			return floor(x).key;
		}

		private Node floor(Node x) {
			if (x == null) return null;
			int cmp = key.compareTo(x.key);
			if (cmp == 0) return x;
			if (cmp < 0) return floor(x.left, key);
			Node t = floor(x.right, key);
			if (t != null) return t;
			else return x;
		}

		public Key select(int k) {
			return select(root, k).key;
		}
		private Node select(Node x, int k) {
			// Return Node containing key of rank k.
			if (x == null) return null;
			int t = size(x.left);
			if      (t > k) return select(x.left,  k);
			else if (t < k) return select(x.right, k - t - 1);
			else            return x;
		}
		public int rank(Key key) {
			return rank(key, root);
		}
		private int rank(Key key, Node x) {
			// Return number of keys less than x.key in the subtree rooted at x.
			if (x == null) return 0;
			int cmp = key.compareTo(x.key);
			if      (cmp < 0) return rank(key, x.left);
			else if (cmp > 0) return 1 + size(x.left) + rank(key, x.right);
			else              return size(x.left);
		}


		public void deleteMin() {
			root = deleteMin(root);
		}
		private Node deleteMin(Node x) {
			if (x.left == null) return x.right;
			x.left = deleteMin(x.left);
			x.N = size(x.left) + size(x.right) + 1;
			return x;
		}


		public void delete(Key key) {
			root = delete(root, key);
		}
		private Node delete(Node x, Key key) {
			if (x == null) return null;
			int cmp = key.compareTo(x.key);
			if      (cmp < 0) x.left  = delete(x.left,  key);
			else if (cmp > 0) x.right = delete(x.right, key);
			else {
				if (x.right == null) return x.left;
				if (x.left == null) return x.right;
				Node t = x;
				x = min(t.right);  // See page 407.
				x.right = deleteMin(t.right);
				x.left = t.left;
			}
			x.N = size(x.left) + size(x.right) + 1;
			return x;
		}



	}
}

```

- Worst case: 所有结点都在一边的树上，比如全在右结点
- Best case: 很平均
- Search hits in a BST built from N random keys require ~ 2 ln N (about 1.39 lg N) compares, on the average.
- Insertions and search misses in a BST built from N random keys require ~ 2 ln N (about 1.39 lg N) compares, on the average.
- min在最左结点 max在最右结点
- floor(key)等于Key或者小于Key但是大于其他剩余key

```java
		public Key floor(Key key) {
			return floor(x).key;
		}

		private Node floor(Node x) {
			if (x == null) return null;
			int cmp = key.compareTo(x.key);
			if (cmp == 0) return x;
			if (cmp < 0) return floor(x.left, key);
			Node t = floor(x.right, key);
			if (t != null) return t;
			else return x;
		}
```
- ceiling(key)等于key或者大于key小于其他剩余key
![BST floor](/Users/Des/Documents/Coding/notes/image/BST\ floor.png)

- delete min
![delete min](/Users/Des/Documents/Coding/notes/image/delete\ min.png)

```java
		public void deleteMin() {
			root = deleteMin(root);
		}
		private Node deleteMin(Node x) {
			if (x.left == null) return x.right;
			x.left = deleteMin(x.left);
			x.N = size(x.left) + size(x.right) + 1;
			return x;
		}
```
- delete
![BST delete](/Users/Des/Documents/Coding/notes/image/BST\ delete.png)

```java
		public void delete(Key key) {
			root = delete(root, key);
		}
		private Node delete(Node x, Key key) {
			if (x == null) return null;
			int cmp = key.compareTo(x.key);
			if      (cmp < 0) x.left  = delete(x.left,  key);
			else if (cmp > 0) x.right = delete(x.right, key);
			else {
				if (x.right == null) return x.left;
				if (x.left == null) return x.right;
				Node t = x;
				x = min(t.right);  // See page 407.
				x.right = deleteMin(t.right);
				x.left = t.left;
			}
			x.N = size(x.left) + size(x.right) + 1;
			return x;
		}
```


