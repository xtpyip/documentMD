# indexTree，AC自动机

## 基本内容

- indexTree 算法

  > indexTree是针对**单点(区间)更新与区间查询**的算法结构
  >
  > 从前文我们了解了前缀树，它是针对于区间查询的结构，但它对于单点更新不是很友好。
  >
  > indexTree是在前缀树的基础上进行的功能增强，它是从下标1开始计算的
  >
  > 一个数组arr的前缀树为**qT**,indexTree为**iT**
  >
  > qT[i] = arr[0]+arr[1]+...+arr[i]
  >
  > iT[i] = arr[j] j是满足下边的情况
  >
  > | 下标i | iT[i] | arr原始下标(arr[1]+arr[2]简写为1+2，从下标1开始) |
  > | ----- | ----- | ------------------------------------------------ |
  > | 1     |       | 1                                                |
  > | 2     |       | 1+2                                              |
  > | 3     |       | 3                                                |
  > | 4     |       | 1+2+3+4                                          |
  > | 5     |       | 5                                                |
  > | 6     |       | 5+6                                              |
  > | 7     |       | 7                                                |
  > | 8     |       | 1+2+3+4+5+6+7+8                                  |
  > | 9     |       | 9                                                |
  > | 10    |       | 9+10                                             |
  >
  > 6 = 0110 ->最后一个1变为0再+1 -> **0101 ~ 0110** = 5+6
  >
  > 8 = 1000 ->最后一个1变为0再+1 -> **0001 ~ 1000** = 1+2+3+4+5+6+7+8
  >
  > 查询前10的累加和
  >
  > 10 = 1010 ->最后一个1变为0再+1 -> **1001~1010** = 9 + 10 = **iT[10]**										
  >
  > ​														   -> **0001 ~ 1000** = 1+2+3+4+5+6+7+8 = **it[8]**
  >
  > ​	= 1+2+3+4+5+6+7+8+9+10

- AC自动机

  > AC 自动机是 **以 Trie 的结构为基础**，结合 **KMP 的思想** 建立的自动机，用于解决多模式匹配等任务。
  >
  > AC 自动机本质上是 Trie 上的自动机。
  >
  > 简单来说，建立一个 AC 自动机有两个步骤：
  >
  > 1. 基础的 Trie 结构：将所有的模式串构成一棵 Trie。
  > 2. KMP 的思想：对 Trie 树上所有的结点构造失配指针。
  >
  > 建立完毕后，就可以利用它进行多模式匹配。

## 问题集合

### IndexTree1D

- 链接：<a href="https://github.com/xtpyip/blog-alogrithm/blob/main/alogrithm/src/main/java/blog/wstx/class32/Code01_IndexTree.java">测试链接</a>

- 内容：

  > 求单点添加（更新）与范围和
  >
  
- 思路：

  > 创建一个indexTree,下标0弃而不用
  >
  > arr[0...n-1]->arr[1...n]
  >
  > indexSum[1..n],下标i所对应的值是arr中的某些值
  >
  > 如i为7-> 111 -> 111~111 7
  >
  > ​         16-> 1 0000 -> 0 0001 ~ 1 0000 
  >
  > 添加操作：
  >
  > ​	影响到当前i，与i只取二进制最后一位+i ... <=n
  >
  > 求各操作：
  >
  > ​	原下标  indexSum下标    代表范围
  >
  > ​	31	      indexSum[31]   1 1111~1 1111
  >
  > ​	29,30	indexSum[30]	1 1110 ~ 1 1101          
  >
  > ​    25,26,27,28   indexSum[28] 1 1100~1 1001
  >
  > ​	17~24     indexSum[24]   1 1000 ~ 1 0001
  >
  > ​	16~1        index[16]       1 0000 ~ 0 0001
  
- 代码：

  <details>
  <summary>一维indexTree</summary>
  <p> - indexTree实现</p>
  <pre><code>// 下标从1开始！
  	public static class IndexTree {
  		private int[] tree;
  		private int N;
  		// 0位置弃而不用！
  		public IndexTree(int size) {
  			N = size + 1;
  			tree = new int[N];
  		}
  		// 1~index 累加和是多少？
  		public int sum(int index) {
  			int ans = tree[index];
  			while (index - (index & (-index)) != 0){
  				index -= index & (-index);
  				ans += tree[index];
  			}
  			return ans;
  		}
  		// index & -index : 提取出index最右侧的1出来
  		// index :           0011001000
  		// index & -index :  0000001000
  		public void add(int index, int d) {
  			while (index <= N){
  				tree[index] += d;
  				index += index & (-index);
  			}
  		}
  	}</code>  </pre>
  </details>

### IndexTree2D

- 链接：<a href="https://leetcode.cn/problems/range-sum-query-2d-mutable">测试链接</a>

- 内容：

  > 求二维单点添加（更新）与范围和

- 思路：

  > 与1维一致，不过是加了一个维度，加了一个笛卡尔积
  >
  > (i,j) 下标的更新(添加) 影响到了
  >
  > (i及其i+i二进制末尾1代表的值.....<=N) * (j及其j+j二进制末尾1代表的值.....<=M)
  >
  > (0,0)位置到(i,j)位置的区间和等于
  >
  > (i及其i-i二进制末尾1代表的值.....>=0) * (j及其j-j二进制末尾1代表的值.....>=0)的下标的所有值

- 代码：

  <details>
  <summary>二维indexTree</summary>
  <p> - indexTree实现</p>
  <pre><code>public class Code02_IndexTree2D {
  	private int[][] tree;
  	private int[][] nums;
  	private int N;
  	private int M;
  	public Code02_IndexTree2D(int[][] matrix) {
  		if (matrix.length == 0 || matrix[0].length == 0) {
  			return;
  		}
  		N = matrix.length;
  		M = matrix[0].length;
  		tree = new int[N + 1][M + 1];
  		nums = new int[N][M];
  		for (int i = 0; i < N; i++) {
  			for (int j = 0; j < M; j++) {
  				update(i, j, matrix[i][j]);
  			}
  		}
  	}
  	private int sum(int row, int col) {
  		int sum = 0;
  		for (int i = row + 1; i > 0; i -= i & (-i)) {
  			for (int j = col + 1; j > 0; j -= j & (-j)) {
  				sum += tree[i][j];
  			}
  		}
  		return sum;
  	}
  	public void update(int row, int col, int val) {
  		if (N == 0 || M == 0) {
  			return;
  		}
  		int add = val - nums[row][col];
  		nums[row][col] = val;
  		for (int i = row + 1; i <= N; i += i & (-i)) {
  			for (int j = col + 1; j <= M; j += j & (-j)) {
  				tree[i][j] += add;
  			}
  		}
  	}
  	public int sumRegion(int row1, int col1, int row2, int col2) {
  		if (N == 0 || M == 0) {
  			return 0;
  		}
  		return sum(row2, col2) + sum(row1 - 1, col1 - 1) - sum(row1 - 1, col2) - sum(row2, col1 - 1);
  	}
  }</code>  </pre>
  </details>

### AC

- 链接：<a href="https://github.com/xtpyip/blog-alogrithm/blob/main/alogrithm/src/main/java/blog/wstx/class32/Code03_AC1.java">测试链接</a>

- 内容：

  > AC自动机

- 思路：

  > 先创建一个前缀树
  >
  > 使用**fail指针指向为其路径上的字符串的最后一个字符结尾的最长的字符串的位置**
  >
  > 默认头指空，第一级子节点fail指向头
  >
  > 如：abc d bc c，如下所示
  >
  > 使用队列层序遍历
  >
  > 第一次完整入队 a d b c 
  >
  > b->b , c->c  
  >
  > 第二次完整入队 b c
  >
  > c->c   
  >
  > 第三次完整入队 c
  >
  > 无

  ![](http://8.130.177.90:9000/blog/24/alogrithm/wstx/class32/a2020_32_ac.png)

- 代码：

  <details>
  <summary>AC自动机实现</summary>
  <p> - 自动机实现</p>
  <pre><code>public static class Node {
  		public int end; // 有多少个字符串以该节点结尾
  		public Node fail;
  		public Node[] nexts;
  		public Node() {
  			end = 0;
  			fail = null;
  			nexts = new Node[26];
  		}
  	}
  	public static class ACAutomation {
  		private Node root;
  		public ACAutomation() {
  			root = new Node();
  		}
  		// 你有多少个匹配串，就调用多少次insert
  		public void insert(String s) {
  			char[] str = s.toCharArray();
  			Node cur = root;
  			int index = 0;
  			for (int i = 0; i < str.length; i++) {
  				index = str[i] - 'a';
  				if (cur.nexts[index] == null) {
  					cur.nexts[index] = new Node();
  				}
  				cur = cur.nexts[index];
  			}
  			cur.end++;
  		}
  		public void build() {
  			// 宽度优先遍历
  			Queue<Node> queue = new LinkedList<>();
  			queue.add(root);
  			Node cur = null;
  			Node cfail = null;
  			while (!queue.isEmpty()){
  				 cur = queue.poll(); // 每弹出一个，要把它的所有的子节点的fail指针挂好
  				for (int i = 0; i < 26; i++) {
  					if(cur.nexts[i] != null){ // 找当前孩子的fail指向
  						cur.nexts[i].fail = root; // 如果找的到更新，找不到就是root
  						cfail = cur.fail; // 从父去找其fail指针
  						while (cfail != null){
  							if(cfail.nexts[i] != null){ // 存在cfail的指针
  								cur.nexts[i].fail = cfail.nexts[i];
  								break;
  							}
  							cfail = cfail.fail;
  						}
  						queue.add(cur.nexts[i]);
  					}
  				}
  			}
  		}
  		public int containNum(String content) {
  			char[] chars = content.toCharArray();
  			Node cur = root;
  			int ans = 0;
  			int index = 0;
  			Node follow = null;
  			for (int i = 0; i < chars.length; i++) {
  				index = chars[i] - 'a';
  				while (cur.nexts[index] == null && cur != root) {
  					cur = cur.fail; // 没有当前的通路
  				}
  				cur = cur.nexts[index] != null ? cur.nexts[index] : root;
  				follow = cur; // 要么走到了root,要么还有内容
  				while (follow != null){
  					if(follow.end == -1){
  						break;
  					}
  					{  // 具体业务
  						ans += follow.end;
  						follow.end = -1;
  					}
  					follow = follow.fail;
  				}
  			}
  			return ans;
  		}
  	}</code>  </pre>
  </details>

### AC2

- 链接：<a href="https://github.com/xtpyip/blog-alogrithm/blob/main/alogrithm/src/main/java/blog/wstx/class32/Code04_AC2.java">测试链接</a>

- 内容：

  > 记录在一个文章中出现了哪些违规词，假设已知道所有的违规词

- 思路：

  > 使用ac自动机，添加所有的节点，并将所有的违规节点都标记一下
  >
  > 对文章遍历，如果进入，则按层遍历所有节点的fail，直到空，中途有违规节点添加
  >
  > 直接文章遍历结束

  ![](http://8.130.177.90:9000/blog/24/alogrithm/wstx/class32/a2020_32_ac.png)

- 代码：

  <details>
  <summary>AC自动机实现</summary>
  <p> - 所有出现的违规词</p>
  <pre><code>public static class Node {
  		public String end; // 有多少个字符串以该节点结尾
  		public Node fail;
  		public boolean endUse;
  		public Node[] nexts;
  		public Node() {
  			end = null;
  			endUse = false;
  			fail = null;
  			nexts = new Node[26];
  		}
  	}
  	public static class ACAutomation {
  		private Node root;
  		public ACAutomation() {
  			root = new Node();
  		}
  		// 你有多少个匹配串，就调用多少次insert
  		public void insert(String s) {
  			char[] str = s.toCharArray();
  			Node cur = root;
  			int index = 0;
  			for (int i = 0; i < str.length; i++) {
  				index = str[i] - 'a';
  				if (cur.nexts[index] == null) {
  					cur.nexts[index] = new Node();
  				}
  				cur = cur.nexts[index];
  			}
  			cur.end = s;
  		}
  		public void build() {
  			// 宽度优先遍历
  			Queue<Node> queue = new LinkedList<>();
  			queue.add(root);
  			Node cur = null;
  			Node cfail = null;
  			while (!queue.isEmpty()){
  				 cur = queue.poll(); // 每弹出一个，要把它的所有的子节点的fail指针挂好
  				for (int i = 0; i < 26; i++) {
  					if(cur.nexts[i] != null){ // 找当前孩子的fail指向
  						cur.nexts[i].fail = root; // 如果找的到更新，找不到就是root
  						cfail = cur.fail; // 从父去找其fail指针
  						while (cfail != null){
  							if(cfail.nexts[i] != null){ // 存在cfail的指针
  								cur.nexts[i].fail = cfail.nexts[i];
  								break;
  							}
  							cfail = cfail.fail;
  						}
  						queue.add(cur.nexts[i]);
  					}
  				}
  			}
  		}
  		public List<String> containWords(String content) {
  			char[] chars = content.toCharArray();
  			Node cur = root;
  			int index = 0;
  			Node follow = null;
  			ArrayList<String> ans = new ArrayList<>();
  			for (int i = 0; i < chars.length; i++) {
  				index = chars[i] - 'a';
  				while (cur.nexts[index] == null && cur != root) {
  					cur = cur.fail; // 没有当前的通路
  				}
  				cur = cur.nexts[index] != null ? cur.nexts[index] : root;
  				follow = cur; // 要么走到了root,要么还有内容
  				while (follow != null){
  					if(follow.endUse){
  						break;
  					}
  					if(follow.end != null){  // 具体业务
  						ans.add(follow.end);
  						follow.endUse = true;
  					}
  					follow = follow.fail;
  				}
  			}
  			return ans;
  		}
  	}</code>  </pre>
  </details>