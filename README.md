# **蓝桥杯样板代码**

https://blog.csdn.net/weixin_41793113/article/details/88762953

代码样板2

https://blog.csdn.net/GD_ONE/article/details/104061907?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param

## 全排列模板1，最常用的写法

```java
public class 全排列_模板1 {

	public static void main(String[] args) {
		dfs(0);
		System.out.println(ans);//9的全排有362880种
	}
	static int[] a = new int[] {1,2,3,4,5,6,7,8,9};
	static int n=9,ans=0;
    
	static void dfs(int m) {
		if(m>=n) {
			System.out.println("一些核心的操作 比如ans:"+ans);
			ans++;
			for(int i=0;i<n;i++)
				System.out.print(a[i]+" ");
			System.out.println();
			return;
		}
		for(int i=m;i<n;i++) {
			swap(i,m);
			dfs(m+1);
			swap(i,m);//回溯
		}
	}
	
	static void swap(int i,int j) {
		int t = a[i];
		a[i] = a[j];
		a[j] = t;
	}
}
```

## 全排列模板2，使用标记数组的写法

```java
public class 全排列_模板2 {
 
	public static void main(String[] args) {
		vis = new boolean[n];
		b = new int[n];
		dfs(0);
		System.out.println(ans);//9的全排有362880种
	}
	
	static int[] a = new int[] {1,2,3,4,5,6,7,8,9};
	static int[] b;
	static boolean[] vis;
	static int n=9,ans=0;
	
	static void dfs(int m) {
		if(m>=n) {
			System.out.println("一些核心的操作 比如ans:"+ans);
			ans++;
			for(int i=0;i<n;i++)
				System.out.print(b[i]+" ");
			System.out.println();
			return;
		}
		
		for(int i=0;i<n;i++) 
			if(!vis[i]) {
				vis[i] = true;
				b[m] = a[i];
				dfs(m+1);
				b[m] = 0;//其实这个也可以不用回溯，它会被覆盖
				vis[i] = false;//回溯
			}
	}
}
```

##  下面是需要排重的全排_模板

在上面模板上使用了哈希表查重，把一些数组并接成字符串

```java
import java.util.HashSet;
 
public class 全排列_模板3 {
 
	public static void main(String[] args) {
		dfs(0);
		System.out.println(ans);//9的全排有362880种
		System.out.println(set.size());//1680
	}
	
	static int[] a = new int[] {1,1,1,2,2,2,3,3,3};
	static int n=9,ans=0;
	static HashSet<String> set = new HashSet<>();
	
	static void dfs(int m) {
		if(m>=n) {
			System.out.println("一些核心的操作 比如ans:"+ans);
			ans++;
			String s="";
			for(int i=0;i<n;i++) {
				s+=a[i];
				System.out.print(a[i]+" ");
			}
			System.out.println();
			set.add(s);
			return;
		}
		for(int i=m;i<n;i++) {
			swap(i,m);
			dfs(m+1);
			swap(i,m);//回溯
		}
	}
	
	static void swap(int i,int j) {
		int t = a[i];
		a[i] = a[j];
		a[j] = t;
	} 
}
```

## 判断闰年

```java
	static boolean is(int x) {
		return x%400==0 || (x%4==0 && x%100!=0);
	}
```

## 筛素数O(![{\color{DarkBlue} n^{\tfrac{3}{2}}}](https://private.codecogs.com/gif.latex?%7B%5Ccolor%7BDarkBlue%7D%20n%5E%7B%5Ctfrac%7B3%7D%7B2%7D%7D%7D))

```java
	static boolean is(int n) {
		if(n==1)
			return false;
		for(int i=2;i*i<=Math.sqrt(n);i++)
			if(n%i==0)
				return false;
		return true;
	}
```

## 倍筛法_素数O(nlogn)

```java
public class 倍筛模板 {
 
	public static void main(String[] args) {
		boolean[] is = new boolean[1000005];
		is[1] = true;//true表示不是素数
		for(int i=2;i<1000005;i++)
			if(!is[2])
				for(int j=2*i;j<1000005;j+=i)
					is[j] = true;
		System.out.println(is[2004]);
	}
}
```

## 最小公倍数gcd

```java
	static int gcd(int a,int b) {
		return b==0?a:gcd(b,a%b);
	}
```

## 最大公约数lcm

```java
	static int lcm(int a,int b) {
		return a*b/gcd(a,b);
	}
```

## 二分答案_模板

[蓝桥杯 2017年第八届真题 分巧克力 经典的二分答案 输入挂](https://blog.csdn.net/weixin_41793113/article/details/88727882)

```java
	static void f(int[] a) {
		int n = a.length;
		int l=0,r=n-1,ans=0;//一般上界需要自己构造
		while(l<=r) {
			int mid = l + (r-l)/2;
			if(ok(a[mid])) {
				r = mid-1;
				ans = mid;
			}else
				l = mid+1;
		}
		System.out.println(ans);
	}
	
	static boolean ok(int x) {
		return false;//按照题意写
	}
```

## 输入挂模板

```java
	//解决javaIO读取过慢的方法，利用该类读取输入数据，不要用Scanner！！！
	static class InputReader {
		public BufferedReader reader;
		public StringTokenizer tokenizer;
 
		public InputReader(InputStream stream) {
			reader = new BufferedReader(new InputStreamReader(stream), 32768);
			tokenizer = null;
		}
 
		public String next() {
			while (tokenizer == null || !tokenizer.hasMoreTokens()) {
				try {
					tokenizer = new StringTokenizer(reader.readLine());
				} catch (IOException e) {
					throw new RuntimeException(e);
				}
			}
			return tokenizer.nextToken();
		}
 
		public int nextInt() {
			return Integer.parseInt(next());
		}
	}
```

## BufferedReader和BufferedWriter

```java
public class Main{
    static BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
    static BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
    public static void main(String[] args) throws IOException{
        //测试writr 不能直接输出int类型
    	int a = 65;
        out.write(a);
        out.write("\n");
    	out.write(a + "\n");  // 使用 + 号拼接个字符串 使参数整体为一个字符串 
        out.write(Integer.toString(a)); // 输出a的字符串形式
        out.write("\n");
       
        //测试 read() 和  readLine();
        int b = in.read();   // read()只读取一个字符
        int c = in.read();   // 吸收 \n
        int x = in.read();   // 吸收 \r
       // String e = in.readLine();
        String d = in.readLine();
        out.write("\n");
        out.write(b + "\n");
        out.write(c + "\n");
        out.write(x + "\n");
        out.write(d + "\n");
        //out.write(e);
        out.flush();
    }
}
```

