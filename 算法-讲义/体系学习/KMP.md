# KMP

## 基本内容

- KMP 算法

  > 它是一种改进的字符串匹配算法，由 D.E.Knuth，J.H.Morris 和 V.R.Pratt 提出的，因此人们称它为克努特 — 莫里斯 — 普拉特操作（简称 KMP 算法）。
  >
  > KMP 算法的核心是利用匹配失败后的信息，尽量减少模式串与主串的匹配次数以达到快速匹配的目的。具体实现就是通过一个 next () 函数实现，函数本身包含了模式串的局部匹配信息。
  >
  > KMP 算法的时间复杂度O(m+n)。
## 问题集合

### KMP

- 链接：<a href="https://github.com/xtpyip/blog-alogrithm/blob/main/alogrithm/src/main/java/blog/wstx/class27/Code01_KMP.java">测试链接</a>

- 内容：

  > 在字符串s1中找到字符串s2第一次出现的在s1的下标返回，没有则返回-1
  >
  
- 思路：

  > 思路一：暴力尝试-略
  >
  > 思路二：KMP算法的实现，next生成不回退，next数组加速不回退
  >
  
- 代码：

  <details>
  <summary>KMP</summary>
  <p> - 匹配字符串</p>
  <pre><code>public static int getIndexOf(String s1, String s2) {
  		if (s1 == null || s2 == null || s2.isEmpty() || s1.length() < s2.length()) {
  			return -1;
  		}
  		char[] char1 = s1.toCharArray();
  		char[] char2 = s2.toCharArray();
  		int x = 0,y = 0;
  		int[] next = getNextArray(char2);
  		while (x < char1.length && y < char2.length){
  			if(char1[x] == char2[y]){
  				// 配对成功
  				x++;
  				y++;
  			}else if(next[y] == -1){ // y == 0
  				// 尝试下一个配对点
  				x++;
  			}else{
  				y = next[y];
  			}
  		}
  		return y == char2.length ? x - y  : -1;
  	}
  	public static int[] getNextArray(char[] str2) {
  		if (str2.length == 1) {
  			return new int[] { -1 };
  		}
  		int[] next = new int[str2.length];
  		next[0] = -1;
  		next[1] = 0;
  		int cnt = 0,i = 2;
  		while (i < next.length){
  			if(str2[i-1] == str2[cnt]){
  				// 配对成功
  				next[i++] = ++cnt;
  			}else if(cnt > 0){
  				// 去下一个位置的最后点判断
  				cnt = next[cnt];
  			}else{
  				// 到最后也没配对成功
  				next[i++] = 0;
  			}
  		}
  		return next;
  	}</code>  </pre>
  </details>

### IsSubTree

- 链接：<a href="https://leetcode.cn/problems/subtree-of-another-tree/description/">测试链接</a>

- 内容：

  > 给你两棵二叉树 `root` 和 `subRoot` 。检验 `root` 中是否包含和 `subRoot` 具有相同结构和节点值的子树。如果存在，返回 `true` ；否则，返回 `false` 。
  >
  > 二叉树 `tree` 的一棵子树包括 `tree` 的某个节点和这个节点的所有后代节点。`tree` 也可以看做它自身的一棵子树。
  >
  > **示例 1：**
  >
  > ![img](https://assets.leetcode.com/uploads/2021/04/28/subtree1-tree.jpg)
  >
  > ```
  > 输入：root = [3,4,5,1,2], subRoot = [4,1,2]
  > 输出：true
  > ```
  >
  > **示例 2：**
  >
  > ![img](https://assets.leetcode.com/uploads/2021/04/28/subtree2-tree.jpg)
  >
  > ```
  > 输入：root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
  > 输出：false
  > ```

- 思路：

  > 思路一：暴力尝试-略
  >
  > 思路二：KMP算法的实现，next生成不回退，next数组加速不回退
  >
  > ​	对数据进行前序序列化，null为"null"字符串，进行字符串匹配

- 代码：

  <details>
  <summary>是否为子树</summary>
  <p> - 匹配字符串</p>
  <pre><code>public static boolean isSubtree(TreeNode big, TreeNode small) {
      if (small == null) {
          return true;
      }
      if (big == null) {
          return false;
      }
      List<String> bList = preSerial(big);
      List<String> sList = preSerial(small);
      String[] bs = new String[bList.size()];
      String[] ss = new String[sList.size()];
      for (int i = 0; i < bList.size(); i++) {
          bs[i] = bList.get(i) == null ? "null" : bList.get(i);
      }
      for (int i = 0; i < sList.size(); i++) {
          ss[i] = sList.get(i) == null ? "null" : sList.get(i);
      }
      int index = getIndexOf(bs,ss);
      return index != -1;
  }
  public static ArrayList<String> preSerial(TreeNode head) {
      ArrayList<String> ans = new ArrayList<>();
      pres(head, ans);
      return ans;
  }
  public static void pres(TreeNode head, ArrayList<String> ans) {
      if (head == null) {
          ans.add(null);
          return;
      };
      ans.add(String.valueOf(head.val));
      pres(head.left, ans);
      pres(head.right, ans);
  }
  public static int getIndexOf(String[] str1, String[] str2) {
      if (str1.length < str2.length) return -1;
      int[] next = getNextArray(str2);
      int x = 0, y = 0;
      while (x < str1.length && y < str2.length) {
          if (str1[x].equals(str2[y])) {
              x++;
              y++;
          } else if (next[y] == -1) { // y = 0
              x++;
          } else {
              y = next[y];
          }
      }
      return y == str2.length ? x - y : -1;
  }
  public static int[] getNextArray(String[] ms) {
      if (ms.length == 1) return new int[]{-1};
      int[] next = new int[ms.length];
      next[0] = -1;
      next[1] = 0;
      int cnt = 0, i = 2;
      while (i < next.length) {
          if (ms[i - 1].equals(ms[cnt])) {
              next[i++] = ++cnt;
          } else if (cnt > 0) {
              cnt = next[cnt];
          } else {
              next[i++] = 0;
          }
      }
      return next;
  }</code>  </pre>
  </details>

### IsRotation

- 链接：<a href="https://github.com/xtpyip/blog-alogrithm/blob/main/alogrithm/src/main/java/blog/wstx/class27/Code03_IsRotation.java">测试链接</a>

- 内容：

  > 一个字符串是否能由另一个字符串旋转得到 。

- 思路：

  > 思路一：暴力尝试-略
  >
  > 思路二：KMP算法的实现，next生成不回退，next数组加速不回退
  >
  > ​	a是否为b的旋转字符串
  >
  > ​	字符串 d = b+b，变成a是否是d的子串

- 代码：

  <details>
  <summary>是否为旋转串</summary>
  <p> - 匹配字符串</p>
  <pre><code> public static boolean isRotation(String b,String a){
          if(b.length() != a.length()) return false;
          int n = b.length();
          char[] dChars = new char[n * 2];
          for (int i = 0; i < n; i++) {
              dChars[i] = b.charAt(i);
              dChars[n+i] = b.charAt(i);
          }
          char[] aChar = a.toCharArray();
          return indexOf(dChars,aChar) != -1;
      }
      public static int indexOf(char[] a,char[] b) {
          int x = 0, y = 0;
          int[] next = getNext(b);
          while (x < a.length && y < b.length) {
              if (a[x] == b[y]) {
                  x++;
                  y++;
              } else if (next[y] == -1) {
                  x++;
              } else {
                  y = next[y];
              }
          }
          return y == b.length ? x - y : -1;
      }
      public static int[] getNext(char[] b){
          if(b.length == 1) return new int[]{-1};
          int[] next = new int[b.length];
          next[0] = -1;
          next[1] = 0;
          int i = 2,cnt = 0;
          while (i < b.length){
              if(b[cnt] == b[i-1]){
                  next[i++] = ++cnt;
              }else if(cnt > 0){
                  cnt = next[cnt];
              }else{
                  next[i++] = 0;
              }
          }
          return next;
      }</code>  </pre>
  </details>