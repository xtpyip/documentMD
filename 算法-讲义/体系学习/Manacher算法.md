# Manacher

## 基本内容

- manacher

  > manacher是用来求取每个位置的回文字符串的长度的
  >
  > 它是一个不回退的算法，时间复杂度为O(n)
## 问题集合

### Manacher

- 链接：<a href="https://github.com/xtpyip/blog-alogrithm/blob/main/alogrithm/src/main/java/blog/wstx/class28/Code01_Manacher.java">测试链接</a>

- 内容：

  > 给你一个字符串 `s`，找到 `s` 中最长的 回文子串的长度。
  >
  > example:
  >
  > ​    babad->bab,aba->3
  
- 思路：

  > 思路一：暴力尝试（添加字符，直接向两侧扩）
  >
  > 思路二：manacher
  >
  > manacher算法：
  >
  > ​	将原始字符串的左右加上一个特殊字符标识，如#字符
  >
  > ​	将在哪个地方**C**能扩到的最远位置记下来，即i+R（i为下标，R为回文字符串的最大半径）
  >
  > ​	当i与i+R(下面统一用**R**表示)有不同的值时，有下面四种情况：
  >
  > ​	1》当i>**R**时，i只要向两侧扩展即可，暴力
  >
  > ​	2》当i<**R**时，存在三种情况
  >
  > ​		1》当【2*i - C】的左右都在【L，R】中时，i此时的值与【2*i - C】一样，可直接跳过
  >
  > ​		2》当【2i-C】的左边超过【L,R】时，i此时至少半径为【R-i】，直接从i+R处开始扩展
  >
  > ​        3》当【2i-C】的左边刚好压到L时，i此时半径为【R-i】
  
- 代码：

  <details>
  <summary>暴力尝试，使用字符加速</summary>
  <p> - 最长回文字符串长度</p>
  <pre><code>	public static int right(String s) {
  		if (s == null || s.length() == 0) {
  			return 0;
  		}
  		char[] str = manacherString(s);
  		int max = 0;
  		for (int i = 0; i < str.length; i++) {
  			int L = i - 1;
  			int R = i + 1;
  			while (L >= 0 && R < str.length && str[L] == str[R]) {
  				L--;
  				R++;
  			}
  			max = Math.max(max, R - L - 1);
  		}
  		return max / 2;
  	}</code>  </pre>
  </details>
  <details>
  <summary>manacher</summary>
  <p> - 最长回文字符串长度</p>
  <pre><code>public static int manacher(String s) {
  		if (s == null || s.length() == 0) {
  			return 0;
  		}
  		char[] str = manacherString(s);
  		// 回文半径的大小
  		int[] pArr = new int[str.length];
  		int C = -1;// 当前扩到最远R位置的那个下标 R = C + pArr[C]
  		int R = -1;// 当前搞到最远R的位置的下一个
  		int max = 1; // 最长回文字符串长度
  		for (int i = 0; i < str.length; i++) {
  			// 当前i如果在R内，则最少半径为min(pArr[2 * C - i],R - i)
  			// 当前i如果在R外，则最少半径为1
  			pArr[i] = R > i ? Math.min(pArr[2 * C - i],R - i) : 1;
  			// 尝试下一个对应的两个位置是否相等
  			while (i + pArr[i] < str.length && i - pArr[i] >= 0){
  				if(str[i + pArr[i]] == str[i - pArr[i]]){
  					pArr[i]++;
  				}else{
  					break; // 有不需要验的，第一次验证也会直接失败
  				}
  			}
  			if(i + pArr[i] > R){ // 可以扩充长度
  				C = i; // 扩充的下标
  				R = i + pArr[i];
  			}
  			max = Math.max(max,pArr[i]);
  		}
  	    return max - 1;
  	}
  	public static char[] manacherString(String str) {
  		char[] chars = new char[str.length() * 2 + 1];
  		chars[0] = '#';
  		for (int i = 0; i < str.length(); i++) {
  			chars[i * 2 + 1] = str.charAt(i);
  			chars[(i + 1) * 2] = '#';
  		}
  		return chars;
  	}</code>  </pre>
  </details>

### AddShortestEnd

- 链接：<a href="https://github.com/xtpyip/blog-alogrithm/blob/main/alogrithm/src/main/java/blog/wstx/class28/Code02_AddShortestEnd.java">测试链接</a>

- 内容：

  > 在给定的任一字符串中的后面加入一个字符串，使得此字符串变成回文字符串。
  >
  > 求能使其变成回文的长度最小的字符串是什么？

- 思路：

  > 任意一个字符串，只有回文子串的右边界刚好是最后一个字符时，所有添加的字符串最少
  >
  > ab123 ->21ba即可
  >
  > 可以将题意转化为求右边界为最后一个字符时的回文子串的回文半径的长度
  >
  > manacher算法求

- 代码：

  <details>
  <summary>manacher</summary>
  <p> - 最少长度字符串</p>
  <pre><code>public static String shortestEnd(String s) {
  		if (s == null || s.length() == 0) {
  			return null;
  		}
  		char[] str = manacherString(s);
  		int[] pArr = new int[str.length];
  		int C = -1;
  		int R = -1;
  		int maxContainsEnd = -1; // 右边界在str.length的最长半径
  		for (int i = 0; i < str.length; i++) {
  			pArr[i] = R > i ? Math.min(pArr[2*C - i],R - i) : 1;
  			while (i - pArr[i] >= 0 && i + pArr[i] < str.length){
  				if(str[i - pArr[i]] == str[i + pArr[i]]){
  					pArr[i]++;
  				}else{
  					break;
  				}
  			}
  			if(i + pArr[i] > R){
  				C = i;
  				R = i + pArr[i];
  			}
  			if(R == str.length){
  				maxContainsEnd = pArr[i];
  				break;
  			}
  		}
  		char[] res = new char[s.length() - (maxContainsEnd - 1)];
  		for (int i = 0; i < res.length; i++) {
  			res[res.length - 1 - i] = str[i * 2 + 1];
  		}
  		return String.valueOf(res);
  	}
  	public static char[] manacherString(String str) {
  		char[] charArr = str.toCharArray();
  		char[] res = new char[str.length() * 2 + 1];
  		int index = 0;
  		for (int i = 0; i != res.length; i++) {
  			res[i] = (i & 1) == 0 ? '#' : charArr[index++];
  		}
  		return res;
  	}</code>  </pre>
  </details>

### AddShortestStart

- 链接：<a href="https://leetcode.cn/problems/shortest-palindrome/description/">测试链接</a>

- 内容：

  > 给定一个字符串 ***s***，你可以通过在字符串前面添加字符将其转换为回文串。
  >
  > 找到并返回可以用这种方式转换的最短回文串。
  >
  > **示例 1：**
  >
  > ```
  > 输入：s = "aacecaaa"
  > 输出："aaacecaaa"
  > ```
  >
  > **示例 2：**
  >
  > ```
  > 输入：s = "abcd"
  > 输出："dcbabcd"
  > ```

- 思路：

  > 同AddShortestEnd思路一样，不过是要求包含最左边界的半径最大值

- 代码：

  <details>
  <summary>manacher实现</summary>
  <p> - 求最短回文串</p>
  <pre><code>public static String shortestPalindrome(String s) {
          if (s == null || s.length() == 0) {
              return "";
          }
          char[] str = manacherString(s);
          int[] pArr = new int[str.length];
          int C = -1;
          int R = -1;
          int maxContainsStart = -1; // 左边界在-1的最长半径
          for (int i = 0; i < str.length; i++) {
              pArr[i] = R > i ? Math.min(pArr[2*C - i],R - i) : 1;
              while (i - pArr[i] >= 0 && i + pArr[i] < str.length){
                  if(str[i - pArr[i]] == str[i + pArr[i]]){
                      pArr[i]++;
                  }else{
                      break;
                  }
              }
              if(i + pArr[i] > R){
                  C = i;
                  R = i + pArr[i];
              }
              if(2 * C  == R - 1){
                  maxContainsStart = Math.max(maxContainsStart,pArr[i]);
              }
          }
          char[] res = new char[s.length() - (maxContainsStart - 1)];
          for (int i = 0; i < res.length; i++) {
              res[res.length - 1 - i] = str[ ((maxContainsStart - 1)*2 + i*2 + 1)];
          }
          return String.valueOf(res)+s;
      }
      public static char[] manacherString(String str) {
          char[] charArr = str.toCharArray();
          char[] res = new char[str.length() * 2 + 1];
          int index = 0;
          for (int i = 0; i != res.length; i++) {
              res[i] = (i & 1) == 0 ? '#' : charArr[index++];
          }
          return res;
      }</code>  </pre>
  </details>
