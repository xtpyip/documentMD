# Morris遍历

## 基本内容

- morris遍历

  > 1、当前cur无左子树，cur = cur.right
  >
  > 2、当前cur有左子树，找到cur左子树的最右节点mostRight
  >
  > ​	1>、若mostRight.right == null,令mostRight.right = cur,cur=cur.left
  >
  > ​	2>、若mostRight.right != null,令cur=cur.right,mostRight=null

## 问题集合

### MorrisTravel

- 链接：<a href="https://github.com/xtpyip/blog-alogrithm/blob/main/alogrithm/src/main/java/blog/wstx/class30/Code01_MorrisTraversal.java">测试链接</a>

- 内容：

  > 先中后充遍历二叉树
  
- 思路：

  > morris遍历序
  >
  > 先中后序：morris遍历
  >
  > 例：中序遍历为1 2 3 4 5 6 7的满二叉树**T**的morris序为
  >
  > ​	4 2 1 2 3 4 6 5 6 7 
  >
  >    只要第一次出现的位置保存下来为 4 2 1 3 6 5 7 这个为**T**的先序遍历
  >
  >    只要第二次出现的位置保存下来为 1 2 3 4 5 6 7 这个为**T**的中序遍历
  >
  >    只要来到第二次的位置对cur.left进行逆序打印(**链表反转**) 1 3 2 5 7 6 4 
  
- 代码：

  <details>
  <summary>morris遍历</summary>
  <p> - morris遍历序</p>
  <pre><code>public static void morris(Node head) {
  		if (head == null) {
  			return;
  		}
  		Node mostRight = null;
  		Node cur = head;
  		while (cur != null){
  			System.out.print(cur.value+" ");
  			mostRight = cur.left;
  			if(mostRight != null){
  				while (mostRight.right != null && mostRight.right != cur){
  					mostRight = mostRight.right;
  				}
  				if(mostRight.right == null){
  					// 第一次来
  					mostRight.right = cur;
  					cur = cur.left;
  					continue;
  				}else{
  					mostRight.right = null;
  				}
  			}
  			cur = cur.right;
  		}
  	}</code>  </pre>
  </details>
  
  <details>
  <summary>morris先序遍历</summary>
  <p> - 先序遍历</p>
  <pre><code>public static void morrisPre(Node head) {
  		System.out.println();
  		Node mostRight = null;
  		Node cur = head;
  		while (cur != null){
  			mostRight = cur.left;
  			if(mostRight != null){
  				while (mostRight.right != null && mostRight.right != cur){
  					mostRight = mostRight.right;
  				}
  				if(mostRight.right == null){
  					// 第一次来
  					System.out.print(cur.value +" ");
  					mostRight.right = cur;
  					cur = cur.left;
  					continue;
  				}else{
  					mostRight.right = null;
  				}
  			}else{
  				System.out.print(cur.value+" ");
  			}
  			cur = cur.right;
  		}
  		System.out.println();
  	}</code>  </pre>
  </details>
  
  <details>
  <summary>morris中序遍历</summary>
  <p> - 中序遍历</p>
  <pre><code>public static void morrisIn(Node head) {
  		if (head == null) {
  			return;
  		}
  		Node cur = head;
  		Node mostRight = null;
  		while (cur != null) {
  			mostRight = cur.left;
  			if (mostRight != null) {
  				while (mostRight.right != null && mostRight.right != cur) {
  					mostRight = mostRight.right;
  				}
  				if (mostRight.right == null) {
  					mostRight.right = cur;
  					cur = cur.left;
  					continue;
  				} else {
  					mostRight.right = null;
  				}
  			}
  			System.out.print(cur.value + " ");
  			cur = cur.right;
  		}
  		System.out.println();
  	}</code>  </pre>
  </details>
  
  <details>
  <summary>morris后序遍历</summary>
  <p> - 后序遍历</p>
  <pre><code>public static void morrisPos(Node head) {
  		if (head == null) {
  			return;
  		}
  		Node cur = head;
  		Node mostRight = null;
  		while (cur != null) {
  			mostRight = cur.left;
  			if (mostRight != null) {
  				while (mostRight.right != null && mostRight.right != cur) {
  					mostRight = mostRight.right;
  				}
  				if (mostRight.right == null) {
  					mostRight.right = cur;
  					cur = cur.left;
  					continue;
  				} else {
  					mostRight.right = null;
  					printEdge(cur.left);
  				}
  			}
  			cur = cur.right;
  		}
  		printEdge(head);
  		System.out.println();
  	}
  	public static void printEdge(Node head) {
  		Node tail = reverseEdge(head);
  		Node cur = tail;
  		while (cur != null) {
  			System.out.print(cur.value + " ");
  			cur = cur.right;
  		}
  		reverseEdge(tail);
  	}
  	public static Node reverseEdge(Node from) {
  		Node pre = null;
  		Node next = null;
  		while (from != null) {
  			next = from.right;
  			from.right = pre;
  			pre = from;
  			from = next;
  		}
  		return pre;
  	}</code>  </pre>
  </details>

### MinDepth

- 链接：<a href="https://leetcode.cn/problems/minimum-depth-of-binary-tree/description/">测试链接</a>

- 内容：

  > 给定一个二叉树，找出其最小深度。
  >
  > 最小深度是从根节点到最近叶子节点的最短路径上的节点数量。
  >
  > **说明：**叶子节点是指没有子节点的节点。
  >
  > **示例 1：**
  >
  > ![img](https://assets.leetcode.com/uploads/2020/10/12/ex_depth.jpg)
  >
  > ```
  > 输入：root = [3,9,20,null,null,15,7]
  > 输出：2
  > ```
  >
  > **示例 2：**
  >
  > ```
  > 输入：root = [2,null,3,null,4,null,5,null,6]
  > 输出：5
  > ```

- 思路：

  > 思路一：递归
  >
  > 思路二：mirris遍历

- 代码：

  <details>
  <summary>递归</summary>
  <p> - 最少节点数量</p>
  <pre><code>public static int minDepth1(TreeNode head) {
  		if (head == null) {
  			return 0;
  		}
  		return p(head);
  	}
  	// 返回x为头的树，最小深度是多少
  	public static int p(TreeNode x) {
  		if (x.left == null && x.right == null) {
  			return 1;
  		}
  		// 左右子树起码有一个不为空
  		int leftH = Integer.MAX_VALUE;
  		if (x.left != null) {
  			leftH = p(x.left);
  		}
  		int rightH = Integer.MAX_VALUE;
  		if (x.right != null) {
  			rightH = p(x.right);
  		}
  		return 1 + Math.min(leftH, rightH);
  	}</code>  </pre>
  </details>

  <details>
  <summary>morris遍历</summary>
  <p> - 最少节点数量</p>
  <pre><code>public static int minDepth2(TreeNode head) {
  		if (head == null) {
  			return 0;
  		}
  		TreeNode cur = head;
  		TreeNode mostRight = null;
  		int curLevel = 0;
  		int minHeight = Integer.MAX_VALUE;
  		while (cur != null) {
  			mostRight = cur.left;
  			if (mostRight != null) {
  				int rightBoardSize = 1;
  				while (mostRight.right != null && mostRight.right != cur) {
  					rightBoardSize++;
  					mostRight = mostRight.right;
  				}
  				if (mostRight.right == null) { // 第一次到达
  					curLevel++;
  					mostRight.right = cur;
  					cur = cur.left;
  					continue;
  				} else { // 第二次到达
  					if (mostRight.left == null) {
  						minHeight = Math.min(minHeight, curLevel);
  					}
  					curLevel -= rightBoardSize;
  					mostRight.right = null;
  				}
  			} else { // 只有一次到达
  				curLevel++;
  			}
  			cur = cur.right;
  		}
  		int finalRight = 1;
  		cur = head;
  		while (cur.right != null) {
  			finalRight++;
  			cur = cur.right;
  		}
  		if (cur.left == null && cur.right == null) {
  			minHeight = Math.min(minHeight, finalRight);
  		}
  		return minHeight;
  	}</code>  </pre>
  </details>
