# DC3生成后缀数组详解

## 基本内容

- 后缀数组

  > ![](http://8.130.177.90:9000/blog/24/alogrithm/wstx/class44/DC3.png)
  >
  > 如果我要对数组排序的话,按字符串的字典序来排,这个就是后缀数组
  >
  > 以某个位置开始后面整体的后缀串,它在所有开头位置的后缀串中排名第几,把它自己的排名作为一个数组,返回跟它对应的就是rank数组(原始下标按字典序的排名)
  >
  > 后缀数组跟rank数组就是一种转换关系,后缀数组可以在O(N)的时间内转化为rank数组
  >
  > rank数组可以在O(N)的时间内转化为后缀数组

## 问题集合

### DC3

- 链接：<a href="https://github.com/xtpyip/blog-alogrithm/blob/main/alogrithm/src/main/java/blog/wstx/class44/DC3.java">测试链接</a>

- 内容：

  > DC3算法
  
- 思路：

  > 使用%3来进行数据的分类，对S1(%3=1)和S2(%3=2)的数据进行排序，最少需要3次出入桶
  >
  > 若存在同排名，则将S1+分隔+S2组成新数组，进行一次桶排序即可确定同排名的准确排名。
  >
  > 注意事项，
  >
  > 1、DC3算法是使用了桶排序的思路，默认最小的分隔值为1
  >
  > 所有的字符串都可以对应char数组，都可以转化为int数组，把int数组的值全部+同一个值，化为>=2的值，在末尾补1
  >
  > 2、为了减少常数，可以将[1,34,100万，10亿]的数据转化为[2,3,4,5,1]最后一个1是分隔数据，可以大大节省桶的数量
  
- 代码：

  <details>
  <summary>DC3算法</summary>
  <p> - DC3代码实现</p>
  <pre><code>public class DC3 {
  	public int[] sa;
  	public int[] rank;
  	public int[] height;
  	// 构造方法的约定:
  	// 数组叫nums，如果你是字符串，请转成整型数组nums
  	// 数组中，最小值>=1
  	// 如果不满足，处理成满足的，也不会影响使用
  	// max, nums里面最大值是多少
  	public DC3(int[] nums, int max) {
  		sa = sa(nums, max);
  		rank = rank();
  		height = height(nums);
  	}
  	private int[] sa(int[] nums, int max) {
  		int n = nums.length;
  		int[] arr = new int[n + 3];
  		for (int i = 0; i < n; i++) {
  			arr[i] = nums[i];
  		}
  		return skew(arr, n, max);
  	}
  	private int[] skew(int[] nums, int n, int K) {
  		int n0 = (n + 2) / 3, n1 = (n + 1) / 3, n2 = n / 3, n02 = n0 + n2;
  		int[] s12 = new int[n02 + 3], sa12 = new int[n02 + 3];
  		for (int i = 0, j = 0; i < n + (n0 - n1); ++i) {
  			if (0 != i % 3) {
  				s12[j++] = i;
  			}
  		}
  		radixPass(nums, s12, sa12, 2, n02, K);
  		radixPass(nums, sa12, s12, 1, n02, K);
  		radixPass(nums, s12, sa12, 0, n02, K);
  		int name = 0, c0 = -1, c1 = -1, c2 = -1;
  		for (int i = 0; i < n02; ++i) {
  			if (c0 != nums[sa12[i]] || c1 != nums[sa12[i] + 1] || c2 != nums[sa12[i] + 2]) {
  				name++;
  				c0 = nums[sa12[i]];
  				c1 = nums[sa12[i] + 1];
  				c2 = nums[sa12[i] + 2];
  			}
  			if (1 == sa12[i] % 3) {
  				s12[sa12[i] / 3] = name;
  			} else {
  				s12[sa12[i] / 3 + n0] = name;
  			}
  		}
  		if (name < n02) {
  			sa12 = skew(s12, n02, name);
  			for (int i = 0; i < n02; i++) {
  				s12[sa12[i]] = i + 1;
  			}
  		} else {
  			for (int i = 0; i < n02; i++) {
  				sa12[s12[i] - 1] = i;
  			}
  		}
  		int[] s0 = new int[n0], sa0 = new int[n0];
  		for (int i = 0, j = 0; i < n02; i++) {
  			if (sa12[i] < n0) {
  				s0[j++] = 3 * sa12[i];
  			}
  		}
  		radixPass(nums, s0, sa0, 0, n0, K);
  		int[] sa = new int[n];
  		for (int p = 0, t = n0 - n1, k = 0; k < n; k++) {
  			int i = sa12[t] < n0 ? sa12[t] * 3 + 1 : (sa12[t] - n0) * 3 + 2;
  			int j = sa0[p];
  			if (sa12[t] < n0 ? leq(nums[i], s12[sa12[t] + n0], nums[j], s12[j / 3])
  					: leq(nums[i], nums[i + 1], s12[sa12[t] - n0 + 1], nums[j], nums[j + 1], s12[j / 3 + n0])) {
  				sa[k] = i;
  				t++;
  				if (t == n02) {
  					for (k++; p < n0; p++, k++) {
  						sa[k] = sa0[p];
  					}
  				}
  			} else {
  				sa[k] = j;
  				p++;
  				if (p == n0) {
  					for (k++; t < n02; t++, k++) {
  						sa[k] = sa12[t] < n0 ? sa12[t] * 3 + 1 : (sa12[t] - n0) * 3 + 2;
  					}
  				}
  			}
  		}
  		return sa;
  	}
  	private void radixPass(int[] nums, int[] input, int[] output, int offset, int n, int k) {
  		int[] cnt = new int[k + 1];
  		for (int i = 0; i < n; ++i) {
  			cnt[nums[input[i] + offset]]++;
  		}
  		for (int i = 0, sum = 0; i < cnt.length; ++i) {
  			int t = cnt[i];
  			cnt[i] = sum;
  			sum += t;
  		}
  		for (int i = 0; i < n; ++i) {
  			output[cnt[nums[input[i] + offset]]++] = input[i];
  		}
  	}
  	private boolean leq(int a1, int a2, int b1, int b2) {
  		return a1 < b1 || (a1 == b1 && a2 <= b2);
  	}
  	private boolean leq(int a1, int a2, int a3, int b1, int b2, int b3) {
  		return a1 < b1 || (a1 == b1 && leq(a2, a3, b2, b3));
  	}
  	private int[] rank() {
  		int n = sa.length;
  		int[] ans = new int[n];
  		for (int i = 0; i < n; i++) {
  			ans[sa[i]] = i;
  		}
  		return ans;
  	}
  	private int[] height(int[] s) {
  		int n = s.length;
  		int[] ans = new int[n];
  		for (int i = 0, k = 0; i < n; ++i) {
  			if (rank[i] != 0) {
  				if (k > 0) {
  					--k;
  				}
  				int j = sa[rank[i] - 1];
  				while (i + k < n && j + k < n && s[i + k] == s[j + k]) {
  					++k;
  				}
  				ans[rank[i]] = k;
  			}
  		}
  		return ans;
  	}
  }</code>  </pre>
  </details>

### LastSubstringInLexicographicalOrder

- 链接：<a href="https://leetcode.cn/problems/last-substring-in-lexicographical-order/description/">测试链接</a>

- 内容：

  > 给你一个字符串 `s` ，找出它的所有子串并按字典序排列，返回排在最后的那个子串。
  >
  > **示例 1：**
  >
  > ```
  > 输入：s = "abab"
  > 输出："bab"
  > 解释：我们可以找出 7 个子串 ["a", "ab", "aba", "abab", "b", "ba", "bab"]。按字典序排在最后的子串是 "bab"。
  > ```
  >
  > **示例 2：**
  >
  > ```
  > 输入：s = "leetcode"
  > 输出："tcode"
  > ```

- 思路：

  > DC3算法直接从sa中获取最后一个后缀串的开始下标进行全局截取
  
- 代码：

  <details>
  <summary>DC3</summary>
  <p> - 排最后的子串</p>
  <pre><code>	public static String lastSubstring(String s) {
  		if (s == null || s.length() == 0) {
  			return s;
  		}
  		int N = s.length();
  		char[] str = s.toCharArray();
  		int min = Integer.MAX_VALUE;
  		int max = Integer.MIN_VALUE;
  		for (char cha : str) {
  			min = Math.min(min, cha);
  			max = Math.max(max, cha);
  		}
  		int[] arr = new int[N];
  		for (int i = 0; i < N; i++) {
  			arr[i] = str[i] - min + 1;
  		}
  		DC3 dc3 = new DC3(arr, max - min + 1);
  		return s.substring(dc3.sa[N - 1]);
  	}
  	public static class DC3 {
  		public int[] sa;
  		public DC3(int[] nums, int max) {
  			sa = sa(nums, max);
  		}
  		private int[] sa(int[] nums, int max) {
  			int n = nums.length;
  			int[] arr = new int[n + 3];
  			for (int i = 0; i < n; i++) {
  				arr[i] = nums[i];
  			}
  			return skew(arr, n, max);
  		}
  		private int[] skew(int[] nums, int n, int K) {
  			int n0 = (n + 2) / 3, n1 = (n + 1) / 3, n2 = n / 3, n02 = n0 + n2;
  			int[] s12 = new int[n02 + 3], sa12 = new int[n02 + 3];
  			for (int i = 0, j = 0; i < n + (n0 - n1); ++i) {
  				if (0 != i % 3) {
  					s12[j++] = i;
  				}
  			}
  			radixPass(nums, s12, sa12, 2, n02, K);
  			radixPass(nums, sa12, s12, 1, n02, K);
  			radixPass(nums, s12, sa12, 0, n02, K);
  			int name = 0, c0 = -1, c1 = -1, c2 = -1;
  			for (int i = 0; i < n02; ++i) {
  				if (c0 != nums[sa12[i]] || c1 != nums[sa12[i] + 1] || c2 != nums[sa12[i] + 2]) {
  					name++;
  					c0 = nums[sa12[i]];
  					c1 = nums[sa12[i] + 1];
  					c2 = nums[sa12[i] + 2];
  				}
  				if (1 == sa12[i] % 3) {
  					s12[sa12[i] / 3] = name;
  				} else {
  					s12[sa12[i] / 3 + n0] = name;
  				}
  			}
  			if (name < n02) {
  				sa12 = skew(s12, n02, name);
  				for (int i = 0; i < n02; i++) {
  					s12[sa12[i]] = i + 1;
  				}
  			} else {
  				for (int i = 0; i < n02; i++) {
  					sa12[s12[i] - 1] = i;
  				}
  			}
  			int[] s0 = new int[n0], sa0 = new int[n0];
  			for (int i = 0, j = 0; i < n02; i++) {
  				if (sa12[i] < n0) {
  					s0[j++] = 3 * sa12[i];
  				}
  			}
  			radixPass(nums, s0, sa0, 0, n0, K);
  			int[] sa = new int[n];
  			for (int p = 0, t = n0 - n1, k = 0; k < n; k++) {
  				int i = sa12[t] < n0 ? sa12[t] * 3 + 1 : (sa12[t] - n0) * 3 + 2;
  				int j = sa0[p];
  				if (sa12[t] < n0 ? leq(nums[i], s12[sa12[t] + n0], nums[j], s12[j / 3])
  						: leq(nums[i], nums[i + 1], s12[sa12[t] - n0 + 1], nums[j], nums[j + 1], s12[j / 3 + n0])) {
  					sa[k] = i;
  					t++;
  					if (t == n02) {
  						for (k++; p < n0; p++, k++) {
  							sa[k] = sa0[p];
  						}
  					}
  				} else {
  					sa[k] = j;
  					p++;
  					if (p == n0) {
  						for (k++; t < n02; t++, k++) {
  							sa[k] = sa12[t] < n0 ? sa12[t] * 3 + 1 : (sa12[t] - n0) * 3 + 2;
  						}
  					}
  				}
  			}
  			return sa;
  		}
  		private void radixPass(int[] nums, int[] input, int[] output, int offset, int n, int k) {
  			int[] cnt = new int[k + 1];
  			for (int i = 0; i < n; ++i) {
  				cnt[nums[input[i] + offset]]++;
  			}
  			for (int i = 0, sum = 0; i < cnt.length; ++i) {
  				int t = cnt[i];
  				cnt[i] = sum;
  				sum += t;
  			}
  			for (int i = 0; i < n; ++i) {
  				output[cnt[nums[input[i] + offset]]++] = input[i];
  			}
  		}
  		private boolean leq(int a1, int a2, int b1, int b2) {
  			return a1 < b1 || (a1 == b1 && a2 <= b2);
  		}
  		private boolean leq(int a1, int a2, int a3, int b1, int b2, int b3) {
  			return a1 < b1 || (a1 == b1 && leq(a2, a3, b2, b3));
  		}
  	}</code>  </pre>
  </details>
