```java

### Basic Idea
Euclid to calculate the gcd

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

###`递归`
递归代码有以下三个特点，违反了就可能得到错误或低效的代码:

* 递归总有一个最简单的情况
* 递归总是尝试去解决一个规模更小的子问题
* 递归调用的父问题域尝试解决的子问题之间不应该有交集
