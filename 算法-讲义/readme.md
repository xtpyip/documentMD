# 算法

## algorithmbasic2020

### class01

#### selectSort

- 链接：暂无

- 内容：

  > 将指定的数组排序

- 思路：

  >第一轮，查找1~N的最小值与0位置交换
  >
  >第二轮，查找2~N的最小值与1位置交换
  >
  >...
  >
  >第n-1轮，查找n-1~N的最小值与n-2位置交换

- 代码：

  ```java
  // 选择排序
      public static void selectSort(int[] arr){
          if(arr == null || arr.length < 2)
              return;
  
          for (int i = 0; i < arr.length-1; i++) {
               int minIndex = i;
              for (int j = minIndex+1; j < arr.length; j++) {
                  minIndex = arr[j] < arr[minIndex] ? j : minIndex;
              }
              swap(arr,minIndex,i);
          }
      }
      public static void swap(int[] arr,int i,int j){
          int temp = arr[i];
          arr[i] = arr[j];
          arr[j] = temp;
      }
  ```

  

#### bubbleSort

- 链接：暂无

- 内容：

  > 将指定数组排序

- 思路：

  > 第一轮：从0~N-1,当i<i+1 且num[i]>num[i+1] 时,i与j对应的值相交换
  >
  > ....

- 代码：

  ```java
  // 冒泡排序
  public static void bubbleSort(int[] arr) {
  		if (arr == null || arr.length < 2) {
  			return;
  		}
  		// 0 ~ N-1
  		// 0 ~ N-2
  		// 0 ~ N-3
  		for (int e = arr.length - 1; e > 0; e--) { // 0 ~ e
  			for (int i = 0; i < e; i++) {
  				if (arr[i] > arr[i + 1]) {
  					swap(arr, i, i + 1);
  				}
  			}
  		}
  	}
  ```

  

#### insertSort

- 链接：暂无

- 内容：

  > 将指定数组排序

- 思路：

  > 将当前数据与前面已经排好序的数据进行处理，插入进指定位置

- 代码：

  ```java
  public static void insertionSort(int[] arr) {
  		if (arr == null || arr.length < 2) {
  			return;
  		}
  		// 不只1个数
  		for (int i = 1; i < arr.length; i++) { // 0 ~ i 做到有序
  			for (int j = i - 1; j >= 0 && arr[j] > arr[j + 1]; j--) {
  				swap(arr, j, j + 1);
  			}
  		}
  	}
  ```

  

#### BSExist

- 链接：暂无

- 内容：

  > 有序数组中是否存在num

- 思路：

  > 迭代搜索查找

- 代码：

  ```java
  public static boolean exist(int[] sortedArr, int num) {
  		if (sortedArr == null || sortedArr.length == 0) {
  			return false;
  		}
  		int L = 0;
  		int R = sortedArr.length - 1;
  		int mid = 0;
  		// L..R
  		while (L < R) { // L..R 至少两个数的时候
  			mid = L + ((R - L) >> 1);
  			if (sortedArr[mid] == num) {
  				return true;
  			} else if (sortedArr[mid] > num) {
  				R = mid - 1;
  			} else {
  				L = mid + 1;
  			}
  		}
  		return sortedArr[L] == num;
  	}
  ```

  

#### BSNearLeft

- 链接：暂无

- 内容：

  > 在有序arr上，找满足>=value的最左位置

- 思路：

  > 迭代遍历

- 代码：

  ```java
  	public static int nearestIndex(int[] arr, int value) {
  		int L = 0;
  		int R = arr.length - 1;
  		int index = -1; // 记录最左的对号
  		while (L <= R) { // 至少一个数的时候
  			int mid = L + ((R - L) >> 1);
  			if (arr[mid] >= value) {
  				index = mid;
  				R = mid - 1;
  			} else {
  				L = mid + 1;
  			}
  		}
  		return index;
  	}
  ```

  

#### BSNearRight

- 链接：暂无

- 内容：

  > 在有序arr上，找满足<=value的最右位置

- 思路：

  > 迭代遍历

- 代码：

  ```java
  	public static int nearestIndex(int[] arr, int value) {
  		int L = 0;
  		int R = arr.length - 1;
  		int index = -1; // 记录最右的对号
  		while (L <= R) {
  			int mid = L + ((R - L) >> 1);
  			if (arr[mid] <= value) {
  				index = mid;
  				L = mid + 1;
  			} else {
  				R = mid - 1;
  			}
  		}
  		return index;
  	}
  ```

  

#### BSAwesome

- 链接：暂无

- 内容：

  > 返回局部最小值所在的下标，此下标的值小于左右值（存在）

- 思路：

  > 判断两端是否存在，若存在则返回
  >
  > 对左右进行迭代遍历，取得当前的mid
  >
  > ​	若【mid】> 【mid-1】则【L,mid-1】一定有局部最小值
  >
  > ​	若【mid】> 【mid+1】则【mid+1,R】一定有局部最小值
  >
  > ​    否则【mid】< 【mid-1】且【mid】<【mid+1】,返回mid

- 代码：

  ```java
  public static int getLessIndex(int[] arr) {
  		if (arr == null || arr.length == 0) {
  			return -1;
  		}
  		if (arr.length == 1 || arr[0] < arr[1]) {
  			return 0;
  		}
  		if (arr[arr.length - 1] < arr[arr.length - 2]) {
  			return arr.length - 1;
  		}
  		int left = 1;
  		int right = arr.length - 2;
  		int mid = 0;
  		while (left < right) {
  			mid = (left + right) / 2;
  			if (arr[mid] > arr[mid - 1]) {
  				right = mid - 1;
  			} else if (arr[mid] > arr[mid + 1]) {
  				left = mid + 1;
  			} else {
  				return mid;
  			}
  		}
  		return left;
  	}
  ```



### class02

#### swap

- 链接：暂无

- 内容：

  > 给两个数字a与b,要求a与b的值相互交换

- 思路：

  > 思路1：使用临时变量
  >
  > 思路2：异或
  >
  > ​	原a,b
  >
  > ​	a = a^b
  >
  > ​	b = a^b=(a^b)^b=a
  >
  > ​	a = a^b=(a^b)^(a^b^b)=b

- 代码：

  ```java
  public static void swap (int[] arr, int i, int j) {
  		// arr[0] = arr[0] ^ arr[0];
  		int temp  = arr[j];
  		arr[j]  = arr[i];
  		arr[i]  = temp;
  	}
  public static void swap (int[] arr, int i, int j) {
  		// arr[0] = arr[0] ^ arr[0];
  		arr[i]  = arr[i] ^ arr[j];
  		arr[j]  = arr[i] ^ arr[j];
  		arr[i]  = arr[i] ^ arr[j];
  	}
  ```

  

#### evenTimesOddTimes

##### oneOdd

- 链接：暂无

- 内容

  > arr中，只有一种数，出现奇数次，求这个数字

- 思路：

  > 异或，异或的性质为同为0，且无关顺序

- 代码：

  ```java
  public static void printOddTimesNum1(int[] arr) {
  		int eor = 0;
  		for (int i = 0; i < arr.length; i++) {
  			eor ^= arr[i];
  		}
  		System.out.println(eor);
  	}
  ```

  

##### twoOdd

- 链接：暂无

- 内容

  > arr中，只有两种数，出现奇数次，求这两个数字

- 思路：

  > 异或，异或的性质为同为0，且无关顺序
  >
  > ​	遍历整个数组，异或后的结果实际上等价于这两个出现奇数次的数字异或的结果
  >
  > ​	这个结果肯定不等于0（两种数），那么这个数的32位上肯定有等于1的存在
  >
  > ​	把某一位上是否等于1的数字可以把arr划分成两组，且这两组刚好各包含一个不同的出现奇数次的数字
  >
  > ​	把问题转化为了oneOdd

- 代码：

  ```java
  // arr中，有两种数，出现奇数次
  	public static void printOddTimesNum2(int[] arr) {
  		int eor = 0;
  		for (int i = 0; i < arr.length; i++) {
  			eor ^= arr[i];
  		}
  		// a 和 b是两种数
  		// eor != 0
  		// eor最右侧的1，提取出来
  		// eor :     00110010110111000
  		// rightOne :00000000000001000
  		int rightOne = eor & (-eor); // 提取出最右的1
  		int onlyOne = 0; // eor'
  		for (int i = 0 ; i < arr.length;i++) {
  			//  arr[1] =  111100011110000
  			// rightOne=  000000000010000
  			if ((arr[i] & rightOne) != 0) {
  				onlyOne ^= arr[i];
  			}
  		}
  		System.out.println(onlyOne + " " + (eor ^ onlyOne));
  	}
  ```

#### KM

- 链接：暂无

- 内容：

  >  输入一定能够保证，数组中所有的数都出现了M次，只有一种数出现了K次，且1 <= K < M
  >
  >  返回这种数

- 思路：

  > 遍历数组，把数组中的数字对应位数值为1的数据+1
  >
  > 任意位数数值%M不等于0的表明要返回的这种数在这个位置上有1这个值
  >
  > 统计32位所有的数据，返回

- 代码：

  ```java
  	public static int km(int[] arr, int k, int m) {
  		int[] help = new int[32];
  		for (int num : arr) {
  			for (int i = 0; i < 32; i++) {
  				help[i] += (num >> i) & 1;
  			}
  		}
  		int ans = 0;
  		for (int i = 0; i < 32; i++) {
  			help[i] %= m;
  			if (help[i] != 0) {
  				ans |= 1 << i;
  			}
  		}
  		return ans;
  	}
  
  ```

### class28

#### Manacher

- 链接：https://leetcode.cn/problems/longest-palindromic-substring/description/（类似）

- 内容：

  > 给你一个字符串 `s`，找到 `s` 中最长的 回文子串的长度。
  >
  > example:
  >
  > ​    babad->bab,aba->3

- 思路：

  > manacher算法：
  >
  > ​	将原始字符串的左右加上一个特殊字符标识，如#字符
  >
  > ​	将之前的位置的能扩到的位置记下来，即i+R（i为下标，R为回文字符串的最大半径）
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

  ```java
  	public static int manacher(String s) {
  		if (s == null || s.length() == 0) {
  			return 0;
  		}
  		// "12132" -> "#1#2#1#3#2#"
  		char[] str = manacherString(s);
  		// 回文半径的大小
  		int[] pArr = new int[str.length];
  		int C = -1;
  		// 讲述中：R代表最右的扩成功的位置
  		// coding：最右的扩成功位置的，再下一个位置
  		int R = -1;
  		int max = Integer.MIN_VALUE;
  		for (int i = 0; i < str.length; i++) { // 0 1 2
  			// R第一个违规的位置，i>= R
  			// i位置扩出来的答案，i位置扩的区域，至少是多大。
  			pArr[i] = R > i ? Math.min(pArr[2 * C - i], R - i) : 1;
              // 统一都走这个地方，当不满足时，进去一次就直接跳出了
  			while (i + pArr[i] < str.length && i - pArr[i] > -1) {
  				if (str[i + pArr[i]] == str[i - pArr[i]])
  					pArr[i]++;
  				else {
  					break;
  				}
  			}
              // 更新R的值，及使R更新的C的值
  			if (i + pArr[i] > R) {
  				R = i + pArr[i];
  				C = i;
  			}
              // 记录最大的回文串的半径长度
  			max = Math.max(max, pArr[i]);
  		}
          // 半径长度-1就等于所求的原回文串的长度
  		return max - 1;
  	}
  
  	public static char[] manacherString(String str) {
  		char[] charArr = str.toCharArray();
  		char[] res = new char[str.length() * 2 + 1];
  		int index = 0;
  		for (int i = 0; i != res.length; i++) {
  			res[i] = (i & 1) == 0 ? '#' : charArr[index++];
  		}
  		return res;
  	}
  ```

  

#### AddShortestEnd

- 链接：暂无

- 内容：

  > 在给定的任一字符串中的后面加入一个字符串，使得此字符串变成回文字符串。
  >
  > 求能使其变成回文的长度最小的字符串为什么？

- 思路：

  > 任意一个字符串，只有回文子串的右边界刚好是最后一个字符时，所有添加的字符串最少
  >
  > ab123 ->21ba即可
  >
  > 可以将题意转化为求右边界为最后一个字符时的回文子串的回文半径的长度
  >
  > manacher算法求

- 代码：

  ```java
  public static String shortestEnd(String s) {
  		if (s == null || s.length() == 0) {
  			return null;
  		}
  		char[] str = manacherString(s);
  		int[] pArr = new int[str.length];
  		int C = -1;
  		int R = -1;
  		int maxContainsEnd = -1;
  		for (int i = 0; i != str.length; i++) {
  			pArr[i] = R > i ? Math.min(pArr[2 * C - i], R - i) : 1;
  			while (i + pArr[i] < str.length && i - pArr[i] > -1) {
  				if (str[i + pArr[i]] == str[i - pArr[i]])
  					pArr[i]++;
  				else {
  					break;
  				}
  			}
  			if (i + pArr[i] > R) {
  				R = i + pArr[i];
  				C = i;
  			}
  			if (R == str.length) {
                  // 当最右压住了最后一个字符时，返回
  				maxContainsEnd = pArr[i];
  				break;
  			}
  		}
          // 返回去除原回文半径的长度的长度的子串
  		char[] res = new char[s.length() - maxContainsEnd + 1];
          // 将需要添加的字符从回文串的最左侧的上一个逆序添加
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
  	}
  ```

### class29

#### findMinKth

- 链接：暂无

- 内容：

  > 给定一个混乱数组，求这个数组中的第k小的数

- 思路：

  > 思路1：全体排序，取第k小，略 O(NlogN)
  >
  > 思路2：利用大根堆（小根堆） O(NlogN)
  >
  > 思路3：改写快排（递归，迭代） O(N)
  >
  > 思路4：bfprt算法（同思路3，不过取flag值使用的是bfprt，使概率随机变成可计算）O(N)

- 代码：

  ```java
  	public static class MaxHeapComparator implements Comparator<Integer> {
  
  		@Override
  		public int compare(Integer o1, Integer o2) {
  			return o2 - o1;
  		}
  
  	}
  
  	// 利用大根堆，时间复杂度O(N*logK)
  	public static int minKth1(int[] arr, int k) {
  		PriorityQueue<Integer> maxHeap = new PriorityQueue<>(new MaxHeapComparator());
  		for (int i = 0; i < k; i++) {
  			maxHeap.add(arr[i]);
  		}
  		for (int i = k; i < arr.length; i++) {
  			if (arr[i] < maxHeap.peek()) {
  				maxHeap.poll();
  				maxHeap.add(arr[i]);
  			}
  		}
  		return maxHeap.peek();
  	}
  // 改写快排，时间复杂度O(N)
  	// k >= 1
  	public static int minKth2(int[] array, int k) {
  		int[] arr = copyArray(array);
  		return process2(arr, 0, arr.length - 1, k - 1);
  	}
  
  	public static int[] copyArray(int[] arr) {
  		int[] ans = new int[arr.length];
  		for (int i = 0; i != ans.length; i++) {
  			ans[i] = arr[i];
  		}
  		return ans;
  	}
  
  	// arr 第k小的数
  	// process2(arr, 0, N-1, k-1)
  	// arr[L..R]  范围上，如果排序的话(不是真的去排序)，找位于index的数
  	// index [L..R]
  	public static int process2(int[] arr, int L, int R, int index) {
  		if (L == R) { // L = =R ==INDEX
  			return arr[L];
  		}
  		// 不止一个数  L +  [0, R -L]
  		int pivot = arr[L + (int) (Math.random() * (R - L + 1))];
  		int[] range = partition(arr, L, R, pivot);
  		if (index >= range[0] && index <= range[1]) {
  			return arr[index];
  		} else if (index < range[0]) {
  			return process2(arr, L, range[0] - 1, index);
  		} else {
  			return process2(arr, range[1] + 1, R, index);
  		}
  	}
  
  	public static int[] partition(int[] arr, int L, int R, int pivot) {
  		int less = L - 1;
  		int more = R + 1;
  		int cur = L;
  		while (cur < more) {
  			if (arr[cur] < pivot) {
  				swap(arr, ++less, cur++);
  			} else if (arr[cur] > pivot) {
  				swap(arr, cur, --more);
  			} else {
  				cur++;
  			}
  		}
  		return new int[] { less + 1, more - 1 };
  	}
  
  	public static void swap(int[] arr, int i1, int i2) {
  		int tmp = arr[i1];
  		arr[i1] = arr[i2];
  		arr[i2] = tmp;
  	}
  // 利用bfprt算法，时间复杂度O(N)
  	public static int minKth3(int[] array, int k) {
  		int[] arr = copyArray(array);
  		return bfprt(arr, 0, arr.length - 1, k - 1);
  	}
  
  	// arr[L..R]  如果排序的话，位于index位置的数，是什么，返回
  	public static int bfprt(int[] arr, int L, int R, int index) {
  		if (L == R) {
  			return arr[L];
  		}
  		// L...R  每五个数一组
  		// 每一个小组内部排好序
  		// 小组的中位数组成新数组
  		// 这个新数组的中位数返回
  		int pivot = medianOfMedians(arr, L, R);
  		int[] range = partition(arr, L, R, pivot);
  		if (index >= range[0] && index <= range[1]) {
  			return arr[index];
  		} else if (index < range[0]) {
  			return bfprt(arr, L, range[0] - 1, index);
  		} else {
  			return bfprt(arr, range[1] + 1, R, index);
  		}
  	}
  
  	// arr[L...R]  五个数一组
  	// 每个小组内部排序
  	// 每个小组中位数领出来，组成marr
  	// marr中的中位数，返回
  	public static int medianOfMedians(int[] arr, int L, int R) {
  		int size = R - L + 1;
  		int offset = size % 5 == 0 ? 0 : 1;
  		int[] mArr = new int[size / 5 + offset];
  		for (int team = 0; team < mArr.length; team++) {
  			int teamFirst = L + team * 5;
  			// L ... L + 4
  			// L +5 ... L +9
  			// L +10....L+14
  			mArr[team] = getMedian(arr, teamFirst, Math.min(R, teamFirst + 4));
  		}
  		// marr中，找到中位数
  		// marr(0, marr.len - 1,  mArr.length / 2 )
  		return bfprt(mArr, 0, mArr.length - 1, mArr.length / 2);
  	}
  
  	public static int getMedian(int[] arr, int L, int R) {
  		insertionSort(arr, L, R);
  		return arr[(L + R) / 2];
  	}
  
  	public static void insertionSort(int[] arr, int L, int R) {
  		for (int i = L + 1; i <= R; i++) {
  			for (int j = i - 1; j >= L && arr[j] > arr[j + 1]; j--) {
  				swap(arr, j, j + 1);
  			}
  		}
  	}
  ```

  

#### maxTopK

- 链接：暂无

- 内容：

  > 给定一个混乱数组，查找当前的前K个大的的数字，并按从大到小的顺序返回

- 思路：

  > 思路1：排序+收集，时间复杂度(O(N*logN))
  >
  > 思路2：大根堆+收集 时间复杂度(O(N + k*logN))
  >
  > 思路3：bfprt+排序收集 时间复杂度(O(N+k*logk))
  >
  > ​	先得到N-K小的数（findMinKth)
  >
  > ​	再遍历数组将所有的大于N-K小的数收集
  >
  > ​	在长度为k的数组长度中进行排序
  >
  > ​	返回

- 代码：

  ```java
  	// 时间复杂度O(N*logN)
  	// 排序+收集
  	public static int[] maxTopK1(int[] arr, int k) {
  		if (arr == null || arr.length == 0) {
  			return new int[0];
  		}
  		int N = arr.length;
  		k = Math.min(N, k);
  		Arrays.sort(arr);
  		int[] ans = new int[k];
  		for (int i = N - 1, j = 0; j < k; i--, j++) {
  			ans[j] = arr[i];
  		}
  		return ans;
  	}
  
  	// 方法二，时间复杂度O(N + K*logN)
  	// 解释：堆
  	public static int[] maxTopK2(int[] arr, int k) {
  		if (arr == null || arr.length == 0) {
  			return new int[0];
  		}
  		int N = arr.length;
  		k = Math.min(N, k);
  		// 从底向上建堆，时间复杂度O(N)
  		for (int i = N - 1; i >= 0; i--) {
  			heapify(arr, i, N);
  		}
  		// 只把前K个数放在arr末尾，然后收集，O(K*logN)
  		int heapSize = N;
  		swap(arr, 0, --heapSize);
  		int count = 1;
  		while (heapSize > 0 && count < k) {
  			heapify(arr, 0, heapSize);
  			swap(arr, 0, --heapSize);
  			count++;
  		}
  		int[] ans = new int[k];
  		for (int i = N - 1, j = 0; j < k; i--, j++) {
  			ans[j] = arr[i];
  		}
  		return ans;
  	}
  
  	public static void heapInsert(int[] arr, int index) {
  		while (arr[index] > arr[(index - 1) / 2]) {
  			swap(arr, index, (index - 1) / 2);
  			index = (index - 1) / 2;
  		}
  	}
  
  	public static void heapify(int[] arr, int index, int heapSize) {
  		int left = index * 2 + 1;
  		while (left < heapSize) {
  			int largest = left + 1 < heapSize && arr[left + 1] > arr[left] ? left + 1 : left;
  			largest = arr[largest] > arr[index] ? largest : index;
  			if (largest == index) {
  				break;
  			}
  			swap(arr, largest, index);
  			index = largest;
  			left = index * 2 + 1;
  		}
  	}
  
  	public static void swap(int[] arr, int i, int j) {
  		int tmp = arr[i];
  		arr[i] = arr[j];
  		arr[j] = tmp;
  	}
  
  	// 方法三，时间复杂度O(n + k * logk)
  	public static int[] maxTopK3(int[] arr, int k) {
  		if (arr == null || arr.length == 0) {
  			return new int[0];
  		}
  		int N = arr.length;
  		k = Math.min(N, k);
  		// O(N)
  		int num = minKth(arr, N - k);
  		int[] ans = new int[k];
  		int index = 0;
  		for (int i = 0; i < N; i++) {
  			if (arr[i] > num) {
  				ans[index++] = arr[i];
  			}
  		}
  		for (; index < k; index++) {
  			ans[index] = num;
  		}
  		// O(k*logk)
  		Arrays.sort(ans);
  		for (int L = 0, R = k - 1; L < R; L++, R--) {
  			swap(ans, L, R);
  		}
  		return ans;
  	}
  
  	// 时间复杂度O(N)
  	public static int minKth(int[] arr, int index) {
  		int L = 0;
  		int R = arr.length - 1;
  		int pivot = 0;
  		int[] range = null;
  		while (L < R) {
  			pivot = arr[L + (int) (Math.random() * (R - L + 1))];
  			range = partition(arr, L, R, pivot);
  			if (index < range[0]) {
  				R = range[0] - 1;
  			} else if (index > range[1]) {
  				L = range[1] + 1;
  			} else {
  				return pivot;
  			}
  		}
  		return arr[L];
  	}
  
  	public static int[] partition(int[] arr, int L, int R, int pivot) {
  		int less = L - 1;
  		int more = R + 1;
  		int cur = L;
  		while (cur < more) {
  			if (arr[cur] < pivot) {
  				swap(arr, ++less, cur++);
  			} else if (arr[cur] > pivot) {
  				swap(arr, cur, --more);
  			} else {
  				cur++;
  			}
  		}
  		return new int[] { less + 1, more - 1 };
  	}
  }
  ```

  

#### reservoirSampling

- 链接：暂无

- 内容：

  > 给定一个数据输入流，要让当前及之前的所有的数据都要以同样的概率放入袋子中，假设此袋子的长度为k，当前数为n，则1~n的每个数据都要以相同概率进入，等价于n个数据选入10个数据。

- 思路：

  > 先让前k个数据直接入袋
  >
  > 当前数据为i,以k/i的概率决定要不要入袋，如果不入，则进入下一个i+1数据进行判断
  >
  > 如果进入，以1/k的概率选中要进入哪个位置
  >
  > 即此数据以k/i * 1/k的概率要入袋，即1/i的概率要入袋，前1~i的数据均是如此。

- 代码：

  ```java
  public static class RandomBox {
  		private int[] bag;
  		private int N;
  		private int count;
  
  		public RandomBox(int capacity) {
  			bag = new int[capacity];
  			N = capacity;
  			count = 0;
  		}
  
  		private int rand(int max) {
  			return (int) (Math.random() * max) + 1;
  		}
  
  		public void add(int num) {
  			count++;
  			if (count <= N) {
  				bag[count - 1] = num;
  			} else {
  				if (rand(count) <= N) {
  					bag[rand(N) - 1] = num;
  				}
  			}
  		}
  
  		public int[] choices() {
  			int[] ans = new int[N];
  			for (int i = 0; i < N; i++) {
  				ans[i] = bag[i];
  			}
  			return ans;
  		}
  
  	}
  
  	// 请等概率返回1~i中的一个数字
  	public static int random(int i) {
  		return (int) (Math.random() * i) + 1;
  	}
  
  	public static void main(String[] args) {
  		System.out.println("hello");
  		int test = 10000;
  		int ballNum = 17;
  		int[] count = new int[ballNum + 1];
  		for (int i = 0; i < test; i++) {
  			int[] bag = new int[10];
  			int bagi = 0;
  			for (int num = 1; num <= ballNum; num++) {
  				if (num <= 10) {
  					bag[bagi++] = num;
  				} else { // num > 10
  					if (random(num) <= 10) { // 一定要把num球入袋子
  						bagi = (int) (Math.random() * 10);
  						bag[bagi] = num;
  					}
  				}
  
  			}
  			for (int num : bag) {
  				count[num]++;
  			}
  		}
  		for (int i = 0; i <= ballNum; i++) {
  			System.out.println(count[i]);
  		}
  
  		System.out.println("hello");
  		int all = 100;
  		int choose = 10;
  		int testTimes = 50000;
  		int[] counts = new int[all + 1];
  		for (int i = 0; i < testTimes; i++) {
  			RandomBox box = new RandomBox(choose);
  			for (int num = 1; num <= all; num++) {
  				box.add(num);
  			}
  			int[] ans = box.choices();
  			for (int j = 0; j < ans.length; j++) {
  				counts[ans[j]]++;
  			}
  		}
  
  		for (int i = 0; i < counts.length; i++) {
  			System.out.println(i + " times : " + counts[i]);
  		}
  
  	}
  }
  ```

  

### class30

#### morrisTraversal

- 链接：暂无

- 内容：

  > mirrors遍历二叉树

- 思路：

  > 1、当前cur无左子树，cur = cur.right
  >
  > 2、当前cur有左子树，找到cur左子树的最右节点mostRight
  >
  > ​	1、若mostRight.right == null,令mostRight.right = cur,cur=cur.left
  >
  > ​	2、若mostRight.right != null,令cur=cur.right,mostRight=null

- 代码：

  ```java
  	public static void morris(Node head) {
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
  			cur = cur.right;
  		}
  	}
  ```

##### morrisPre

- 链接：暂无

- 内容：morris实现前序遍历

- 思路：

  > 第一次出现则打印

- 代码：

  ```java
  public static void morrisPre(Node head) {
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
  					System.out.print(cur.value + " ");
  					mostRight.right = cur;
  					cur = cur.left;
  					continue;
  				} else {
  					mostRight.right = null;
  				}
  			} else {
  				System.out.print(cur.value + " ");
  			}
  			cur = cur.right;
  		}
  		System.out.println();
  	}
  ```

  

##### morrisIn

- 链接：暂无

- 内容：morris实现中序遍历

- 思路：

  > 无左子树或第二次返回时就打印

- 代码：

  ```java
  public static void morrisIn(Node head) {
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
  	}
  ```

  

##### morrisPos

- 链接：暂无

- 内容：morris实现后序遍历

- 思路：

  > 第二次时，将其左子树节点到最右节点的数据逆序打印
  >
  > 再逆序打印根节点到最右节点的数据

- 代码：

  ```java
  public static void morrisPos(Node head) {
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
  	}
  ```

  

##### isBST

- 链接：https://leetcode.cn/problems/validate-binary-search-tree/description/

- 内容：

  > 给定一个节点，判断其是否为二叉搜索树

- 思路：

  > morris遍历，将前一个数据记录下来，判断
  >
  > 注：要将所有的节点的指定全部复原才能返回

- 代码：

  ```java
      public static boolean isValidBST(Node head) {
          if(head == null) return true;
          Node cur = head,mostRight = null,pre = null;
          boolean ans = true;
          while (cur != null) {
              mostRight = cur.left;
              if(mostRight != null){
                  while (mostRight.right != null && mostRight.right != cur){
                      mostRight = mostRight.right;
                  }
                  if(mostRight.right == null){
                      mostRight.right = cur;
                      cur = cur.left;
                      continue;
                  }else{
                      mostRight.right = null;
                  }
              }
              if(pre != null && pre.value >= cur.value){
                  ans = false;
              }
              pre = cur;
              cur = cur.right;
          }
          return ans;
      }
  ```

  

#### minDepth

- 链接：https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/

- 内容：

  > 求根节点到叶节点的最小深度

- 思路：

  > 思路一：二叉树的递归套路
  >
  > 思路二：morris遍历
  >
  > ​	计算level与mostRightSize，当为叶节点时进行结算和level的修正
  >
  > ​	最后计算根到最右节点的这一条边的长度
  >
  > ​	汇总，得到最小长度

- 代码：

  ```java
  public static int minDepth1(TreeNode head) {
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
      }
  
      // 下面的方法是morris遍历的解
      public static int minDepth2(TreeNode head) {
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
                      if (mostRight.left == null) { // 叶子节点
                          minHeight = Math.min(minHeight, curLevel);
                      }
                      curLevel -= rightBoardSize; // 重复计算的数据
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
      }
  ```

  

### class31

#### segmentTree

- 链接：暂无

- 内容：

  > 在指定范围内的添加，更新，查找的时间复杂度都为logn级别

- 思路：

  > 使用线段树
  >
  > 流程：
  >
  > ​	创建：数组下标0不使用，直接使用build(1,N,1)进行递归创建，更新sum,lazy,update,change数组
  >
  > ​	添加：
  >
  > ​		1、若此任务包含当前的范围，sum与lazy信息数据更改
  >
  > ​		2、若此任务不包含当前的范围，将当前范围内的数据更新与lazy信息先下放一层
  >
  > ​		3、将任务分解为下一层的此任务的添加
  >
  > ​		4、将下面的添加后的数据往上更新sum数组
  >
  > ​	更新：
  >
  > ​		1、若此任务包含当前的范围，sum与lazy信息数据更改并进行数据更新
  >
  > ​		2、若此任务不包含当前的范围，将当前范围内的数据更新与lazy信息先下放一层
  >
  > ​		3、将任务分解为下一层的此任务的更新
  >
  > ​		4、将下面的添加后的数据往上更新sum数组
  >
  > ​	查询：
  >
  > ​		1、若此任务包含当前的范围，返回sum的信息
  >
  > ​		2、若此任务不包含当前的范围，将当前范围内的数据更新与lazy信息先下放一层
  >
  > ​		3、将任务分解为下一层的此任务的查询
  >
  > ​		4、将下面的查询后的数据往上更新sum数组

- 代码：

  ```java
      public static class SegmentTree{
          // arr[] 为原序列的信息从0开始，但在arr里是从1开始的
          // sum[] 模拟线段树维护区间的和
          // lazy[] 为累加和懒惰标记
          // change[] 为更新的值
          // update[] 为更新懒惰标记
          private int MAX;
          private int[] arr;
          private int[] sum;
          private int[] lazy;
          private int[] change;
          private boolean[] update;
  
          public SegmentTree(int[] origin){
              MAX = origin.length + 1;
              arr = new int[MAX]; // arr[0] 不使用
              for (int i = 1; i < MAX; i++) {
                  arr[i] = origin[i-1];
              }
              sum= new int[MAX << 2]; // 用来支持脑补概念中，某一个范围的累加和信息
              lazy = new int[MAX << 2];
              change = new int[MAX << 2];
              update = new boolean[MAX << 2];
          }
          public void pushUp(int rt){
              sum[rt] = sum[rt << 1] + sum[rt << 1 | 1];
          }
          // 之前的，所有懒增加，和懒更新，从父范围，发给左右两个子范围
          // 分发策略是什么
          // ln表示左子树元素结点个数，rn表示右子树结点个数
          private void pushDown(int rt, int ln, int rn) {
              if(update[rt]){
                  update[rt << 1] = true;
                  update[rt << 1 | 1] = true;
                  change[rt << 1] = change[rt];
                  change[rt << 1 | 1] = change[rt];
                  lazy[rt << 1] = 0;
                  lazy[rt << 1 | 1] = 0;
                  sum[rt << 1] = change[rt] * ln;
                  sum[rt << 1 | 1] = change[rt] * rn;
                  update[rt] = false;
              }
              if(lazy[rt] != 0){
                  lazy[rt << 1] += lazy[rt];
                  sum[rt << 1] += lazy[rt] * ln;
                  lazy[rt << 1 | 1] += lazy[rt];
                  sum[rt << 1 | 1] += lazy[rt] * rn;
                  lazy[rt] = 0;
              }
          }
          // 在初始化阶段，先把sum数组，填好
          // 在arr[l~r]范围上，去build，1~N，
          // rt : 这个范围在sum中的下标
          public void build(int l,int r,int rt){
              if(l == r){
                  sum[rt] = arr[l];
                  return;
              }
              int mid = (l+r)>>1;
              build(l,mid,rt<<1);
              build(mid+1,r,rt<<1|1);
              pushUp(rt);
          }
  
          // L~R  所有的值变成C
          // l~r  rt
          public void update(int L,int R,int C,int l,int r,int rt){
              if(L <= l && r <= R){
                  update[rt] = true;
                  change[rt] = C;
                  sum[rt] = C * (r-l+1);
                  lazy[rt] = 0;
                  return;
              }
              // 当前任务躲不掉，无法懒更新，要往下发
              int mid = (r + l) >> 1;
              pushDown(rt,mid - l + 1, r - mid);
              if(L <= mid){
                  update(L,R,C,l,mid,rt << 1);
              }
              if(R > mid){
                  update(L,R,C,mid+1,r,rt << 1 | 1);
              }
              pushUp(rt);
          }
          // L~R, C 任务！
          // rt，l~r
          public void add(int L,int R,int C,int l,int r,int rt){
              // 任务如果把此时的范围全包了！
              if (L <= l && r <= R) {
                  sum[rt] += C * (r - l + 1);
                  lazy[rt] += C;
                  return;
              }
              // 任务没有把你全包！
              // l  r  mid = (l+r)/2
              int mid = (l + r) >> 1;
              pushDown(rt,mid - l + 1,r - mid);
              // L~R
              if(L <= mid){
                  add(L,R,C,l,mid,rt << 1);
              }
              if(R > mid){
                  add(L,R,C,mid+1,R,rt << 1 | 1);
              }
              pushUp(rt);
          }
  
          // 1~6 累加和是多少？ 1~8 rt
          public long query(int L, int R, int l, int r, int rt) {
              if(L <= l && r <= R){
                  return sum[rt];
              }
              int mid = (l+r) >> 1;
              pushDown(rt,mid - l + 1,r - mid);
              long ans = 0;
              if(L <= mid){
                  ans += query(L,R,l,mid,rt << 1);
              }
              if(R > mid){
                  ans += query(L,R,mid+1,r,rt<<1 | 1);
              }
              return ans;
          }
      }
  ```

#### fallingSquares

- 链接：暂无

- 内容：

  > 给一个二维数组，第一维i是第几个掉下的正方形，第二维的下标0表示沿哪个坐标下去，下标1表示此正方形的连长，返回一个长度为第一维长度的list集合，表示在各个位置的最大高度
  >
  > 注: 【0，1】的坐标轴是前闭后开的，可以转化为【0，【0】+【1】-1】的坐标轴

- 思路：

  >使用线段树，将sum改为max,无需要更新操作，只要指定范围内的添加和查询操作

- 代码：

  ```java
  public static class SegmentTree {
  		private int[] max;
  		private int[] change;
  		private boolean[] update;
  
  		public SegmentTree(int size) {
  			int N = size + 1;
  			max = new int[N << 2];
  
  			change = new int[N << 2];
  			update = new boolean[N << 2];
  		}
  
  		private void pushUp(int rt) {
  			max[rt] = Math.max(max[rt << 1], max[rt << 1 | 1]);
  		}
  
  		// ln表示左子树元素结点个数，rn表示右子树结点个数
  		private void pushDown(int rt, int ln, int rn) {
  			if (update[rt]) {
  				update[rt << 1] = true;
  				update[rt << 1 | 1] = true;
  				change[rt << 1] = change[rt];
  				change[rt << 1 | 1] = change[rt];
  				max[rt << 1] = change[rt];
  				max[rt << 1 | 1] = change[rt];
  				update[rt] = false;
  			}
  		}
  
  		public void update(int L, int R, int C, int l, int r, int rt) {
  			if (L <= l && r <= R) {
  				update[rt] = true;
  				change[rt] = C;
  				max[rt] = C;
  				return;
  			}
  			int mid = (l + r) >> 1;
  			pushDown(rt, mid - l + 1, r - mid);
  			if (L <= mid) {
  				update(L, R, C, l, mid, rt << 1);
  			}
  			if (R > mid) {
  				update(L, R, C, mid + 1, r, rt << 1 | 1);
  			}
  			pushUp(rt);
  		}
  
  		public int query(int L, int R, int l, int r, int rt) {
  			if (L <= l && r <= R) {
  				return max[rt];
  			}
  			int mid = (l + r) >> 1;
  			pushDown(rt, mid - l + 1, r - mid);
  			int left = 0;
  			int right = 0;
  			if (L <= mid) {
  				left = query(L, R, l, mid, rt << 1);
  			}
  			if (R > mid) {
  				right = query(L, R, mid + 1, r, rt << 1 | 1);
  			}
  			return Math.max(left, right);
  		}
  
  	}
  
  	public HashMap<Integer, Integer> index(int[][] positions) {
  		TreeSet<Integer> pos = new TreeSet<>();
  		for (int[] arr : positions) {
  			pos.add(arr[0]);
  			pos.add(arr[0] + arr[1] - 1);
  		}
  		HashMap<Integer, Integer> map = new HashMap<>();
  		int count = 0;
  		for (Integer index : pos) {
  			map.put(index, ++count);
  		}
  		return map;
  	}
  
  	public List<Integer> fallingSquares(int[][] positions) {
  		HashMap<Integer, Integer> map = index(positions);
  		int N = map.size();
  		SegmentTree segmentTree = new SegmentTree(N);
  		int max = 0;
  		List<Integer> res = new ArrayList<>();
  		// 每落一个正方形，收集一下，所有东西组成的图像，最高高度是什么
  		for (int[] arr : positions) {
  			int L = map.get(arr[0]);
  			int R = map.get(arr[0] + arr[1] - 1);
  			int height = segmentTree.query(L, R, 1, N, 1) + arr[1];
  			max = Math.max(max, height);
  			res.add(max);
  			segmentTree.update(L, R, height, 1, N, 1);
  		}
  		return res;
  	}
  ```

  

### class32

#### indexTree

- 链接：暂无

- 内容：

  > 求单点添加（更新）与范围和

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

  ```java
  // 下标从1开始！
  	public static class IndexTree {
  
  		private int[] tree;
  		private int N;
  
  		// 0位置弃而不用！
  		public IndexTree(int size) {
  			N = size;
  			tree = new int[N + 1];
  		}
  
  		// 1~index 累加和是多少？
  		public int sum(int index) {
  			int ret = 0;
  			while (index > 0) {
  				ret += tree[index];
  				index -= index & -index;
  			}
  			return ret;
  		}
  
  		// index & -index : 提取出index最右侧的1出来
  		// index :           0011001000
  		// index & -index :  0000001000
  		public void add(int index, int d) {
  			while (index <= N) {
  				tree[index] += d;
  				index += index & -index;
  			}
  		}
  	}
  
  ```

#### indexTree2D

- 链接：https://leetcode.com/problems/range-sum-query-2d-mutable

- 内容：

  > 实现一个二维的indexTree,能够更新，求和，及范围和

- 思路：

  > 思路同一维实现，不过加了一个维度 数量i*数量j

- 代码：

  ```java
  public class Code02_IndexTree2D {
      private int[][] tree, nums;
      private int N, M;
  
      public Code02_IndexTree2D(int[][] matrix) {
          N = matrix.length;
          M = matrix[0].length;
          tree = new int[N + 1][M + 1];
          nums = new int[N][M];
          for (int i = 0; i < N; i++) {
              for (int j = 0; j < M; j++) {
                  update(i,j,matrix[i][j]);
              }
          }
      }
  
      private int sum(int row, int col) {
          int sum = 0;
          for (int i = row + 1; i <= N; i += i & -i) {
              for (int j = col + 1; j <= M; j += j & -j) {
                  sum += tree[i][j];
              }
          }
          return sum;
      }
  
      public void update(int row, int col, int val) {
          if (N == 0 || M == 0) return;
          int add = val - nums[row][col];
          nums[row][col] = val;
          for (int i = row + 1; i <= N; i += i & -i) {
              for (int j = col + 1; j <= M; j += j & -j) {
                  tree[i][j] += add;
              }
          }
      }
  
      public int sumRegion(int row1, int col1, int row2, int col2) {
          if(N == 0 || M == 0)
              return 0;
          return sum(row2,col2) - sum(row1-1,col2) - sum(row2,col1-1) + sum(row1-1,col1-1);
      }
  }
  ```

  

#### AC-前置(前缀树)

- 链接：暂无

- 内容

  > AC自动机，

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

  ![](img/a2020_32_ac.png)

- 代码：

  ```java
  	public static class Node {
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
  					Node next = new Node();
  					cur.nexts[index] = next;
  				}
  				cur = cur.nexts[index];
  			}
  			cur.end++;
  		}
  
  		public void build() {
  			Queue<Node> queue = new LinkedList<>();
  			queue.add(root);
  			Node cur = null;
  			Node cfail = null;
  			while (!queue.isEmpty()) {
  				cur = queue.poll(); // 父
  				for (int i = 0; i < 26; i++) { // 下级所有的路
  					if (cur.nexts[i] != null) { // 该路下有子节点
  						cur.nexts[i].fail = root; // 初始时先设置一个值
  						cfail = cur.fail;
  						while (cfail != null) { // cur不是头节点
  							if (cfail.nexts[i] != null) {
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
  			char[] str = content.toCharArray();
  			Node cur = root;
  			Node follow = null;
  			int index = 0;
  			int ans = 0;
  			for (int i = 0; i < str.length; i++) {
  				index = str[i] - 'a';
  				while (cur.nexts[index] == null && cur != root) {
  					cur = cur.fail;
  				}
  				cur = cur.nexts[index] != null ? cur.nexts[index] : root;
  				follow = cur;
  				while (follow != root) {
  					if (follow.end == -1) {
  						break;
  					}
  					{ // 不同的需求，在这一段{ }之间修改
  						ans += follow.end;
  						follow.end = -1;
  					} // 不同的需求，在这一段{ }之间修改
  					follow = follow.fail;
  				}
  			}
  			return ans;
  		}
      }
  ```

  

#### AC2

- 链接：

- 内容：

  > 记录在一个文章中出现了哪些违规词，假设已知道所有的违规词

- 思路：

  > 使用ac自动机，添加所有的节点，并将所有的违规节点都标记一下
  >
  > 对文章遍历，如果进入，则按层遍历所有节点的fail，直到空，中途有违规节点添加
  >
  > 直接文章遍历结束

- 代码：

  ```java
  // 前缀树的节点
  	public static class Node {
  		// 如果一个node，end为空，不是结尾
  		// 如果end不为空，表示这个点是某个字符串的结尾，end的值就是这个字符串
  		public String end;
  		// 只有在上面的end变量不为空的时候，endUse才有意义
  		// 表示，这个字符串之前有没有加入过答案
  		public boolean endUse;
  		public Node fail;
  		public Node[] nexts;
  
  		public Node() {
  			endUse = false;
  			end = null;
  			fail = null;
  			nexts = new Node[26];
  		}
  	}
  
  	public static class ACAutomation {
  		private Node root;
  
  		public ACAutomation() {
  			root = new Node();
  		}
  
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
  			Queue<Node> queue = new LinkedList<>();
  			queue.add(root);
  			Node cur = null;
  			Node cfail = null;
  			while (!queue.isEmpty()) {
  				// 某个父亲，cur
  				cur = queue.poll();
  				for (int i = 0; i < 26; i++) { // 所有的路
  					// cur -> 父亲  i号儿子，必须把i号儿子的fail指针设置好！
  					if (cur.nexts[i] != null) { // 如果真的有i号儿子
  						cur.nexts[i].fail = root;
  						cfail = cur.fail;
  						while (cfail != null) {
  							if (cfail.nexts[i] != null) {
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
  
  		// 大文章：content
  		public List<String> containWords(String content) {
  			char[] str = content.toCharArray();
  			Node cur = root;
  			Node follow = null;
  			int index = 0;
  			List<String> ans = new ArrayList<>();
  			for (int i = 0; i < str.length; i++) {
  				index = str[i] - 'a'; // 路
  				// 如果当前字符在这条路上没配出来，就随着fail方向走向下条路径
  				while (cur.nexts[index] == null && cur != root) {
  					cur = cur.fail;
  				}
  				// 1) 现在来到的路径，是可以继续匹配的
  				// 2) 现在来到的节点，就是前缀树的根节点
  				cur = cur.nexts[index] != null ? cur.nexts[index] : root;
  				follow = cur;
  				while (follow != root) {
  					if (follow.endUse) {
  						break;
  					}
  					// 不同的需求，在这一段之间修改
  					if (follow.end != null) {
  						ans.add(follow.end);
  						follow.endUse = true;
  					}
  					// 不同的需求，在这一段之间修改
  					follow = follow.fail;
  				}
  			}
  			return ans;
  		}
  
  	}
  ```

  

### class33

#### hash

- hash函数是一个把长度大的入参数据转化为长度小的出参数据的一个函数方法

- 具有两个性质，**离散性与均匀性**

- 内容：

  > hash的底层是一个数组+链表（树结构）实现的，当查询速度慢了（或者其中一个数组的数据太长，超过范围了），会进行扩容操作，将数组扩充，并使用新的hash函数将原数据进行填充。
  >
  > 例如，当数据达到 2 4 8 16 ... log_2n时会进行数据扩充，扩充的代价则是一个等比数列
  > $$
  > W = a_0*(1-r^n)/(1-r) = 2*{(1-2^k)}/{(1-2)}
  > $$
  > k = log_2n
  > $$
  > W = 2*(1-2^{log_{2}n})/(1-2) = 2*(1-n)/(1-2) = 2*(n-1)
  > $$
  > 因为此时扩充的代价是O(N)，不同的扩充策略会影响常数时间，不会影响复杂度的级别
  >
  > 查询或添加了N个，所以查询的时间复杂度平均是O(N)/N = O(1)

#### 布隆过滤器

- 特点

  - 利用哈希函数的性质
  - 每一条数据提取特征
  - 加入描黑库

- 作用

  - 对指定的数据添加黑名单
  - 有误判率（不可避免）(只要是添加过的黑名单，不会误报，只会有一定概率把正确的误报成黑名单)

- 重要公式：

  - **假设数据量为n,预期失误率为p(布隆过滤器大小和样本的大小无关)**

  - 根据n和p,算出布隆过滤器需要的bit位，向上取整记为m

  - 根据m和n,算出布隆过滤器需要多少个哈希函数，向上取整，记为k

  - 根据修正公式，算出真实的失误率p_true

    ![](img/a2020_32_bloom.png)

  - 根据两个不同的hash函数，可以使用2*h1+h2,3h1+h2等构造出多个不相同的hash函数

- 应用

  - hdfs（HDFS（Hadoop Distributed File System）是Hadoop生态系统中的分布式文件系统，用于存储和处理大规模数据集），查找文件
  - url判断（黑名单）

#### 一致性哈希

- 分布式存储结构常见的结构 
  - 哈希域变环设计
    - 成环，然后加节点，顺时针的那部分交由另一个节点管理
  - 虚拟节点技术
    - 每个物理空间set管理一个环上的n个节点
    - 添加一个物理空间set,之前的物理空间set管理的节点分给新的set,使所有的set数据量几乎相等

### class34

#### 资源限制类型技巧汇总

- 1)布隆过滤器用于集合的建立与查询，并可以节省大量空间
- 2)一致性哈希解决数据服务器的负载管理问题
- 3)利用并查集结构做岛问题的并行计算
- 4)哈希函数可以把数据按照种类均匀分流
- 5)位图解决某一范围上数字的出现情况，并可以节省大量空间
- 6)利用分段统计思想、并进一步节省大量空间
- 7)利用堆、外排序来做多个处理单元的结果合并

#### 题目一
- 内容：

  > 32位无符号整数的范围是0~4,294,967,295,现在有一个正好包含40亿个无符号整数的文件，可以使用最多1GB的内存，怎么找到出现次数最多的数?

- 思路：

  **哈希函数可以把数据按照种类均匀分流**

  > 分流：一个hash数据占用8字节的数据内存，key与value均为4字节。
  >
  > 那么1GB的内存最多只能有1GB/8B=1G=125,000,000（条）
  >
  > 最多只有1亿多条数据，但是hash表内部还有索引等占据的内存空间，这里直接保守估计只能存1千万条数据。
  >
  > 总共只有40亿个无符号整数，那可以使用这1千万条数据内存空间进行分流。
  >
  > 因为**hash函数的离散性与均匀性**，我们假设使用了一个hash函数对这源40亿个无符号整数进行数据处理，%400后的结果表示进入哪个桶中，（桶是只有一个的，但我们可以先找出所有在0中的桶后进行一些处理后记录其中出现次数最多的数，释放资源后，再把所有要进1中的数据同样处理...），**这样每个桶中估计刚好有1千万条数据**。
  >
  > 因为**同一个无符号整数使用同一个哈希函数得出的结果是一样的**，不会因这个整数所在的位置的不同。
  >
  > **从桶0记录出现最大的值及其数量，释放桶0资源，记录桶1与之前最大的值及其数量比较，直到结束。（桶0和桶1...是同一个内存空间，不过是在不同过程的不同称呼而已**）

- 进阶：**当一个哈希函数无法满足时，可以使用两个哈希函数对数据进行依次处理，过程同一个哈希函数。**

#### 题目二
- 内容：

  > 32位无符号整数的范围是0~4,294,967,295,现在有一个正好包含40亿个无符号整数的文件，所以在整个范围中必然存在没出现过的数。可以使用最多1GB的内存，怎么找到所有未出现过的数?

- 思路：

  **位图解决某一范围上数字的出现情况，并可以节省大量空间**

  > 我们可以联想一下布隆过滤器，它是把一个url(数字)映射到bit位上(一位或多位)，如果这些位上同时存在，则表明数据存在。
  >
  > 我们可以使用同样的方法，但不使用哈希函数，因为它有误判率
  >
  > 我们可以申请长度为4,294,967,296/32=134,217,728长度(向上取整)的int数组，这个长度为134,217,728，所占空间为536,870,912B空间，1GB所占1,000,000,000B空间，远远小于1GB空间。
  >
  > 我们**对任意一个无符号整数S的处理策略是，先定位S所在的数组下标i,i=S/32,再找到S对应的哪位k,k=S%32,对任意一个S，把arr[i]这个数据的k位，使用1<<(S%32)变成1(原先为0则变，原先为1则不变)**
  >
  > 把所有的数据全过一遍后，对于**位上为0的数据所代表的无符号整数即是没有的，收集所有。**

- 【进阶】

  > 内存限制为3KB，但是只用找到一个没出现过的数即可

- 【进阶】思路

  **利用分段统计思想、并进一步节省大量空间**

  > 3KB = 3000KB ,一个无符号数据占4字节，3000/4=750个
  >
  > 找到小于750的最大的二的次幂，512
  >
  > **0~2^32-1**一共有2^32个数据，可以分512份，每一份有2^(32-9)=2^23个数据
  >
  > arr = int[512] 
  >
  > arr[0]表示0~2^23-1这个范围内的数据的数量，arr[1]表示2^23~2^24-1这个范围内的数量
  >
  > 当有一个arr[i] 的数量不等于2^23时，说明其内至少有一个无符号位数字不存在。
  >
  > 然后在**i * 2^23~(i+1) * 2^23-1**这个范围内继续分512份，找到数量不等于其范围的区间
  >
  > 继续重复上述过程
  >
  > 直到找到为止。

- 【进阶】

  > 内存限制为几个变量，但是只用找到一个没出现过的数即可

- 【进阶】思路

  > 二分
  >
  > 找到0~2^31-1,2^31~2^32-1这两个区间的数量，然后查找不符合的那个区间
  >
  > 以这个区间再继续二分
  >
  > 直到找到了要找的不存在的值。

#### 题目三
- 内容

  > 有一个包含100亿个URL的大文件，假设每个URL占用64B，请找出其中所有重复的URL

- 思路

  > 思路一：布隆过滤器，但有失误率
  >
  > 思路二：哈希分流
  >
  > 把大文件通过哈希分为小文件，若需要再把小文件分为小小文件...
  >
  > 若有重复的肯定会进入同一个小....文件中,即可找到所有重复的url

- 【进阶】

  > 某搜索公司一天的用户搜索词汇是海量的(百亿数据量)，请设计一种求出每天热门Top100词汇的可行办法

- 【进阶】思路

  > 哈希分流+100容量的小根堆

#### 题目四
- 内容

  > 32位无符号整数的范围是0~4294967295,现在有40亿个无符号整数,可以使用最多1GB的内存，找出所有出现了两次的数。

- 思路

  > 使用位图
  >
  > 每两位表示一个数据出现的次数，00表示未出现 ，01表示出现1次，10表示出现2次，11表示出现3次及以上
  >
  > 需要的空间2^32个数，每个数占2位，共占据2^34bit，一共要占据2^31B空间
  >
  > 1GB = 1,000,000,000B，2^31B = 1,073,741,824 空间不够
  >
  > 先分段，再计算
  >
  > 第一段计算所有0~2^31-1的数据的出现两次重复的数
  >
  > 第二段计算所有2^31~2^32-1的数据的出现两次重复的数

#### 题目五
- 内容

  > 32位无符号整数的范围是0~4294967295，现在有40亿个无符号整数可以使用最多10MB的内存，怎么找到这40亿个整数的中位数?

- 思路

  > 10MB, 10MB/4B = 10^7/4 = 2.5 * 10^7 = 25,000,000
  >
  > 保守估计能申请134217728(2^27)长度的int数组
  >
  > 计算每个arr[i]的值，则能定位到哪个arr[i]包含中位数
  >
  > 继续在arr[i]所代表的范围中进行求第几个数
  >
  > 再进行分段
  >
  > 直到结束。

- 【进阶】

  > 只有3KB

- 【进阶】思路

  > 同上，不过要多进行几次分段处理

#### 题目六
- 内容

  > 32位无符号整数的范围是0~4294967295,有一个10G大小的文件，每一行都装着这种类型的数字，整个文件是无序的，给你5G的内存空间，请你输出一个10G大小的文件，就是原文件所有数字排序的结果

- 思路

  > 利用堆，使用5G的内存空间的堆，记录这个内存下的小的值及其次数，然后写入文件中。
  >
  > 再利用堆，把除了上一次的最大值以下的值添加入堆，然后写入文件中。
  >
  > 直到所有的数据都完成了排序并写入了文件中。

### class35

#### AVLTree

- 链接：暂无

- 内容：

  > avl树的创建，添加节点与删除节点
  >
  > 

- 思路：

  > avl树的创建，初始化
  >
  > 一个avl树在初始是，头是null,且size=0
  >
  > avl树的节点内包含自己的key与value值，left与right指针，还有自己的高度（叶子节点为1）

  - 添加节点

    > 添加节点与BST是一样的，不过要加一个补丁，该补丁是对avl树的补充
    >
    > 保证avl树任一节点的左右子树之差不超过1
    >
    > 且在添加节点的位置直到根节点都要对高度进行处理

    ```java
    private AVLNode<K, V> add(AVLNode<K, V> cur, K key, V value) {
    			if (cur == null) {
    				return new AVLNode<K, V>(key, value);
    			} else {
    				if (key.compareTo(cur.k) < 0) { // 要放在左边
    					cur.l = add(cur.l, key, value);
    				} else {
    					cur.r = add(cur.r, key, value); // 要放在右边
    				}
    				cur.h = Math.max(cur.l != null ? cur.l.h : 0, cur.r != null ? cur.r.h : 0) + 1;
    				return maintain(cur);
    			}
    		}
    ```

  - 删除节点

    > 删除节点同BST,存在四种情况，每一种情况都要对沿途树进行处理
    >
    > 1、删除节点左右子树均不存在，直接删除
    >
    > 2、删除节点左子树不存在，用右子树代替删除节点
    >
    > 3、删除节点右子树不存在，用左子树代替删除节点
    >
    > 4、删除节点左右子树均存在，使用删除节点的前驱或后继替代

    ```java
    	private AVLNode<K, V> delete(AVLNode<K, V> cur, K key) {
    			if (key.compareTo(cur.k) > 0) {
    				cur.r = delete(cur.r, key);
    			} else if (key.compareTo(cur.k) < 0) {
    				cur.l = delete(cur.l, key);
    			} else {
    				if (cur.l == null && cur.r == null) {
    					cur = null;
    				} else if (cur.l == null && cur.r != null) {
    					cur = cur.r;
    				} else if (cur.l != null && cur.r == null) {
    					cur = cur.l;
    				} else {
    					AVLNode<K, V> des = cur.r;
    					while (des.l != null) {
    						des = des.l;
    					}
    					cur.r = delete(cur.r, des.k);
    					des.l = cur.l;
    					des.r = cur.r;
    					cur = des;
    				}
    			}
    			if (cur != null) {
    				cur.h = Math.max(cur.l != null ? cur.l.h : 0, cur.r != null ? cur.r.h : 0) + 1;
    			}
    			return maintain(cur);
    		}
    ```

- 代码：

  - 左旋与右旋

    ```java
    // LL
    private AVLNode<K, V> rightRotate(AVLNode<K, V> cur) {
    			AVLNode<K, V> left = cur.l;
    			cur.l = left.r;
    			left.r = cur;
    			cur.h = Math.max((cur.l != null ? cur.l.h : 0), (cur.r != null ? cur.r.h : 0)) + 1;
    			left.h = Math.max((left.l != null ? left.l.h : 0), (left.r != null ? left.r.h : 0)) + 1;
    			return left;
    		}
    // RR
    		private AVLNode<K, V> leftRotate(AVLNode<K, V> cur) {
    			AVLNode<K, V> right = cur.r;
    			cur.r = right.l;
    			right.l = cur;
    			cur.h = Math.max((cur.l != null ? cur.l.h : 0), (cur.r != null ? cur.r.h : 0)) + 1;
    			right.h = Math.max((right.l != null ? right.l.h : 0), (right.r != null ? right.r.h : 0)) + 1;
    			return right;
    		}
    ```

  - maintain补丁

    ```java
    	private AVLNode<K, V> maintain(AVLNode<K, V> cur) {
    			if (cur == null) {
    				return null;
    			}
    			int leftHeight = cur.l != null ? cur.l.h : 0;
    			int rightHeight = cur.r != null ? cur.r.h : 0;
    			if (Math.abs(leftHeight - rightHeight) > 1) {
    				if (leftHeight > rightHeight) {
    					int leftLeftHeight = cur.l != null && cur.l.l != null ? cur.l.l.h : 0;
    					int leftRightHeight = cur.l != null && cur.l.r != null ? cur.l.r.h : 0;
    					if (leftLeftHeight >= leftRightHeight) {
                            // LL与LR同时出现（删除节点时），一定要使用LL
                            // LL
    						cur = rightRotate(cur);
    					} else {
                            // LR
    						cur.l = leftRotate(cur.l);
    						cur = rightRotate(cur);
    					}
    				} else {
    					int rightLeftHeight = cur.r != null && cur.r.l != null ? cur.r.l.h : 0;
    					int rightRightHeight = cur.r != null && cur.r.r != null ? cur.r.r.h : 0;
    					if (rightRightHeight >= rightLeftHeight) {
                            // RR
    						cur = leftRotate(cur);
    					} else {
                            // RL 
    						cur.r = rightRotate(cur.r);
    						cur = leftRotate(cur);
    					}
    				}
    			}
    			return cur;
    		}
    ```

- 相关api

  ```java
  	private AVLNode<K, V> findLastIndex(K key) {
  			AVLNode<K, V> pre = root;
  			AVLNode<K, V> cur = root;
  			while (cur != null) {
  				pre = cur;
  				if (key.compareTo(cur.k) == 0) {
  					break;
  				} else if (key.compareTo(cur.k) < 0) {
  					cur = cur.l;
  				} else {
  					cur = cur.r;
  				}
  			}
  			return pre;
  		}
  
  	private AVLNode<K, V> findLastNoSmallIndex(K key) {
  			AVLNode<K, V> ans = null;
  			AVLNode<K, V> cur = root;
  			while (cur != null) {
  				if (key.compareTo(cur.k) == 0) {
  					ans = cur;
  					break;
  				} else if (key.compareTo(cur.k) < 0) {
  					ans = cur;
  					cur = cur.l;
  				} else {
  					cur = cur.r;
  				}
  			}
  			return ans;
  		}
  	private AVLNode<K, V> findLastNoBigIndex(K key) {
  			AVLNode<K, V> ans = null;
  			AVLNode<K, V> cur = root;
  			while (cur != null) {
  				if (key.compareTo(cur.k) == 0) {
  					ans = cur;
  					break;
  				} else if (key.compareTo(cur.k) < 0) {
  					cur = cur.l;
  				} else {
  					ans = cur;
  					cur = cur.r;
  				}
  			}
  			return ans;
  		}
  ```

  

### class36

#### sizeBalancedTree

- 链接：暂无

- 内容：

  > sb树，任何的子树的节点个数不能超过其叔叔为根的子树节点个数

- 思路：

  > 同avl树，出现ll,rr,lr,rl时，要进行旋转操作
  >
  > 但这里是递归调用，而不是avl的有限几个看看是否平衡
  >
  > 且，sb树在删除时不会进行补丁操作

- 代码：

  ```java
  public static class SizeBalancedTreeMap<K extends Comparable<K>, V> {
  		private SBTNode<K, V> root;
  
  		private SBTNode<K, V> rightRotate(SBTNode<K, V> cur) {
  			SBTNode<K, V> leftNode = cur.l;
  			cur.l = leftNode.r;
  			leftNode.r = cur;
  			leftNode.size = cur.size;
  			cur.size = (cur.l != null ? cur.l.size : 0) + (cur.r != null ? cur.r.size : 0) + 1;
  			return leftNode;
  		}
  
  		private SBTNode<K, V> leftRotate(SBTNode<K, V> cur) {
  			SBTNode<K, V> rightNode = cur.r;
  			cur.r = rightNode.l;
  			rightNode.l = cur;
  			rightNode.size = cur.size;
  			cur.size = (cur.l != null ? cur.l.size : 0) + (cur.r != null ? cur.r.size : 0) + 1;
  			return rightNode;
  		}
  
  		private SBTNode<K, V> maintain(SBTNode<K, V> cur) {
  			if (cur == null) {
  				return null;
  			}
  			int leftSize = cur.l != null ? cur.l.size : 0;
  			int leftLeftSize = cur.l != null && cur.l.l != null ? cur.l.l.size : 0;
  			int leftRightSize = cur.l != null && cur.l.r != null ? cur.l.r.size : 0;
  			int rightSize = cur.r != null ? cur.r.size : 0;
  			int rightLeftSize = cur.r != null && cur.r.l != null ? cur.r.l.size : 0;
  			int rightRightSize = cur.r != null && cur.r.r != null ? cur.r.r.size : 0;
  			if (leftLeftSize > rightSize) {
  				cur = rightRotate(cur);
  				cur.r = maintain(cur.r);
  				cur = maintain(cur);
  			} else if (leftRightSize > rightSize) {
  				cur.l = leftRotate(cur.l);
  				cur = rightRotate(cur);
  				cur.l = maintain(cur.l);
  				cur.r = maintain(cur.r);
  				cur = maintain(cur);
  			} else if (rightRightSize > leftSize) {
  				cur = leftRotate(cur);
  				cur.l = maintain(cur.l);
  				cur = maintain(cur);
  			} else if (rightLeftSize > leftSize) {
  				cur.r = rightRotate(cur.r);
  				cur = leftRotate(cur);
  				cur.l = maintain(cur.l);
  				cur.r = maintain(cur.r);
  				cur = maintain(cur);
  			}
  			return cur;
  		}
  		// 现在，以cur为头的树上，新增，加(key, value)这样的记录
  		// 加完之后，会对cur做检查，该调整调整
  		// 返回，调整完之后，整棵树的新头部
  		private SBTNode<K, V> add(SBTNode<K, V> cur, K key, V value) {
  			if (cur == null) {
  				return new SBTNode<K, V>(key, value);
  			} else {
  				cur.size++;
  				if (key.compareTo(cur.key) < 0) {
  					cur.l = add(cur.l, key, value);
  				} else {
  					cur.r = add(cur.r, key, value);
  				}
  				return maintain(cur);
  			}
  		}
  
  		// 在cur这棵树上，删掉key所代表的节点
  		// 返回cur这棵树的新头部
  		private SBTNode<K, V> delete(SBTNode<K, V> cur, K key) {
  			cur.size--;
  			if (key.compareTo(cur.key) > 0) {
  				cur.r = delete(cur.r, key);
  			} else if (key.compareTo(cur.key) < 0) {
  				cur.l = delete(cur.l, key);
  			} else { // 当前要删掉cur
  				if (cur.l == null && cur.r == null) {
  					// free cur memory -> C++
  					cur = null;
  				} else if (cur.l == null && cur.r != null) {
  					// free cur memory -> C++
  					cur = cur.r;
  				} else if (cur.l != null && cur.r == null) {
  					// free cur memory -> C++
  					cur = cur.l;
  				} else { // 有左有右
  					SBTNode<K, V> pre = null;
  					SBTNode<K, V> des = cur.r;
  					des.size--;
  					while (des.l != null) {
  						pre = des;
  						des = des.l;
  						des.size--;
  					}
  					if (pre != null) {
  						pre.l = des.r;
  						des.r = cur.r;
  					}
  					des.l = cur.l;
  					des.size = des.l.size + (des.r == null ? 0 : des.r.size) + 1;
  					// free cur memory -> C++
  					cur = des;
  				}
  			}
  			// cur = maintain(cur);
  			return cur;
  		}
  }
  ```

#### skipList

- 链接：暂无

- 内容：

  > 跳表

- 思路：

  > 跳表的实质是使用概率事件来完成对数据的分级

- 代码：

  ```java
  // 跳表的节点定义
  	public static class SkipListNode<K extends Comparable<K>, V> {
  		public K key;
  		public V val;
  		public ArrayList<SkipListNode<K, V>> nextNodes;
  
  		public SkipListNode(K k, V v) {
  			key = k;
  			val = v;
  			nextNodes = new ArrayList<SkipListNode<K, V>>();
  		}
  
  		// 遍历的时候，如果是往右遍历到的null(next == null), 遍历结束
  		// 头(null), 头节点的null，认为最小
  		// node  -> 头，node(null, "")  node.isKeyLess(!null)  true
  		// node里面的key是否比otherKey小，true，不是false
  		public boolean isKeyLess(K otherKey) {
  			//  otherKey == null -> false 
  			return otherKey != null && (key == null || key.compareTo(otherKey) < 0);
  		}
  
  		public boolean isKeyEqual(K otherKey) {
  			return (key == null && otherKey == null)
  					|| (key != null && otherKey != null && key.compareTo(otherKey) == 0);
  		}
  
  	}
  
  	public static class SkipListMap<K extends Comparable<K>, V> {
  		private static final double PROBABILITY = 0.5; // < 0.5 继续做，>=0.5 停
  		private SkipListNode<K, V> head;
  		private int size;
  		private int maxLevel;
  
  		public SkipListMap() {
  			head = new SkipListNode<K, V>(null, null);
  			head.nextNodes.add(null); // 0
  			size = 0;
  			maxLevel = 0;
  		}
  
  		// 从最高层开始，一路找下去，
  		// 最终，找到第0层的<key的最右的节点
  		private SkipListNode<K, V> mostRightLessNodeInTree(K key) {
  			if (key == null) {
  				return null;
  			}
  			int level = maxLevel;
  			SkipListNode<K, V> cur = head;
  			while (level >= 0) { // 从上层跳下层
  				//  cur  level  -> level-1
  				cur = mostRightLessNodeInLevel(key, cur, level--);
  			}
  			return cur;
  		}
  
  		// 在level层里，如何往右移动
  		// 现在来到的节点是cur，来到了cur的level层，在level层上，找到<key最后一个节点并返回
  		private SkipListNode<K, V> mostRightLessNodeInLevel(K key, 
  				SkipListNode<K, V> cur, 
  				int level) {
  			SkipListNode<K, V> next = cur.nextNodes.get(level);
  			while (next != null && next.isKeyLess(key)) {
  				cur = next;
  				next = cur.nextNodes.get(level);
  			}
  			return cur;
  		}
  
  		public boolean containsKey(K key) {
  			if (key == null) {
  				return false;
  			}
  			SkipListNode<K, V> less = mostRightLessNodeInTree(key);
  			SkipListNode<K, V> next = less.nextNodes.get(0);
  			return next != null && next.isKeyEqual(key);
  		}
  
  		// 新增、改value
  		public void put(K key, V value) {
  			if (key == null) {
  				return;
  			}
  			// 0层上，最右一个，< key 的Node -> >key
  			SkipListNode<K, V> less = mostRightLessNodeInTree(key);
  			SkipListNode<K, V> find = less.nextNodes.get(0);
  			if (find != null && find.isKeyEqual(key)) {
  				find.val = value;
  			} else { // find == null   8   7   9
  				size++;
  				int newNodeLevel = 0;
  				while (Math.random() < PROBABILITY) {
  					newNodeLevel++;
  				}
  				// newNodeLevel
  				while (newNodeLevel > maxLevel) {
  					head.nextNodes.add(null);
  					maxLevel++;
  				}
  				SkipListNode<K, V> newNode = new SkipListNode<K, V>(key, value);
  				for (int i = 0; i <= newNodeLevel; i++) {
  					newNode.nextNodes.add(null);
  				}
  				int level = maxLevel;
  				SkipListNode<K, V> pre = head;
  				while (level >= 0) {
  					// level 层中，找到最右的 < key 的节点
  					pre = mostRightLessNodeInLevel(key, pre, level);
  					if (level <= newNodeLevel) {
  						newNode.nextNodes.set(level, pre.nextNodes.get(level));
  						pre.nextNodes.set(level, newNode);
  					}
  					level--;
  				}
  			}
  		}
  
  		public V get(K key) {
  			if (key == null) {
  				return null;
  			}
  			SkipListNode<K, V> less = mostRightLessNodeInTree(key);
  			SkipListNode<K, V> next = less.nextNodes.get(0);
  			return next != null && next.isKeyEqual(key) ? next.val : null;
  		}
  
  		public void remove(K key) {
  			if (containsKey(key)) {
  				size--;
  				int level = maxLevel;
  				SkipListNode<K, V> pre = head;
  				while (level >= 0) {
  					pre = mostRightLessNodeInLevel(key, pre, level);
  					SkipListNode<K, V> next = pre.nextNodes.get(level);
  					// 1）在这一层中，pre下一个就是key
  					// 2）在这一层中，pre的下一个key是>要删除key
  					if (next != null && next.isKeyEqual(key)) {
  						// free delete node memory -> C++
  						// level : pre -> next(key) -> ...
  						pre.nextNodes.set(level, next.nextNodes.get(level));
  					}
  					// 在level层只有一个节点了，就是默认节点head
  					if (level != 0 && pre == head && pre.nextNodes.get(level) == null) {
  						head.nextNodes.remove(level);
  						maxLevel--;
  					}
  					level--;
  				}
  			}
  		}
  ```



### class37

#### countOfRangeSum

- 链接：暂无

- 内容：

  > 给你一个混乱数组，和区间[lower,upper],求这个数组有多少个子数组在这个区间内，包含边界。

- 思路：

  > 改写sb树
  >
  > example：[4,5,3,-1,5,7,4,0,4,6]  [6,9]
  >
  > ans = 以[0]位置为最后的子数组的数量+以[1]位置为最后的子数组的数量+...+以[n-1]位置为最后的子数组的数量
  >
  > 以[n-1]位置为最后的子数组的数量 = 以[0]为开始的子数组在[Sum_(n_1) - 9,Sum_(n-1) - 6]的数量
  >
  > ...
  >
  > 可以把原始问题转化为
  >
  > 当前i的值为arr[i]，求之前所有子数组的和在[Sum_(n_1) - 9,Sum_(n-1) - 6]区间的数量
  >
  > 为了使其方便，可以在前面添加一个0
  >
  > 如下表

  | 当前下标 | 当前值 | 以0开始的子数组的和        | 前缀和 | 要求的区间（变换） | 满足数量                                         |
  | -------- | ------ | -------------------------- | ------ | ------------------ | ------------------------------------------------ |
  | 0        | 4      | 0(开始就添加的)            | 4      | [-5,-2]            | 0(如果4在区间中，那么有一个数字0在，直接能得到1) |
  | 1        | 5      | 0,4                        | 9      | [0,3]              | 1                                                |
  | 2        | 3      | 0,4,9                      | 12     | [3,6]              | 1                                                |
  | ...      | ...    | ...                        | ...    | ...                | ...                                              |
  | n-1      | 6      | 0,4,9,12,11,16,23,27,27,31 | 37     | [28,31]            | 1                                                |

  >根据上述的流程，我们可以看出，我们要设计一个结构满足以下几个方面
  >
  >1、能够添加重复值
  >
  >2、可以计算<num的数量
  >
  >3、时间复杂度要尽量低
  >
  >使用改写sb树的方法
  >
  >如下代码，all表示以自己为根的节点的树的节点数量 (all - c.l.all - c.r.all) 为自己这个节点为5的数量
  >
  >满足1和3
  >
  >计算< num的数量
  >
  >​	c.key < num    ans+=c.all - c.r.all
  >
  >   c.key == num ans += c.all - c.l.all -c.r.all
  >
  >   c.key > num   c = c.left
  >
  >  直到结束

  ```java
  	public static class SBTNode {
  		public long key;
  		public SBTNode l;
  		public SBTNode r;
  		public long size; // 不同key的size
  		public long all; // 总的size
  		public SBTNode(long k) {
  			key = k;
  			size = 1;
  			all = 1;
  		}
  	}
  /**                   5,6
                   3,2       7,3            
  **
  */
  ```

  

- 代码：

  ```java
  	public static int countRangeSum1(int[] nums, int lower, int upper) {
  		int n = nums.length;
  		long[] sums = new long[n + 1];
  		for (int i = 0; i < n; ++i)
  			sums[i + 1] = sums[i] + nums[i];
  		return countWhileMergeSort(sums, 0, n + 1, lower, upper);
  	}
  
  	private static int countWhileMergeSort(long[] sums, int start, int end, int lower, int upper) {
  		if (end - start <= 1)
  			return 0;
  		int mid = (start + end) / 2;
  		int count = countWhileMergeSort(sums, start, mid, lower, upper)
  				+ countWhileMergeSort(sums, mid, end, lower, upper);
  		int j = mid, k = mid, t = mid;
  		long[] cache = new long[end - start];
  		for (int i = start, r = 0; i < mid; ++i, ++r) {
  			while (k < end && sums[k] - sums[i] < lower)
  				k++;
  			while (j < end && sums[j] - sums[i] <= upper)
  				j++;
  			while (t < end && sums[t] < sums[i])
  				cache[r++] = sums[t++];
  			cache[r] = sums[i];
  			count += j - k;
  		}
  		System.arraycopy(cache, 0, sums, start, t - start);
  		return count;
  	}
  
  	public static class SBTNode {
  		public long key;
  		public SBTNode l;
  		public SBTNode r;
  		public long size; // 不同key的size
  		public long all; // 总的size
  
  		public SBTNode(long k) {
  			key = k;
  			size = 1;
  			all = 1;
  		}
  	}
  
  	public static class SizeBalancedTreeSet {
  		private SBTNode root;
  		private HashSet<Long> set = new HashSet<>();
  
  		private SBTNode rightRotate(SBTNode cur) {
  			long same = cur.all - (cur.l != null ? cur.l.all : 0) - (cur.r != null ? cur.r.all : 0);
  			SBTNode leftNode = cur.l;
  			cur.l = leftNode.r;
  			leftNode.r = cur;
  			leftNode.size = cur.size;
  			cur.size = (cur.l != null ? cur.l.size : 0) + (cur.r != null ? cur.r.size : 0) + 1;
  			// all modify
  			leftNode.all = cur.all;
  			cur.all = (cur.l != null ? cur.l.all : 0) + (cur.r != null ? cur.r.all : 0) + same;
  			return leftNode;
  		}
  
  		private SBTNode leftRotate(SBTNode cur) {
  			long same = cur.all - (cur.l != null ? cur.l.all : 0) - (cur.r != null ? cur.r.all : 0);
  			SBTNode rightNode = cur.r;
  			cur.r = rightNode.l;
  			rightNode.l = cur;
  			rightNode.size = cur.size;
  			cur.size = (cur.l != null ? cur.l.size : 0) + (cur.r != null ? cur.r.size : 0) + 1;
  			// all modify
  			rightNode.all = cur.all;
  			cur.all = (cur.l != null ? cur.l.all : 0) + (cur.r != null ? cur.r.all : 0) + same;
  			return rightNode;
  		}
  
  		private SBTNode maintain(SBTNode cur) {
  			if (cur == null) {
  				return null;
  			}
  			long leftSize = cur.l != null ? cur.l.size : 0;
  			long leftLeftSize = cur.l != null && cur.l.l != null ? cur.l.l.size : 0;
  			long leftRightSize = cur.l != null && cur.l.r != null ? cur.l.r.size : 0;
  			long rightSize = cur.r != null ? cur.r.size : 0;
  			long rightLeftSize = cur.r != null && cur.r.l != null ? cur.r.l.size : 0;
  			long rightRightSize = cur.r != null && cur.r.r != null ? cur.r.r.size : 0;
  			if (leftLeftSize > rightSize) {
  				cur = rightRotate(cur);
  				cur.r = maintain(cur.r);
  				cur = maintain(cur);
  			} else if (leftRightSize > rightSize) {
  				cur.l = leftRotate(cur.l);
  				cur = rightRotate(cur);
  				cur.l = maintain(cur.l);
  				cur.r = maintain(cur.r);
  				cur = maintain(cur);
  			} else if (rightRightSize > leftSize) {
  				cur = leftRotate(cur);
  				cur.l = maintain(cur.l);
  				cur = maintain(cur);
  			} else if (rightLeftSize > leftSize) {
  				cur.r = rightRotate(cur.r);
  				cur = leftRotate(cur);
  				cur.l = maintain(cur.l);
  				cur.r = maintain(cur.r);
  				cur = maintain(cur);
  			}
  			return cur;
  		}
  
  		private SBTNode add(SBTNode cur, long key, boolean contains) {
  			if (cur == null) {
  				return new SBTNode(key);
  			} else {
  				cur.all++;
  				if (key == cur.key) {
  					return cur;
  				} else { // 还在左滑或者右滑
  					if (!contains) {
  						cur.size++;
  					}
  					if (key < cur.key) {
  						cur.l = add(cur.l, key, contains);
  					} else {
  						cur.r = add(cur.r, key, contains);
  					}
  					return maintain(cur);
  				}
  			}
  		}
  
  		public void add(long sum) {
  			boolean contains = set.contains(sum);
  			root = add(root, sum, contains);
  			set.add(sum);
  		}
  
  		public long lessKeySize(long key) {
  			SBTNode cur = root;
  			long ans = 0;
  			while (cur != null) {
  				if (key == cur.key) {
  					return ans + (cur.l != null ? cur.l.all : 0);
  				} else if (key < cur.key) {
  					cur = cur.l;
  				} else {
  					ans += cur.all - (cur.r != null ? cur.r.all : 0);
  					cur = cur.r;
  				}
  			}
  			return ans;
  		}
  
  		// > 7 8...
  		// <8 ...<=7
  		public long moreKeySize(long key) {
  			return root != null ? (root.all - lessKeySize(key + 1)) : 0;
  		}
  
  	}
  ```

  

#### slideingWindowMedian

- 链接：暂无

- 内容：

  > 给你一个混乱的数组，窗口的区间为L，R，开始时LR都在最左侧
  >
  > 1、L可以向右移动
  >
  > 2、R可以向右移动
  >
  > 求任意L,R位置的中位数（排序后的那个），奇数返回中间，偶数返回(umid + lmid)/2

- 思路：

  > 我们可以创建一个结构，它满足以下要求
  >
  > 1、数据可重复
  >
  > 2、可以求出当前第几个位置的数字
  >
  > 3、复杂度较低
  >
  > 改写sb树
  >
  > ​     5,6
  >
  > 3,2     7,3
  >
  > 表示5有1个数，且左子树为2，右子树为3
  >
  > 若位置为4，则（6-3） = 3 ，位置4在右子树 -》以7为根的树找第1个节点

  ```java
  	public static class SBTNode<K extends Comparable<K>> {
  		public K key;
  		public SBTNode<K> l;
  		public SBTNode<K> r;
  		public int size;
  
  		public SBTNode(K k) {
  			key = k;
  			size = 1;
  		}
  	}
  ```

  

- 代码：

  ```java
  	public static class SBTNode<K extends Comparable<K>> {
  		public K key;
  		public SBTNode<K> l;
  		public SBTNode<K> r;
  		public int size;
  
  		public SBTNode(K k) {
  			key = k;
  			size = 1;
  		}
  	}
  
  	public static class SizeBalancedTreeMap<K extends Comparable<K>> {
  		private SBTNode<K> root;
  
  		private SBTNode<K> rightRotate(SBTNode<K> cur) {
  			SBTNode<K> leftNode = cur.l;
  			cur.l = leftNode.r;
  			leftNode.r = cur;
  			leftNode.size = cur.size;
  			cur.size = (cur.l != null ? cur.l.size : 0) + (cur.r != null ? cur.r.size : 0) + 1;
  			return leftNode;
  		}
  
  		private SBTNode<K> leftRotate(SBTNode<K> cur) {
  			SBTNode<K> rightNode = cur.r;
  			cur.r = rightNode.l;
  			rightNode.l = cur;
  			rightNode.size = cur.size;
  			cur.size = (cur.l != null ? cur.l.size : 0) + (cur.r != null ? cur.r.size : 0) + 1;
  			return rightNode;
  		}
  
  		private SBTNode<K> maintain(SBTNode<K> cur) {
  			if (cur == null) {
  				return null;
  			}
  			int leftSize = cur.l != null ? cur.l.size : 0;
  			int leftLeftSize = cur.l != null && cur.l.l != null ? cur.l.l.size : 0;
  			int leftRightSize = cur.l != null && cur.l.r != null ? cur.l.r.size : 0;
  			int rightSize = cur.r != null ? cur.r.size : 0;
  			int rightLeftSize = cur.r != null && cur.r.l != null ? cur.r.l.size : 0;
  			int rightRightSize = cur.r != null && cur.r.r != null ? cur.r.r.size : 0;
  			if (leftLeftSize > rightSize) {
  				cur = rightRotate(cur);
  				cur.r = maintain(cur.r);
  				cur = maintain(cur);
  			} else if (leftRightSize > rightSize) {
  				cur.l = leftRotate(cur.l);
  				cur = rightRotate(cur);
  				cur.l = maintain(cur.l);
  				cur.r = maintain(cur.r);
  				cur = maintain(cur);
  			} else if (rightRightSize > leftSize) {
  				cur = leftRotate(cur);
  				cur.l = maintain(cur.l);
  				cur = maintain(cur);
  			} else if (rightLeftSize > leftSize) {
  				cur.r = rightRotate(cur.r);
  				cur = leftRotate(cur);
  				cur.l = maintain(cur.l);
  				cur.r = maintain(cur.r);
  				cur = maintain(cur);
  			}
  			return cur;
  		}
  
  		private SBTNode<K> findLastIndex(K key) {
  			SBTNode<K> pre = root;
  			SBTNode<K> cur = root;
  			while (cur != null) {
  				pre = cur;
  				if (key.compareTo(cur.key) == 0) {
  					break;
  				} else if (key.compareTo(cur.key) < 0) {
  					cur = cur.l;
  				} else {
  					cur = cur.r;
  				}
  			}
  			return pre;
  		}
  
  		private SBTNode<K> add(SBTNode<K> cur, K key) {
  			if (cur == null) {
  				return new SBTNode<K>(key);
  			} else {
  				cur.size++;
  				if (key.compareTo(cur.key) < 0) {
  					cur.l = add(cur.l, key);
  				} else {
  					cur.r = add(cur.r, key);
  				}
  				return maintain(cur);
  			}
  		}
  
  		private SBTNode<K> delete(SBTNode<K> cur, K key) {
  			cur.size--;
  			if (key.compareTo(cur.key) > 0) {
  				cur.r = delete(cur.r, key);
  			} else if (key.compareTo(cur.key) < 0) {
  				cur.l = delete(cur.l, key);
  			} else {
  				if (cur.l == null && cur.r == null) {
  					// free cur memory -> C++
  					cur = null;
  				} else if (cur.l == null && cur.r != null) {
  					// free cur memory -> C++
  					cur = cur.r;
  				} else if (cur.l != null && cur.r == null) {
  					// free cur memory -> C++
  					cur = cur.l;
  				} else {
  					SBTNode<K> pre = null;
  					SBTNode<K> des = cur.r;
  					des.size--;
  					while (des.l != null) {
  						pre = des;
  						des = des.l;
  						des.size--;
  					}
  					if (pre != null) {
  						pre.l = des.r;
  						des.r = cur.r;
  					}
  					des.l = cur.l;
  					des.size = des.l.size + (des.r == null ? 0 : des.r.size) + 1;
  					// free cur memory -> C++
  					cur = des;
  				}
  			}
  			return cur;
  		}
  
  		private SBTNode<K> getIndex(SBTNode<K> cur, int kth) {
  			if (kth == (cur.l != null ? cur.l.size : 0) + 1) {
  				return cur;
  			} else if (kth <= (cur.l != null ? cur.l.size : 0)) {
  				return getIndex(cur.l, kth);
  			} else {
  				return getIndex(cur.r, kth - (cur.l != null ? cur.l.size : 0) - 1);
  			}
  		}
  
  		public int size() {
  			return root == null ? 0 : root.size;
  		}
  
  		public boolean containsKey(K key) {
  			if (key == null) {
  				throw new RuntimeException("invalid parameter.");
  			}
  			SBTNode<K> lastNode = findLastIndex(key);
  			return lastNode != null && key.compareTo(lastNode.key) == 0 ? true : false;
  		}
  
  		public void add(K key) {
  			if (key == null) {
  				throw new RuntimeException("invalid parameter.");
  			}
  			SBTNode<K> lastNode = findLastIndex(key);
  			if (lastNode == null || key.compareTo(lastNode.key) != 0) {
  				root = add(root, key);
  			}
  		}
  
  		public void remove(K key) {
  			if (key == null) {
  				throw new RuntimeException("invalid parameter.");
  			}
  			if (containsKey(key)) {
  				root = delete(root, key);
  			}
  		}
  
  		public K getIndexKey(int index) {
  			if (index < 0 || index >= this.size()) {
  				throw new RuntimeException("invalid parameter.");
  			}
  			return getIndex(root, index + 1).key;
  		}
  
  	}
  
  	public static class Node implements Comparable<Node> {
  		public int index;
  		public int value;
  
  		public Node(int i, int v) {
  			index = i;
  			value = v;
  		}
  
  		@Override
  		public int compareTo(Node o) {
  			return value != o.value ? Integer.valueOf(value).compareTo(o.value)
  					: Integer.valueOf(index).compareTo(o.index);
  		}
  	}
  
  	public static double[] medianSlidingWindow(int[] nums, int k) {
  		SizeBalancedTreeMap<Node> map = new SizeBalancedTreeMap<>();
  		for (int i = 0; i < k - 1; i++) {
  			map.add(new Node(i, nums[i]));
  		}
  		double[] ans = new double[nums.length - k + 1];
  		int index = 0;
  		for (int i = k - 1; i < nums.length; i++) {
  			map.add(new Node(i, nums[i]));
  			if (map.size() % 2 == 0) {
  				Node upmid = map.getIndexKey(map.size() / 2 - 1);
  				Node downmid = map.getIndexKey(map.size() / 2);
  				ans[index++] = ((double) upmid.value + (double) downmid.value) / 2;
  			} else {
  				Node mid = map.getIndexKey(map.size() / 2);
  				ans[index++] = (double) mid.value;
  			}
  			map.remove(new Node(i - k + 1, nums[i - k + 1]));
  		}
  		return ans;
  	}
  ```

  

#### addRemoveGetIndexGreat

- 链接：暂无

- 内容：

  > 实现arraylist并使其添加删除指定index的时间复杂度最小

- 思路：

  > 使用改写sb树的方法
  >
  > sb树的左旋，右旋操作是不会改变sb树的中序遍历顺序的，这也是数组的顺序
  >
  > 在指定index中添加或删除后，sb树会进行补丁操作，但它的中序遍历顺序是不变的，这保证了通过下标来get时的准确性。

- 代码：

  ```java
  public static class SBTNode<V> {
  		public V value;
  		public SBTNode<V> l;
  		public SBTNode<V> r;
  		public int size;
  
  		public SBTNode(V v) {
  			value = v;
  			size = 1;
  		}
  	}
  
  	public static class SbtList<V> {
  		private SBTNode<V> root;
  
  		private SBTNode<V> rightRotate(SBTNode<V> cur) {
  			SBTNode<V> leftNode = cur.l;
  			cur.l = leftNode.r;
  			leftNode.r = cur;
  			leftNode.size = cur.size;
  			cur.size = (cur.l != null ? cur.l.size : 0) + (cur.r != null ? cur.r.size : 0) + 1;
  			return leftNode;
  		}
  
  		private SBTNode<V> leftRotate(SBTNode<V> cur) {
  			SBTNode<V> rightNode = cur.r;
  			cur.r = rightNode.l;
  			rightNode.l = cur;
  			rightNode.size = cur.size;
  			cur.size = (cur.l != null ? cur.l.size : 0) + (cur.r != null ? cur.r.size : 0) + 1;
  			return rightNode;
  		}
  
  		private SBTNode<V> maintain(SBTNode<V> cur) {
  			if (cur == null) {
  				return null;
  			}
  			int leftSize = cur.l != null ? cur.l.size : 0;
  			int leftLeftSize = cur.l != null && cur.l.l != null ? cur.l.l.size : 0;
  			int leftRightSize = cur.l != null && cur.l.r != null ? cur.l.r.size : 0;
  			int rightSize = cur.r != null ? cur.r.size : 0;
  			int rightLeftSize = cur.r != null && cur.r.l != null ? cur.r.l.size : 0;
  			int rightRightSize = cur.r != null && cur.r.r != null ? cur.r.r.size : 0;
  			if (leftLeftSize > rightSize) {
  				cur = rightRotate(cur);
  				cur.r = maintain(cur.r);
  				cur = maintain(cur);
  			} else if (leftRightSize > rightSize) {
  				cur.l = leftRotate(cur.l);
  				cur = rightRotate(cur);
  				cur.l = maintain(cur.l);
  				cur.r = maintain(cur.r);
  				cur = maintain(cur);
  			} else if (rightRightSize > leftSize) {
  				cur = leftRotate(cur);
  				cur.l = maintain(cur.l);
  				cur = maintain(cur);
  			} else if (rightLeftSize > leftSize) {
  				cur.r = rightRotate(cur.r);
  				cur = leftRotate(cur);
  				cur.l = maintain(cur.l);
  				cur.r = maintain(cur.r);
  				cur = maintain(cur);
  			}
  			return cur;
  		}
  
  		private SBTNode<V> add(SBTNode<V> root, int index, SBTNode<V> cur) {
  			if (root == null) {
  				return cur;
  			}
  			root.size++;
  			int leftAndHeadSize = (root.l != null ? root.l.size : 0) + 1;
  			if (index < leftAndHeadSize) {
  				root.l = add(root.l, index, cur);
  			} else {
  				root.r = add(root.r, index - leftAndHeadSize, cur);
  			}
  			root = maintain(root);
  			return root;
  		}
  
  		private SBTNode<V> remove(SBTNode<V> root, int index) {
  			root.size--;
  			int rootIndex = root.l != null ? root.l.size : 0;
  			if (index != rootIndex) {
  				if (index < rootIndex) {
  					root.l = remove(root.l, index);
  				} else {
  					root.r = remove(root.r, index - rootIndex - 1);
  				}
  				return root;
  			}
  			if (root.l == null && root.r == null) {
  				return null;
  			}
  			if (root.l == null) {
  				return root.r;
  			}
  			if (root.r == null) {
  				return root.l;
  			}
  			SBTNode<V> pre = null;
  			SBTNode<V> suc = root.r;
  			suc.size--;
  			while (suc.l != null) {
  				pre = suc;
  				suc = suc.l;
  				suc.size--;
  			}
  			if (pre != null) {
  				pre.l = suc.r;
  				suc.r = root.r;
  			}
  			suc.l = root.l;
  			suc.size = suc.l.size + (suc.r == null ? 0 : suc.r.size) + 1;
  			return suc;
  		}
  
  		private SBTNode<V> get(SBTNode<V> root, int index) {
  			int leftSize = root.l != null ? root.l.size : 0;
  			if (index < leftSize) {
  				return get(root.l, index);
  			} else if (index == leftSize) {
  				return root;
  			} else {
  				return get(root.r, index - leftSize - 1);
  			}
  		}
  
  		public void add(int index, V num) {
  			SBTNode<V> cur = new SBTNode<V>(num);
  			if (root == null) {
  				root = cur;
  			} else {
  				if (index <= root.size) {
  					root = add(root, index, cur);
  				}
  			}
  		}
  
  		public V get(int index) {
  			SBTNode<V> ans = get(root, index);
  			return ans.value;
  		}
  
  		public void remove(int index) {
  			if (index >= 0 && size() > index) {
  				root = remove(root, index);
  			}
  		}
  
  		public int size() {
  			return root == null ? 0 : root.size;
  		}
  
  	}
  
  	// 通过以下这个测试，
  	// 可以很明显的看到LinkedList的插入、删除、get效率不如SbtList
  	// LinkedList需要找到index所在的位置之后才能插入或者读取，时间复杂度O(N)
  	// SbtList是平衡搜索二叉树，所以插入或者读取时间复杂度都是O(logN)
  	public static void main(String[] args) {
  		// 功能测试
  		int test = 50000;
  		int max = 1000000;
  		boolean pass = true;
  		ArrayList<Integer> list = new ArrayList<>();
  		SbtList<Integer> sbtList = new SbtList<>();
  		for (int i = 0; i < test; i++) {
  			if (list.size() != sbtList.size()) {
  				pass = false;
  				break;
  			}
  			if (list.size() > 1 && Math.random() < 0.5) {
  				int removeIndex = (int) (Math.random() * list.size());
  				list.remove(removeIndex);
  				sbtList.remove(removeIndex);
  			} else {
  				int randomIndex = (int) (Math.random() * (list.size() + 1));
  				int randomValue = (int) (Math.random() * (max + 1));
  				list.add(randomIndex, randomValue);
  				sbtList.add(randomIndex, randomValue);
  			}
  		}
  		for (int i = 0; i < list.size(); i++) {
  			if (!list.get(i).equals(sbtList.get(i))) {
  				pass = false;
  				break;
  			}
  		}
  		System.out.println("功能测试是否通过 : " + pass);
  
  		// 性能测试
  		test = 500000;
  		list = new ArrayList<>();
  		sbtList = new SbtList<>();
  		long start = 0;
  		long end = 0;
  
  		start = System.currentTimeMillis();
  		for (int i = 0; i < test; i++) {
  			int randomIndex = (int) (Math.random() * (list.size() + 1));
  			int randomValue = (int) (Math.random() * (max + 1));
  			list.add(randomIndex, randomValue);
  		}
  		end = System.currentTimeMillis();
  		System.out.println("ArrayList插入总时长(毫秒) ： " + (end - start));
  
  		start = System.currentTimeMillis();
  		for (int i = 0; i < test; i++) {
  			int randomIndex = (int) (Math.random() * (i + 1));
  			list.get(randomIndex);
  		}
  		end = System.currentTimeMillis();
  		System.out.println("ArrayList读取总时长(毫秒) : " + (end - start));
  
  		start = System.currentTimeMillis();
  		for (int i = 0; i < test; i++) {
  			int randomIndex = (int) (Math.random() * list.size());
  			list.remove(randomIndex);
  		}
  		end = System.currentTimeMillis();
  		System.out.println("ArrayList删除总时长(毫秒) : " + (end - start));
  
  		start = System.currentTimeMillis();
  		for (int i = 0; i < test; i++) {
  			int randomIndex = (int) (Math.random() * (sbtList.size() + 1));
  			int randomValue = (int) (Math.random() * (max + 1));
  			sbtList.add(randomIndex, randomValue);
  		}
  		end = System.currentTimeMillis();
  		System.out.println("SbtList插入总时长(毫秒) : " + (end - start));
  
  		start = System.currentTimeMillis();
  		for (int i = 0; i < test; i++) {
  			int randomIndex = (int) (Math.random() * (i + 1));
  			sbtList.get(randomIndex);
  		}
  		end = System.currentTimeMillis();
  		System.out.println("SbtList读取总时长(毫秒) :  " + (end - start));
  
  		start = System.currentTimeMillis();
  		for (int i = 0; i < test; i++) {
  			int randomIndex = (int) (Math.random() * sbtList.size());
  			sbtList.remove(randomIndex);
  		}
  		end = System.currentTimeMillis();
  		System.out.println("SbtList删除总时长(毫秒) :  " + (end - start));
  
  	}
  ```

  

### class38



## coding-for-great-offer

### class35

#### TopKFrequentElements

- 代码链接：https://leetcode.cn/problems/top-k-frequent-elements/description/

- 内容描述

  给你一个整数数组 `nums` 和一个整数 `k` ，请你返回其中出现频率前 `k` 高的元素。你可以按 **任意顺序** 返回答案。

- 思路：![](img/cfgo_35_1.png)

- 代码实现

  ```java
  public int[] topKFrequent(int[] nums, int k) {
          Map<Integer, Integer> map = new HashMap<>();
          for (int i = 0; i < nums.length; i++) {
              if (map.getOrDefault(nums[i], 0) == 0) {
                  map.put(nums[i], 1);
              } else {
                  map.put(nums[i], map.get(nums[i]) + 1);
              }
          }
          PriorityQueue<Integer> pq = new PriorityQueue<>(new Comparator<Integer>() {
              @Override
              public int compare(Integer o1, Integer o2) {
                  return map.get(o1) - map.get(o2);
              }
          });
          for (Integer key : map.keySet()) {
              if(pq.size() < k){
                  pq.add(key);
              }else if(map.get(key) > map.get(pq.peek())){
                  pq.remove();
                  pq.add(key);
              }
          }
          int[] ans = new int[k];
          int i = 0;
          while (!pq.isEmpty()) {
              ans[i++] = pq.remove();
          }
          return ans;
      }
  ```

#### LongestSubstringWithAtLeastKRepeatingCharacters

- 链接：

  https://leetcode.cn/problems/longest-substring-with-at-least-k-repeating-characters/description/

- 内容

  给你一个字符串 `s` 和一个整数 `k` ，请你找出 `s` 中的最长子串， 要求该子串中的每一字符出现次数都不少于 `k` 。返回这一子串的长度。

  如果不存在这样的子字符串，则返回 0。

- 思路

  ![](img/cfgo_35_2.png)

- 代码：

  ```java
  public int longestSubstring2(String s, int k) {
          char[] str = s.toCharArray();
          int max = 0; // 最长子串的长度
          int n = s.length();
      // 隐含条件，一定有i种字符构成的子串的各个字符数量满足>=k
          for (int i = 1; i <= 26; i++) { 
              int[] counts = new int[256];
              int kind = 0;//目前在counts数组中的种类
              int count = 0; // 满足>=k的种类数
              int R = -1;// 窗口的右边界
              for (int L = 0; L < n; L++) {
                  // [L...R]
                  while (R + 1 < n && !(kind == i && counts[str[R + 1] - 'a'] == 0)) {
                      // 扩到最右边，只要下一个R不会让kind=i+1
                      R++;
                      if (counts[str[R] - 'a'] == 0) {
                          // 当前kind未记录此字符值
                          kind++;
                      }
                      if (counts[str[R] - 'a'] == k - 1) {
                          // 当前字符的数量==k-1（没有算R位置的）
                          count++;
                      }
                      counts[str[R] - 'a']++; // 统一对R位置的字符数量++
                  }
                  // [L...R]
                  if (count == i) { // R未越界，且存在i个字符都达到了>=k
                      max = Math.max(max, R - L + 1);
                  }
                  // L++
                  if (counts[str[L] - 'a'] == 1) { // 当前字符数量为1，L右移就没有了
                      kind--;
                  }
                  if (counts[str[L] - 'a'] == k) { // 当前字符数量为k,L右移就没有了
                      count--;
                  }
                  counts[str[L] - 'a']--; // 对L的字符数量减-
              }
          }
          return max;
      }
  ```

  

#### FizzBuzz

- 链接：https://leetcode.cn/problems/fizz-buzz/description/

- 内容：

  > 给你一个整数 `n` ，找出从 `1` 到 `n` 各个整数的 Fizz Buzz 表示，并用字符串数组 `answer`（**下标从 1 开始**）返回结果，其中：
  >
  > - `answer[i] == "FizzBuzz"` 如果 `i` 同时是 `3` 和 `5` 的倍数。
  > - `answer[i] == "Fizz"` 如果 `i` 是 `3` 的倍数。
  > - `answer[i] == "Buzz"` 如果 `i` 是 `5` 的倍数。
  > - `answer[i] == i` （以字符串形式）如果上述条件全不满足。

- 思路：无

- 代码

  ```java
      public List<String> fizzBuzz(int n) {
          List<String> ans = new ArrayList<>();
          for (int i = 1; i <= n; i++) {
              if(i % 15 == 0){
                  ans.add("FizzBuzz");
              }else if (i % 5 == 0){
                  ans.add("Buzz");
              }else if (i % 3 == 0){
                  ans.add("Fizz");
              }else{
                  ans.add(i+"");
              }
          }
          return ans;
      }
  ```

  

#### 4SumII

- 链接：https://leetcode.cn/problems/4sum-ii/description/

- 内容：

  > 给你四个整数数组 `nums1`、`nums2`、`nums3` 和 `nums4` ，数组长度都是 `n` ，请你计算有多少个元组 `(i, j, k, l)` 能满足：
  >
  > - `0 <= i, j, k, l < n`
  > - `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`

- 思路：

  > 将前两个数组的各个和及其出现的次数存储在map中
  >
  > 遍历后两个数组，当后两个数组各个元素的值与map中的值相加等于0时，则有map.get(-temp)个组合

- 代码：

  ```java
  public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
          Map<Integer, Integer> map = new HashMap<>();
          for (int i = 0; i < nums1.length; i++) {
              for (int j = 0; j < nums2.length; j++) {
                  int temp = nums1[i] + nums2[j];
                  if(map.containsKey(temp)){
                      map.put(temp,map.get(temp)+1);
                  }else{
                      map.put(temp,1);
                  }
              }
          }
          int ans = 0;
          for (int i = 0; i < nums3.length; i++) {
              for (int j = 0; j < nums4.length; j++) {
                  int temp = nums3[i] + nums4[j];
                  if(map.containsKey(-temp)){
                      ans += map.get(-temp);
                  }
              }
          }
          return ans;
      }
  ```

#### 待补充）NumberOfLongestIncreasingSubsequence

#### LongestUnivaluePath

- 链接：https://leetcode.cn/problems/longest-univalue-path/description/

- 内容：

  > 给定一个二叉树的 `root` ，返回 *最长的路径的长度* ，这个路径中的 *每个节点具有相同值* 。 这条路径可以经过也可以不经过根节点。
  >
  > **两个节点之间的路径长度** 由它们之间的边数表示。

- 思路：

  > 二叉树的递归套路
  >
  > 对于路径有下面几种情况：
  >
  > 1、当前节点为最端，另一端为左子树或右子树（node.val = left.val）
  >
  > 2、当前节点不为端，左子树或右子树内有两个端点
  >
  > 3、当前节点不为端，但当前节点连接左右子树
  >
  > 需要：需要当前节点的最长值，也需要当前节点为端点的最长值

- 代码：

  ```java
   class Help{
              int length;// 路径必须从x出发且只能往下走的情况下，路径的最大距离
              int max;// 路径不要求必须从x出发的情况下，整棵树的合法路径最大距离
  		// getter,setter,constructor
          }
          public int longestUnivaluePath(TreeNode root) {
              if (root == null) {
                  return 0;
              }
              Help help = process(root);
              return help.max-1;
          }
          public Help process(TreeNode node){
              if(node == null){
                  return new Help(0,0);
              }
              TreeNode lNode = node.left;
              TreeNode rNode = node.right;
              // 获取此节点的左边的Help
              Help lHelp = process(lNode);
              Help rHelp = process(rNode);
              // 必须从x出发的情况下，往下的最大路径
              int len = 1;
              if (lNode != null && lNode.val == node.val) {
                  len = lHelp.length + 1;
              }
              if (rNode != null && rNode.val == node.val) {
                  len = Math.max(len,rHelp.length+1);
              }
              // 不要求从x出发，最大路径
              int max = Math.max(Math.max(lHelp.max, rHelp.max), len);
              if(lNode != null && rNode != null && lNode.val == node.val && rNode.val == node.val){
                  max = Math.max(max, lHelp.length + rHelp.length + 1);
              }
              return new Help(len,max);
          }
  ```

  

#### StringKth

- 内容：

  > 给定一个长度len，表示一共有几位, 所有字符都是小写(a~z)，可以生成长度为1，长度为2，长度为3...长度为len的所有字符串
  > 如果把所有字符串根据字典序排序，每个字符串都有所在的位置。
  > 给定一个字符串str，给定len，请返回str是总序列中的第几个。
  >
  > 比如len = 4，字典序的前几个字符串为:
  >  a aa aaa aaaa aaab ... aaaz ... azzz b ba baa baaa ... bzzz c ...
  > a是这个序列中的第1个，bzzz是这个序列中的第36558个

- 思路：

  > cdb，总共长度为7，请问cdb是第几个？
  > 第一位c :
  > 	以a开头，剩下长度为(0~6)的所有可能性有几个
  > 	 +
  > 	以b开头，剩下长度为(0~6)的所有可能性有几个
  > 	+
  > 	以c开头，剩下长度为(0)的所有可能性有几个
  >          第二位d :
  > 	           +
  > 	        以ca开头的情况下，剩下长度为(0~5)的所有可能性有几个
  > 	           +
  > 	       以cb开头的情况下，剩下长度为(0~5)的所有可能性有几个
  > 	          +
  > 	      以cc开头的情况下，剩下长度为(0~5)的所有可能性有几个
  > 	         +
  > 	      以cd开头的情况下，剩下长度为(0)的所有可能性有几个
  > 	         第三位b
  > 	             +
  > 	           以cda开头的情况下，剩下长度为(0~4)的所有可能性有几个
  > 	            +
  > 	           以cdb开头的情况下，剩下长度为(0)的所有可能性有几个

- 代码：

  ```java
  public static int kth(String s, int len) {
          if(s == null || s.length() == 0 || s.length() > len){
              return -1;
          }
          char[] num = s.toCharArray();
          int ans = 0;
          for (int i = 0,rest = len -1; i < num.length; i++,rest--) {
              ans += (num[i] - 'a') * f(rest) + 1;
          }
          return ans;
      }
      // 不管以什么开头，剩下长度为(0~len)的所有可能性有几个
      public static int f(int len){
          // 1 + 26 + 26^2+..+26^n
          int ans = 1;
          for (int i = 1,base = 26; i <= len; i++,base *= 26) {
              ans += base;
          }
          return ans;
      }
  ```

  

#### MagicStone

- 链接；小红书

- 内容：

  > // [0,4,7] ： 0表示这里石头没有颜色，如果变红代价是4，如果变蓝代价是7
  >
  > // [1,X,X] ： 1表示这里石头已经是红，而且不能改颜色，所以后两个数X无意义
  >
  > // [2,X,X] ： 2表示这里石头已经是蓝，而且不能改颜色，所以后两个数X无意义
  >
  > // 颜色只可能是0、1、2，代价一定>=0
  >
  > // 给你一批这样的小数组，要求最后必须所有石头都有颜色，且红色和蓝色一样多，返回最小代价
  >
  > // 如果怎么都无法做到所有石头都有颜色、且红色和蓝色一样多，返回-1

- 思路：

  > 如果 n为奇数，红与蓝不可能相等
  >
  > 统计所有的红与蓝的数量
  >
  > 如果最后红或蓝的数量超过一半，则不可能
  >
  > 如果红与蓝的数量都不超过一半，则需要所有的空白的颜色进行改变（贪心）
  >
  > [0,1,7] [0,5,2] [0,4,3] 要1个红，2个蓝
  >
  > 当所选择红时，要代价为10
  >
  > -6，-3，-1，第二个和第三个选择蓝，此时代价10 +(-3-1) = 6
  >
  > 1红+2蓝+3蓝= 1+2+3= 6

- 代码：

  ```java
  public static int minCost(int[][] stones) {
  		int n = stones.length;
  		if ((n & 1) != 0) {
  			return -1;
  		}
      // stones[i][2] - stones[i][1]; 这个值最小放在最前面
      // 当[0] = 0时，以[2]-[1]大小从小到大排序
  		Arrays.sort(stones, (a, b) -> a[0] == 0 && b[0] == 0 ? (b[1] - b[2] - a[1] + a[2]) : (a[0] - b[0]));
  		int zero = 0;
  		int red = 0;
  		int blue = 0;
  		int cost = 0;
  		for (int i = 0; i < n; i++) {
  			if (stones[i][0] == 0) {
  				zero++;
  				cost += stones[i][1];
  			} else if (stones[i][0] == 1) {
  				red++;
  			} else {
  				blue++;
  			}
  		}
  		if (red > (n >> 1) || blue > (n >> 1)) {
  			return -1;
  		}
  		blue = zero - ((n >> 1) - red);// 要选择改为蓝的数量
  		for (int i = 0; i < blue; i++) {
  			cost += stones[i][2] - stones[i][1]; // 这个值最小放在最前面
  		}
  		return cost;
  	}
  ```

  

#### WatchMovieMaxTime

- 链接：小红书

- 内容：

  > // 来自小红书
  >
  > // 一场电影开始和结束时间可以用一个小数组来表示["07:30","12:00"]
  >
  > // 已知有2000场电影开始和结束都在同一天，这一天从00:00开始到23:59结束
  >
  > // 一定要选3场完全不冲突的电影来观看，返回最大的观影时间
  >
  > // 如果无法选出3场完全不冲突的电影来观看，返回-1

- 思路：

  > 将所有的电影按照时间开始从小到大排序，按照结束时间从小到大排序
  >
  > 对于任一一个电影，可以选择观看，或者不观看，要满足观看三次，返回最大观影时间
  >
  >  process2(int[][] movies, int index, int time, int rest)
  >
  >  所有的电影，从index开始选择，开始时间，剩余观影次数
  >
  > +记忆化搜索

- 代码：

  ```java
  // 优化后的递归解
  	public static int maxEnjoy2(int[][] movies) {
  		Arrays.sort(movies, (a, b) -> a[0] != b[0] ? (a[0] - b[0]) : (a[1] - b[1]));
  		return process2(movies, 0, 0, 3);
  	}
  
  	public static int process2(int[][] movies, int index, int time, int rest) {
  		if (index == movies.length) {
  			return rest == 0 ? 0 : -1;
  		}
          // 不看这个电影
  		int p1 = process2(movies, index + 1, time, rest);
          // 先判断是否能看这个电影，且看这个电影，是否能满足三次观影
  		int next = movies[index][0] >= time && rest > 0 ? process2(movies, index + 1, movies[index][1], rest - 1) : -1;
          // 不可以则计-1，可以返回观影时间
  		int p2 = next != -1 ? (movies[index][1] - movies[index][0] + next) : -1;
  		return Math.max(p1, p2);
  	}
  
  	// 记忆化搜索的动态规划
  	public static int maxEnjoy3(int[][] movies) {
  		Arrays.sort(movies, (a, b) -> a[0] != b[0] ? (a[0] - b[0]) : (a[1] - b[1]));
  
  		int max = 0;
  		for (int[] movie : movies) {
  			max = Math.max(max, movie[1]);
  		}
  
  		int[][][] dp = new int[movies.length][max + 1][4];
  		for (int i = 0; i < movies.length; i++) {
  			for (int j = 0; j <= max; j++) {
  				for (int k = 0; k <= 3; k++) {
  					dp[i][j][k] = -2;// 用-2代表没算过这个过程
  				}
  			}
  		}
  		return process3(movies, 0, 0, 3, dp);
  	}
  
  	public static int process3(int[][] movies, int index, int time, int rest, int[][][] dp) {
  		if (index == movies.length) {
  			return rest == 0 ? 0 : -1;
  		}
  		if (dp[index][time][rest] != -2) {
  			return dp[index][time][rest];
  		}
  		int p1 = process3(movies, index + 1, time, rest, dp);
  		int next = movies[index][0] >= time && rest > 0 ? process3(movies, index + 1, movies[index][1], rest - 1, dp)
  				: -1;
  		int p2 = next != -1 ? (movies[index][1] - movies[index][0] + next) : -1;
  		int ans = Math.max(p1, p2);
  		dp[index][time][rest] = ans;
  		return ans;
  	}
  ```

  

#### WalkToEnd

- 链接：网易

- 内容：

  > // map[i][j] == 0，代表(i,j)是海洋，渡过的话代价是2
  >
  > // map[i][j] == 1，代表(i,j)是陆地，渡过的话代价是1
  >
  > // map[i][j] == 2，代表(i,j)是障碍，无法渡过
  >
  > // 每一步上、下、左、右都能走，返回从左上角走到右下角最小代价是多少，如果无法到达返回-1

- 思路：

  > 从[0,0]开始走，向上下左右，如果能走到最后说明存在
  >
  > 建立小根堆，将访问过的标记，如果存在当前节点到最后的路，则一定是最小的
  >
  > 如果没返回，说明不能走标记过的路，（走了也一定不是最小，且无法通过）

- 代码：

  ```java
  public static int minCost(int[][] map) {
          if (map[0][0] == 2) {
              return -1;
          }
          int n = map.length;
          int m = map[0].length;
          PriorityQueue<Node> heap = new PriorityQueue<>((a, b) -> a.cost - b.cost);
          boolean[][] visited = new boolean[n][m];
          add(map, 0, 0, 0, heap, visited);
          while (!heap.isEmpty()) {
              Node cur = heap.poll();
              if (cur.row == n - 1 && cur.col == m - 1) {
                  return cur.cost;
              }
              add(map, cur.row - 1, cur.col, cur.cost, heap, visited);
              add(map, cur.row + 1, cur.col, cur.cost, heap, visited);
              add(map, cur.row, cur.col - 1, cur.cost, heap, visited);
              add(map, cur.row, cur.col + 1, cur.cost, heap, visited);
          }
          return -1;
      }
  
      public static void add(int[][] m, int i, int j, int pre, PriorityQueue<Node> heap, boolean[][] visited) {
          if (i >= 0 && i < m.length && j >= 0 && j < m[0].length && m[i][j] != 2 && !visited[i][j]) {
              heap.add(new Node(i, j, pre + (m[i][j] == 0 ? 2 : 1)));
              visited[i][j] = true;
          }
      }
  
      public static class Node {
          public int row;
          public int col;
          public int cost;
  
          public Node(int a, int b, int c) {
              row = a;
              col = b;
              cost = c;
          }
      }
  ```

  

#### CircleCandy

- 链接：网易

- 内容：

  > 给定一个正数数组arr，表示每个小朋友的得分
  >
  > // 任何两个相邻的小朋友，如果得分一样，怎么分糖果无所谓，但如果得分不一样，分数大的一定要比分数少的多拿一些糖果
  >
  > // 假设所有的小朋友坐成一个环形，返回在不破坏上一条规则的情况下，需要的最少糖果数

- 思路：

  > 如果不是环形，则可以使用两个数组
  >
  > 原      [3,4,2,1,5,6,2,4]
  >
  > left    [1,2,1,1,2,3,1,2]
  >
  > right [1,3,2,1,1,2,1,1]
  >
  > 最小  [1,3,2,1,2,3,1,2]
  >
  > 如果是环形的，我们可以先找到全局最小值
  >
  > 环形 3,4,2,1,5,6,2,4
  >
  > 下标 0,1,2,3,4,5,6,7
  >
  > 下标3最小 =》生成一个n+1的数组 1,5,6,2,4,3,4,2,1
  >
  > ​                                                   下标 3,4,5,6,7,0,1,2,3
  >
  > 对环形进行不环形的求解，同上

- 代码：

  ```java
  public static int minCandy(int[] arr) {
  		if (arr == null || arr.length == 0) {
  			return 0;
  		}
  		if (arr.length == 1) {
  			return 1;
  		}
  		int n = arr.length;
  		int minIndex = 0;
  		for (int i = 0; i < n; i++) {
  			if (arr[i] <= arr[lastIndex(i, n)] && arr[i] <= arr[nextIndex(i, n)]) {
  				minIndex = i;
  				break;
  			}
  		}
  		int[] nums = new int[n + 1];
  		for (int i = 0; i <= n; i++, minIndex = nextIndex(minIndex, n)) {
  			nums[i] = arr[minIndex];
  		}
  		int[] left = new int[n + 1];
  		left[0] = 1;
  		for (int i = 1; i <= n; i++) {
  			left[i] = nums[i] > nums[i - 1] ? (left[i - 1] + 1) : 1;
  		}
  		int[] right = new int[n + 1];
  		right[n] = 1;
  		for (int i = n - 1; i >= 0; i--) {
  			right[i] = nums[i] > nums[i + 1] ? (right[i + 1] + 1) : 1;
  		}
  		int ans = 0;
  		for (int i = 0; i < n; i++) {
  			ans += Math.max(left[i], right[i]);
  		}
  		return ans;
  	}
  
  	public static int nextIndex(int i, int n) {
  		return i == n - 1 ? 0 : (i + 1);
  	}
  
  	public static int lastIndex(int i, int n) {
  		return i == 0 ? (n - 1) : (i - 1);
  	}
  ```

  

### class36

#### ReverseInvertString

- 链接：网易

- 内容：

  > // 规定：L[1]对应a，L[2]对应b，L[3]对应c，...，L[25]对应y
  > // S1 = a
  > // S(i) = S(i-1) + L[i] + reverse(invert(S(i-1)));
  > // 解释invert操作：
  > // S1 = a
  > // S2 = aby
  > // 假设invert(S(2)) = 甲乙丙
  > // a + 甲 = 26, 那么 甲 = 26 - 1 = 25 -> y
  > // b + 乙 = 26, 那么 乙 = 26 - 2 = 24 -> x
  > // y + 丙 = 26, 那么 丙 = 26 - 25 = 1 -> a
  > // 如上就是每一位的计算方式，所以invert(S2) = yxa
  > // 所以S3 = S2 + L[3] + reverse(invert(S2)) = aby + c + axy = abycaxy
  > // invert(abycaxy) = yxawyba, 再reverse = abywaxy
  > // 所以S4 = abycaxy + d + abywaxy = abycaxydabywaxy
  > // 直到S25结束
  > // 给定两个参数n和k，返回Sn的第k位是什么字符，n从1开始，k从1开始
  > // 比如n=4，k=2，表示S4的第2个字符是什么，返回b字符
  >
  > 给你两个参数n与k，返回Sn的第k个字符

- 思路：

  > 分治（二分）：
  >
  > 思路：Sn 是由Sn-1 + Ln + R(I(Sn-1))得到的，则对于它的第k个位置有三个不同的情况
  >
  > k <= len(Sn-1)时，等价于Sn-1的第k个位置
  >
  > k == len(Sn-1)+1时，等价于Ln的值
  >
  > k > len(Sn-1)+1时，等价于Sn-1的第  2*(len(Sn-1)+1)-k位置的**值的invert**

- 代码

  ```java
  public class Code01_ReverseInvertString {
  	static int[] len;
  	static {
  		len = new int[26];
  		len[1] = 1;
  		// init
  		for (int i = 2; i < len.length; i++) {
  			len[i] = 2*len[i-1] + 1;
  		}
  	}
  
  	// 求sn中的第k个字符
  	// O(n), s <= 25 O(1)
  	public static char kth(int n, int k) {
  		if(n == 1) return 'a';
  		int length = len[n-1];
  		if(k <= length){
  			return kth(n-1,k);
  		}else if(k == length+1){
  			return (char) ('a' + n - 1);
  		}else{
  			// sn
  			// 我需要右半区，从左往右的第a个
  			// 需要找到，s(n-1)从右往左的第a个
  			// 当拿到字符之后，invert一下，就可以返回了！
  			// abc
  			//     wxy
  //			return invert(kth(n-1,length-(k-length-1)+1));
  			return invert(kth(n-1,length*2-k+2));
  		}
  	}
  
  	public static Character invert(Character c){
  		// a97 -> y121 b98->x120
  		Character c1 = (char) (218 - c);
  		return c1;
  	}
  }
  ```

#### Ratio01Split

- 链接：京东

- 内容：

  > // 把一个01字符串切成多个部分，要求每一部分的0和1比例一样，同时要求尽可能多的划分
  >
  > // 比如 : 01010101
  >
  > // 01 01 01 01 这是一种切法，0和1比例为 1 : 1
  >
  > // 0101 0101 也是一种切法，0和1比例为 1 : 1
  >
  > // 两种切法都符合要求，但是那么尽可能多的划分为第一种切法，部分数为4
  >
  > // 比如 : 00001111
  >
  > // 只有一种切法就是00001111整体作为一块，那么尽可能多的划分，部分数为1
  >
  > // 给定一个01字符串str，假设长度为N，要求返回一个长度为N的数组ans
  >
  > // 其中ans[i] = str[0...i]这个前缀串，要求每一部分的0和1比例一样，同时要求尽可能多的划分下，部分数是多少
  >
  > // 输入: str = "010100001"
  >
  > // 输出: ans = [1, 1, 1, 2, 1, 2, 1, 1, 3]

- 思路：

  > 整体与局部的关系
  >
  > 当[L,R]范围内的0与1的比例是3：7
  >
  > 存在L<j<R使得[j,R]范围内的0与1的比例也是3：7，则有[L,j-1]范围内的0与1的比例也是3：7
  >
  > 所以当前位置的值是多少，就等价于它之前的存在这个比例的数量
  >
  > // 输入: str = "010100001"
  >
  > // 输出: ans = [1, 1, 1, 2, 1, 2, 1, 1, 3]
  >
  > 如下黑体显示的当前的0与1的比例在之前存在，则其值为 取之前数量+1

  | 下标 | 值   | 比例                                                |
  | ---- | ---- | --------------------------------------------------- |
  | 0    | 0    | 1：0->1                                             |
  | 1    | 1    | 1:0->1    1:1->1                                    |
  | 2    | 0    | 1:0->1    1:1->1  2:1->1                            |
  | 3    | 1    | 1:0->1    **1:1->2**  2:1->1                        |
  | 4    | 0    | 1:0->1    1:1->2  2:1->1  3:2->1                    |
  | 5    | 0    | 1:0->1    1:1->2  **2:1->2**  3:2->1                |
  | 6    | 0    | 1:0->1    1:1->2  2:1->2  3:2->1  5:2->1            |
  | 7    | 0    | 1:0->1    1:1->2  2:1->2  3:2->1  5:2->1 3:1->1     |
  | 8    | 1    | 1:0->1    1:1->2  **2:1->3**  3:2->1  5:2->1 3:1->1 |

- 代码：

  ```java
  	public static int[] split(int[] arr) {
  		// key : 分子
  		// value : 属于key的分母表, 每一个分母，及其 分子/分母 这个比例，多少个前缀拥有
  		Map<Integer, Map<Integer, Integer>> map = new HashMap<>();
  		int n = arr.length;
  		int[] ans = new int[n];
  		int zeroCount = 0; // 0的次数
  		int oneCount = 0;// 1的次数
  		for (int i = 0; i < arr.length; i++) {
  			if(arr[i] == 0){
  				zeroCount++;
  			}else{
  				oneCount++;
  			}
  			if(zeroCount == 0 || oneCount == 0){
  				ans[i] = i+1; // 所有的0或1分为单个
  			}else{
  				// 求最大公约数
  				int g = gcd(zeroCount,oneCount);
  				int x = zeroCount/g; // 分子
  				int y = oneCount/g; // 分母
  				if(!map.containsKey(x)){
  					map.put(x,new HashMap<>());
  				}
  				if(!map.get(x).containsKey(y)){
  					map.get(x).put(y,1);
  				}else{
  					map.get(x).put(y,map.get(x).get(y)+1);
  				}
  				ans[i] = map.get(x).get(y);
  			}
  		}
  		return ans;
  	}
  // 辗转相除法
  	public static int gcd(int m,int n){
  		while (m != 0){
  			int temp = m;
  			m = n%m;
  			n = temp;
  		}
  		return n;
  	}
  ```

#### MatchCount-前置知识（kmp)

- 链接：美团

- 内容：

  > // 给定两个字符串s1和s2
  > // 返回在s1中有多少个子串等于s2

- 思路：

  > kmp更改一下，将next数组扩宽一位，变成如下
  >
  > 原：求aaa子串在aaaaaa中出现的次数
  >
  > 改为类似为：求aaa?子串在aaaaaa中是否匹配
  >
  > 由aaa?得到的next数组与aaaaaa作匹配，每当轮到?时，我们可知已经匹配成功了，将这个值+1，然后再继续用next数组作不回退匹配即可

- 代码：

  ```java
  public class Code03_MatchCount {
  	public static int sa(String s1, String s2) {
  		if (s1 == null || s2 == null || s1.length() < s2.length()) {
  			return 0;
  		}
  		char[] str1 = s1.toCharArray();
  		char[] str2 = s2.toCharArray();
  		return count(str1, str2);
  	}
  	// 改写kmp为这道题需要的功能
  	public static int count(char[] str1, char[] str2) {
  		int x = 0;
  		int y = 0;
  		int count = 0;
  		int[] next = getNextArray(str2);
  		while (x < str1.length) {
  			if (str1[x] == str2[y]) {
  				x++;
  				y++;
  				if (y == str2.length) {
  					count++;
  					y = next[y];
  				}
  			} else if (next[y] == -1) {
  				x++;
  			} else {
  				y = next[y];
  			}
  		}
  		return count;
  	}
  	// next数组多求一位
  	// 比如：str2 = aaaa
  	// 那么，next = -1,0,1,2,3
  	// 最后一个3表示，终止位置之前的字符串最长前缀和最长后缀的匹配长度
  	// 也就是next数组补一位
  	public static int[] getNextArray(char[] str2) {
  		if (str2.length == 1) {
  			return new int[] { -1, 0 };
  		}
  		int[] next = new int[str2.length + 1];
  		next[0] = -1;
  		next[1] = 0;
  		int i = 2;
  		int cn = 0;
  		while (i < next.length) {
  			if (str2[i - 1] == str2[cn]) {
  				next[i++] = ++cn;
  			} else if (cn > 0) {
  				cn = next[cn];
  			} else {
  				next[i++] = 0;
  			}
  		}
  		return next;
  	}
  }
  ```

#### ComputeExpressionValue

- 链接：美团

- 内容：

  >  () 分值为2， (()) 分值为3， ((())) 分值为4
  >
  >  也就是说，每包裹一层，分数就是里面的分值+1
  >
  >  ()() 分值为2 * 2，(())() 分值为3 * 2
  >
  > 也就是说，每连接一段，分数就是各部分相乘，以下是一个结合起来的例子
  >
  >  (()())()(()) -> (2 * 2 + 1) * 2 * 3 -> 30
  >
  >  给定一个括号字符串str，已知str一定是正确的括号结合，不会有违规嵌套
  >
  >  返回分数

- 思路：

  > 用栈来计算
  >
  > 例 (()())()(()) 长度为12，f(i)返回两个值，第一个值返回的是与其匹配的右括号的值-1，第二个返回值是右括号的位置
  >
  > f(i)所返回的值 是[i,info[1]]这个区间的值
  >
  > ans是记录当前[0,i]这个区间的得分的

  | 当前位置 | 当前值 | 局部ans          | 全局ans |
  | -------- | ------ | ---------------- | ------- |
  | 0        | (      | 0                | 1       |
  | 1        | (      | 1(进入了新的f中) | 1       |
  | 2        | )      | 0                | 2       |
  | 3        | (      | 1(进入了新的f中) | 2       |
  | 4        | )      | 0                | 4       |
  | 5        | )      | 0                | 5       |
  | 6        | (      | 1(进入了新的f中) | 5       |
  | 7        | )      | 0                | 10      |
  | 8        | (      | 1(进入了新的f中) | 10      |
  | 9        | (      | 1(进入了新的f中) | 10      |
  | 10       | )      | 2                | 10      |
  | 11       | )      | 0                | 30      |

- 代码

  ```java
  public static int sores(String s) {
  		return compute(s.toCharArray(), 0)[0];
  	}
  	// s[i.....] 遇到 ')' 或者 终止位置  停！
  	// 返回值：int[]  长度就是2
  	// 0 ：分数是多少
  	// 1 : 来到了什么位置停的！
  	public static int[] compute(char[] s, int i) {
  		if (s[i] == ')') {
  			return new int[] { 1, i };
  		}
  		int ans = 1;
  		while (i < s.length && s[i] != ')') {
  			int[] info = compute(s, i + 1);
  			ans *= info[0] + 1;
  			i = info[1] + 1;
  		}
  		return new int[] { ans, i };
  	}
  ```

#### Query3Problems-前置知识（线段树）

- 链接：美团

- 内容：

  > ```
  > 给定一个数组arr，长度为N，做出一个结构，可以高效的做如下的查询
  > 1) int querySum(L,R) : 查询arr[L...R]上的累加和
  > 2) int queryAim(L,R) : 查询arr[L...R]上的目标值，目标值定义如下：
  >        假设arr[L...R]上的值为[a,b,c,d]，a+b+c+d = s
  >        目标值为 : (s-a)^2 + (s-b)^2 + (s-c)^2 + (s-d)^2
  > 3) int queryMax(L,R) : 查询arr[L...R]上的最大值
  > 要求：
  > 1) 初始化该结构的时间复杂度不能超过O(N*logN)
  > 2) 三个查询的时间复杂度不能超过O(logN)
  > 3) 查询时，认为arr的下标从1开始，比如 : 
  >    arr = [ 1, 1, 2, 3 ];
  >    querySum(1, 3) -> 4
  >    queryAim(2, 4) -> 50
  >    queryMax(1, 4) -> 3
  > ```

- 思路：

  > 1)使用前缀和，3)使用线段树求区间最大值
  >
  > 2)拆开后为s^2 - 2as +a^2+...s^2-2ds+d^2=4*s^2+a^2+b^2+c^2+d^2-2s(a+b+c+d)
  >
  >  = 2*s^2 + a^2+b^2+c^2+d^2
  >
  > 使用平方的一个前缀和数组

- 代码：

  ```java
  public class Code05_Query3Problems {
  	public static class SegmentTree {
  		private int[] max;
  		private int[] change;
  		private boolean[] update;
  		public SegmentTree(int N) {
  			max = new int[N << 2];
  			change = new int[N << 2];
  			update = new boolean[N << 2];
  			for (int i = 0; i < max.length; i++) {
  				max[i] = Integer.MIN_VALUE;
  			}
  		}
  		private void pushUp(int rt) {
  			max[rt] = Math.max(max[rt << 1], max[rt << 1 | 1]);
  		}
  		// ln表示左子树元素结点个数，rn表示右子树结点个数
  		private void pushDown(int rt, int ln, int rn) {
  			if (update[rt]) {
  				update[rt << 1] = true;
  				update[rt << 1 | 1] = true;
  				change[rt << 1] = change[rt];
  				change[rt << 1 | 1] = change[rt];
  				max[rt << 1] = change[rt];
  				max[rt << 1 | 1] = change[rt];
  				update[rt] = false;
  			}
  		}
  		public void update(int L, int R, int C, int l, int r, int rt) {
  			if (L <= l && r <= R) {
  				update[rt] = true;
  				change[rt] = C;
  				max[rt] = C;
  				return;
  			}
  			int mid = (l + r) >> 1;
  			pushDown(rt, mid - l + 1, r - mid);
  			if (L <= mid) {
  				update(L, R, C, l, mid, rt << 1);
  			}
  			if (R > mid) {
  				update(L, R, C, mid + 1, r, rt << 1 | 1);
  			}
  			pushUp(rt);
  		}
  		public int query(int L, int R, int l, int r, int rt) {
  			if (L <= l && r <= R) {
  				return max[rt];
  			}
  			int mid = (l + r) >> 1;
  			pushDown(rt, mid - l + 1, r - mid);
  			int left = 0;
  			int right = 0;
  			if (L <= mid) {
  				left = query(L, R, l, mid, rt << 1);
  			}
  			if (R > mid) {
  				right = query(L, R, mid + 1, r, rt << 1 | 1);
  			}
  			return Math.max(left, right);
  		}
  	}
  	public static class Query {
  		public int[] sum1;
  		public int[] sum2;
  		public SegmentTree st;
  		public int m;
  		public Query(int[] arr) {
  			int n = arr.length;
  			m = arr.length + 1;
  			sum1 = new int[m];
  			sum2 = new int[m];
  			st = new SegmentTree(m);
  			for (int i = 0; i < n; i++) {
  				sum1[i + 1] = sum1[i] + arr[i];
  				sum2[i + 1] = sum2[i] + arr[i] * arr[i];
  				st.update(i + 1, i + 1, arr[i], 1, m, 1);
  			}
  		}
  		public int querySum(int L, int R) {
  			return sum1[R] - sum1[L - 1];
  		}
  		public int queryAim(int L, int R) {
  			int sumPower2 = querySum(L, R);
  			sumPower2 *= sumPower2;
  			return sum2[R] - sum2[L - 1] + (R - L - 1) * sumPower2;
  		}
  		public int queryMax(int L, int R) {
  			return st.query(L, R, 1, m, 1);
  		}
  	}
  	public static void main(String[] args) {
  		int[] arr = { 1, 1, 2, 3 };
  		Query q = new Query(arr);
  		System.out.println(q.querySum(1, 3));
  		System.out.println(q.queryAim(2, 4));
  		System.out.println(q.queryMax(1, 4));
  	}
  }
  ```

#### NodeWeight

- 链接：美团

- 内容：

  > ```
  > 有一棵树，给定头节点h，和结构数组m，下标0弃而不用
  > 比如h = 1, m = [ [] , [2,3], [4], [5,6], [], [], []]
  > 表示1的孩子是2、3; 2的孩子是4; 3的孩子是5、6; 4、5和6是叶节点，都不再有孩子
  > 每一个节点都有颜色，记录在c数组里，比如c[i] = 4, 表示节点i的颜色为4
  > 一开始只有叶节点是有权值的，记录在w数组里，
  > 比如，如果一开始就有w[i] = 3, 表示节点i是叶节点、且权值是3
  > 现在规定非叶节点i的权值计算方式：
  > 根据i的所有直接孩子来计算，假设i的所有直接孩子，颜色只有a,b,k
  > w[i] = Max {
  >              (颜色为a的所有孩子个数 + 颜色为a的孩子权值之和), 
  >              (颜色为b的所有孩子个数 + 颜色为b的孩子权值之和),
  >              (颜色为k的所有孩子个数 + 颜色k的孩子权值之和)
  >            }
  > 请计算所有孩子的权值并返回
  > ```

- 思路：

  > 后序遍历+map集合求最大值

- 代码：

  ```java
  public class Code06_NodeWeight {
  
  	// 当前来到h节点，
  	// h的直接孩子，在哪呢？m[h] = {a,b,c,d,e}
  	// 每个节点的颜色在哪？比如i号节点，c[i]就是i号节点的颜色
  	// 每个节点的权值在哪？比如i号节点，w[i]就是i号节点的权值
  	// void : 把w数组填满就是这个函数的目标
  	public static void w(int h, int[][] m, int[] w, int[] c) {
  		if (m[h].length == 0) { // 叶节点
  			return;
  		}
  		// 有若干个直接孩子
  		// 1 7个
  		// 3 10个
  		HashMap<Integer, Integer> colors = new HashMap<Integer, Integer>();
  		// 1 20
  		// 3 45
  		HashMap<Integer, Integer> weights = new HashMap<Integer, Integer>();
  		for (int child : m[h]) {
              // 对其子节点进行处理
  			w(child, m, w, c);
              // 维护颜色及权重值
  			colors.put(c[child], colors.getOrDefault(c[child], 0) + 1);
  			weights.put(c[child], weights.getOrDefault(c[child], 0) + w[child]);
  		}
  		for (int color : colors.keySet()) {
              // 将最大的值写入w数组中即可
  			w[h] = Math.max(w[h], colors.get(color) + weights.get(color));
  		}
  	}
  }
  ```

#### PickAddMax

- 链接：腾讯

- 内容：

  > 给定一个数组arr，当拿走某个数a的时候，其他所有的数都+a
  >  请返回最终所有数都拿走的最大分数
  >  比如: [2,3,1]
  >  当拿走3时，获得3分，数组变成[5,4]
  >  当拿走5时，获得5分，数组变成[9]
  >  当拿走9时，获得9分，数组变成[]
  >  这是最大的拿取方式，返回总分17

- 思路：

  > 每次拿当前数组中的最大值，记录最后的结果

- 代码：

  ```java
  	public static int pick(int[] arr) {
  		Arrays.sort(arr);
  		int ans = 0;
  		for (int i = arr.length - 1; i >= 0; i--) {
  			ans = (ans << 1) + arr[i];
  		}
  		return ans;
  	}
  ```

#### MinBoatEvenNumbers-前置知识（同时坐船，最小数量）

- 链接：腾讯

- 内容：

  > 给定一个正数数组arr，代表每个人的体重。给定一个正数limit代表船的载重，所有船都是同样的载重量
  > 每个人的体重都一定不大于船的载重
  > 要求：
  > 1, 可以1个人单独一搜船
  > 2, 一艘船如果坐2人，两个人的体重相加需要是偶数，且总体重不能超过船的载重
  > 3, 一艘船最多坐2人
  > 返回如果想所有人同时坐船，船的最小数量

- 思路：

  > 分为奇数与偶数两个数组，对每个数组求其最小值

- 代码：

  ```java
  public class Code08_MinBoatEvenNumbers {
  
  	public static int minBoat(int[] arr, int limit) {
  		Arrays.sort(arr);
  		int odd = 0;
  		int even = 0;
  		for (int num : arr) {
  			if ((num & 1) == 0) {
  				even++;
  			} else {
  				odd++;
  			}
  		}
  		int[] odds = new int[odd];
  		int[] evens = new int[even];
  		for (int i = arr.length - 1; i >= 0; i--) {
  			if ((arr[i] & 1) == 0) {
  				evens[--even] = arr[i];
  			} else {
  				odds[--odd] = arr[i];
  			}
  		}
  		return min(odds, limit) + min(evens, limit);
  	}
  
  	public static int min(int[] arr, int limit) {
  		if (arr == null || arr.length == 0) {
  			return 0;
  		}
  		int N = arr.length;
  		if (arr[N - 1] > limit) {
  			return -1;
  		}
  		int lessR = -1;
  		for (int i = N - 1; i >= 0; i--) {
  			if (arr[i] <= (limit / 2)) {
  				lessR = i;
  				break;
  			}
  		}
  		if (lessR == -1) {
  			return N;
  		}
  		int L = lessR;
  		int R = lessR + 1;
  		int noUsed = 0;
  		while (L >= 0) {
  			int solved = 0;
  			while (R < N && arr[L] + arr[R] <= limit) {
  				R++;
  				solved++;
  			}
  			if (solved == 0) {
  				noUsed++;
  				L--;
  			} else {
  				L = Math.max(-1, L - solved);
  			}
  		}
  		int all = lessR + 1;
  		int used = all - noUsed;
  		int moreUnsolved = (N - all) - used;
  		return used + ((noUsed + 1) >> 1) + moreUnsolved;
  	}
  	
  	// 首尾双指针的解法
  	public static int numRescueBoats2(int[] people, int limit) {
  		Arrays.sort(people);
  		int ans = 0;
  		int l = 0;
  		int r = people.length - 1;
  		int sum = 0;
  		while (l <= r) {
  			sum = l == r ? people[l] : people[l] + people[r];
  			if (sum > limit) {
  				r--;
  			} else {
  				l++;
  				r--;
  			}
  			ans++;
  		}
  		return ans;
  	}
  
  }
  ```

  

#### MaxKLenSequence-前置知识（单调栈）

- 链接：腾讯

- 内容：

  >  给定一个字符串str，和一个正数k
  > 返回长度为k的所有子序列中，字典序最大的子序列

- 思路：

  > 使用单调栈对子序列进行压栈，当栈中数量+剩余子串的数量 = k时，
  >
  > 单调栈中的元素+剩余子串构成的序列即为字典序最大的子序列

- 代码：

  ```java
  	public static String maxString(String s, int k) {
  		if (k <= 0 || s.length() < k) {
  			return "";
  		}
  		char[] str = s.toCharArray();
  		int n = str.length;
  		char[] stack = new char[n];
  		int size = 0;
  		for (int i = 0; i < n; i++) {
  			while (size > 0 && stack[size - 1] < str[i] && size + n - i > k) {
  				size--;
  			}
  			if (size + n - i == k) {
  				return String.valueOf(stack, 0, size) + s.substring(i);
  			}
  			stack[size++] = str[i];
  		}
  		return String.valueOf(stack, 0, k);
  	}
  ```

#### StoneGameIV

- 链接：https://leetcode.com/problems/stone-game-iv/

- 内容：

  > 一开始，有 `n` 个石子堆在一起。每个人轮流操作，正在操作的玩家可以从石子堆里拿走 **任意** 非零 **平方数** 个石子。
  >
  > 如果石子堆里没有石子了，则无法操作的玩家输掉游戏。
  >
  > 给你正整数 `n` ，且已知两个人都采取最优策略。如果 Alice 会赢得比赛，那么返回 `True` ，否则返回 `False` 。

- 思路：

  > 从1~i,i*i<=n尝试是否可以拿完
  >
  > 递归改动态规划

- 代码：

  ```java
  public class Code10_StoneGameIV {
  
  	// 当前的！先手，会不会赢
  	// 打表，不能发现规律
  	public static boolean winnerSquareGame1(int n) {
  		if (n == 0) {
  			return false;
  		}
  		// 当前的先手，会尝试所有的情况，1，4，9，16，25，36....
  		for (int i = 1; i * i <= n; i++) {
  			// 当前的先手，决定拿走 i * i 这个平方数
  			// 它的对手会不会赢？ winnerSquareGame1(n - i * i)
  			if (!winnerSquareGame1(n - i * i)) {
  				return true;
  			}
  		}
  		return false;
  	}
  
  	public static boolean winnerSquareGame2(int n) {
  		int[] dp = new int[n + 1];
  		dp[0] = -1;
  		return process2(n, dp);
  	}
  
  	public static boolean process2(int n, int[] dp) {
  		if (dp[n] != 0) {
  			return dp[n] == 1 ? true : false;
  		}
  		boolean ans = false;
  		for (int i = 1; i * i <= n; i++) {
  			if (!process2(n - i * i, dp)) {
  				ans = true;
  				break;
  			}
  		}
  		dp[n] = ans ? 1 : -1;
  		return ans;
  	}
  
  	public static boolean winnerSquareGame3(int n) {
  		boolean[] dp = new boolean[n + 1];
  		for (int i = 1; i <= n; i++) {
  			for (int j = 1; j * j <= i; j++) {
  				if (!dp[i - j * j]) {
  					dp[i] = true;
  					break;
  				}
  			}
  		}
  		return dp[n];
  	}
  	
  	public static void main(String[] args) {
  		int n = 10000000;
  		System.out.println(winnerSquareGame3(n));
  	}
  
  }
  ```

  

#### BusRoutes

- 链接:https://leetcode.com/problems/bus-routes/

- 内容：

  > You are given an array `routes` representing bus routes where `routes[i]` is a bus route that the `ith` bus repeats forever.
  >
  > - For example, if `routes[0] = [1, 5, 7]`, this means that the `0th` bus travels in the sequence `1 -> 5 -> 7 -> 1 -> 5 -> 7 -> 1 -> ...` forever.
  >
  > You will start at the bus stop `source` (You are not on any bus initially), and you want to go to the bus stop `target`. You can travel between bus stops by buses only.
  >
  > Return *the least number of buses you must take to travel from* `source` *to* `target`. Return `-1` if it is not possibl

- 思路：

  > 对所有的线路进行宽度优先遍历，直到找到目标或终止

- 代码：

  ```java
  public class Code11_BusRoutes {
  	// 0 : [1,3,7,0]
  	// 1 : [7,9,6,2]
  	// ....
  	// 返回：返回换乘几次+1 -> 返回一共坐了多少条线的公交。
  	public static int numBusesToDestination(int[][] routes, int source, int target) {
  		if (source == target) {
  			return 0;
  		}
  		int n = routes.length;
  		// key : 车站
  		// value : list -> 该车站拥有哪些线路！
  		HashMap<Integer, ArrayList<Integer>> map = new HashMap<>();
  		for (int i = 0; i < n; i++) {
  			for (int j = 0; j < routes[i].length; j++) {
  				if (!map.containsKey(routes[i][j])) {
  					map.put(routes[i][j], new ArrayList<>());
  				}
  				map.get(routes[i][j]).add(i);
  			}
  		}
  		ArrayList<Integer> queue = new ArrayList<>();
  		boolean[] set = new boolean[n];
  		for (int route : map.get(source)) {
  			queue.add(route);
  			set[route] = true;
  		}
  		int len = 1;
  		while (!queue.isEmpty()) {
  			ArrayList<Integer> nextLevel = new ArrayList<>();
  			for (int route : queue) {
  				int[] bus = routes[route];
  				for (int station : bus) {
  					if (station == target) {
  						return len;
  					}
  					for (int nextRoute : map.get(station)) {
  						if (!set[nextRoute]) {
  							nextLevel.add(nextRoute);
  							set[nextRoute] = true;
  						}
  					}
  				}
  			}
  			queue = nextLevel;
  			len++;
  		}
  		return -1;
  	}
  }
  ```


### class37

#### FlattenBinaryTreeToLinkedList-前置mirrors遍历

- 链接：https://leetcode.cn/problems/flatten-binary-tree-to-linked-list/description/

- 内容：

  > 给你二叉树的根结点 `root` ，请你将它展开为一个单链表：
  >
  > - 展开后的单链表应该同样使用 `TreeNode` ，其中 `right` 子指针指向链表中下一个结点，而左子指针始终为 `null` 。
  > - 展开后的单链表应该与二叉树 [**先序遍历**](https://baike.baidu.com/item/先序遍历/6442839?fr=aladdin) 顺序相同。

- 思路：

  > 二叉树递归套路
  >
  > mirrors遍历

- 代码：

  - 二叉树递归套路

    ```java
    	public static void flatten1(TreeNode root) {
    		process(root);
    	}
    	static class Help{
    		TreeNode pre;
    		TreeNode tail;
    		public Help(TreeNode p,TreeNode t){pre=p;tail=t;}
    	}
    	public static Help process(TreeNode cur){
    		if(cur == null){
    			return null;
    		}
    		Help lHelp = process(cur.left);
    		Help rHelp = process(cur.right);
    
    		cur.left = null;
    		cur.right = lHelp == null ? null : lHelp.pre;
    		TreeNode tail = lHelp == null ? cur : lHelp.tail;
    		tail.right = rHelp == null ? null : rHelp.pre;
    		tail = rHelp == null ? tail : rHelp.tail;
    		return new Help(cur,tail);
    	}
    ```

  - mirrors遍历

    - 前置知识

      ```java
      /*
      	假设当前来到节点cur，开始时cur来到头结点的位置
      	如果cur没有左孩子，cur向右移动(cur = cur.right ）
      	如果cur有左孩子，找到左子树上最右的节点mostRight：
      		a. 如果mostRight的右指针指向空，让其指向cur，然后cur向左移动（cur = cur.left）
      		b. 如果mostRight的右指针指向cur，让其指向null，然后cur向右移动（cur=cur.right）
      	cur为空遍历停止
      	*/
      
      	public void mirrors(TreeNode root){
      		if(root == null) return;
      		TreeNode cur = root;
      		TreeNode mostRight = null;
      		while (cur != null){
      			mostRight = cur.left;
      			if(mostRight != null){
      				while (mostRight.left != null && mostRight.right != cur){
      					mostRight = mostRight.left;
      				}
      				if(mostRight.right == null){
      					mostRight.right = cur;
      					cur = cur.left;
      					continue;
      				}else{
      					mostRight.right = null;
      				}
      			}
      			cur = cur.right;
      		}
      	}
      ```

    ```java
    // mirrors遍历
    	public void flatten2(TreeNode root){
    		if (root == null) {
    			return;
    		}
    		TreeNode pre = null;
    		TreeNode cur = root;
    		TreeNode mostRight = null;
    		while (cur != null) {
    			mostRight = cur.left;
    			if (mostRight != null) {
    				while (mostRight.right != null && mostRight.right != cur) {
    					mostRight = mostRight.right;
    				}
    				if (mostRight.right == null) {
    					mostRight.right = cur;
    					if (pre != null) {
    						pre.left = cur;
    					}
    					pre = cur;
    					cur = cur.left;
    					continue;
    				} else {
    					mostRight.right = null;
    				}
    			} else {
    				if (pre != null) {
    					pre.left = cur;
    				}
    				pre = cur;
    			}
    			cur = cur.right;
    		}
    		cur = root;
    		TreeNode next = null;
    		while (cur != null) {
    			next = cur.left;
    			cur.left = null;
    			cur.right = next;
    			cur = next;
    		}
    	}
    ```

#### MaximalSquare

- 链接：https://leetcode.cn/problems/maximal-square/description/

- 内容：

  > 在一个由 `'0'` 和 `'1'` 组成的二维矩阵内，找到只包含 `'1'` 的最大正方形，并返回其面积。

- 思路：

  > 动态规划：f(i,j)为以[i,j]为下标的位置为右下角，所构成的正方形最大的边长
  >
  > 则 f(m,n) = min(f(m,n-1),f(m-1,n),f(m-1,n-1)+1)
  >
  > max为f()能取到的最大值

- 代码：

  ```java
  public static int maximalSquare(char[][] m) {
  		if (m == null || m.length == 0 || m[0].length == 0) {
  			return 0;
  		}
  		int N = m.length;
  		int M = m[0].length;
  		int[][] dp = new int[N + 1][M + 1];
  		int max = 0;
  		for (int i = 0; i < N; i++) {
  			if (m[i][0] == '1') {
  				dp[i][0] = 1;
  				max = 1;
  			}
  		}
  		for (int j = 1; j < M; j++) {
  			if (m[0][j] == '1') {
  				dp[0][j] = 1;
  				max = 1;
  			}
  		}
  		for (int i = 1; i < N; i++) {
  			for (int j = 1; j < M; j++) {
  				if (m[i][j] == '1') {
  					dp[i][j] = Math.min(
  							Math.min(dp[i - 1][j],
  									dp[i][j - 1]), 
  							dp[i - 1][j - 1]) 
  							+ 1;
  					max = Math.max(max, dp[i][j]);
  				}
  			}
  		}
  		return max * max;
  	}
  ```

#### InvertBinaryTree

- 链接：https://leetcode.cn/problems/invert-binary-tree/description/

- 内容：

  > 给你一棵二叉树的根节点 `root` ，翻转这棵二叉树，并返回其根节点。

- 思路：

  > 递归反转

- 代码：

  ```java
  	public static TreeNode invertTree(TreeNode root) {
  		if (root == null) {
  			return null;
  		}
  		TreeNode left = root.left;
  		root.left = invertTree(root.right);
  		root.right = invertTree(left);
  		return root;
  	}
  ```

  

#### HouseRobberIII

- 链接：https://leetcode.cn/problems/house-robber-iii/description/

- 内容：

  > 小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为 `root` 。
  >
  > 除了 `root` 之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果 **两个直接相连的房子在同一天晚上被打劫** ，房屋将自动报警。
  >
  > 给定二叉树的 `root` 。返回 ***在不触动警报的情况下** ，小偷能够盗取的最高金额* 。

- 思路：

  > 二叉树的递归套路
  >
  >    与获取员工最大happy值一样

- 代码：

  ```java
  public static int rob(TreeNode root) {
  		Info info = process(root);
  		return Math.max(info.no, info.yes);
  	}
  
  	public static class Info {
  		public int no;
  		public int yes;
  
  		public Info(int n, int y) {
  			no = n;
  			yes = y;
  		}
  	}
  
  	public static Info process(TreeNode x) {
  		if (x == null) {
  			return new Info(0, 0);
  		}
  		Info leftInfo = process(x.left);
  		Info rightInfo = process(x.right);
  		int no = Math.max(leftInfo.no, leftInfo.yes) + Math.max(rightInfo.no, rightInfo.yes);
  		int yes = x.val + leftInfo.no + rightInfo.no;
  		return new Info(no, yes);
  	}
  ```

  

#### DecodeString

- 链接：https://leetcode.cn/problems/decode-string/description/

- 内容：

  > 给定一个经过编码的字符串，返回它解码后的字符串。
  >
  > 编码规则为: `k[encoded_string]`，表示其中方括号内部的 `encoded_string` 正好重复 `k` 次。注意 `k` 保证为正整数。
  >
  > 你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。
  >
  > 此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 `k` ，例如不会出现像 `3a` 或 `2[4]` 的输入

- 思路：

  > 与class36的ComputeExpressionValue类似，都是递归调用。
  >
  > 不同的是上面返回的是同一类型，可以用数组，另外一个只能使用抽象对象。

- 代码：

  ```java
  public static String decodeString(String s) {
  		char[] str = s.toCharArray();
  		return process(str, 0).ans;
  	}
  	public static class Info {
  		public String ans;
  		public int stop;
  
  		public Info(String a, int e) {
  			ans = a;
  			stop = e;
  		}
  	}
  
  	// s[i....]  何时停？遇到   ']'  或者遇到 s的终止位置，停止
  	// 返回Info
  	// 0) 串
  	// 1) 算到了哪
  	public static Info process(char[] s, int i) {
  		StringBuilder ans = new StringBuilder();
  		int count = 0;
  		while(i < s.length && s[i] != ']'){
  			if((s[i] >= 'a' && s[i] <= 'z') || (s[i] >= 'A' && s[i] <= 'Z')){
  				ans.append(s[i++]);
  			}else if(s[i] >= '0' && s[i] <= '9'){
  				count = count*10 + s[i++] - '0';
  			}else{
  				Info next = process(s, i + 1);
  				ans.append(timesString(count,next.ans));
  				count = 0;
  				i = next.stop + 1;
  			}
  		}
  		return new Info(ans.toString(),i);
  	}
  
  	public static String timesString(int times, String str) {
  		StringBuilder ans = new StringBuilder();
  		for (int i = 0; i < times; i++) {
  			ans.append(str);
  		}
  		return ans.toString();
  	}
  ```

  

#### QueueReconstructionByHeight-前置SBT

- 链接：https://leetcode.cn/problems/queue-reconstruction-by-height/description/

- 内容：

  > 假设有打乱顺序的一群人站成一个队列，数组 `people` 表示队列中一些人的属性（不一定按顺序）。每个 `people[i] = [hi, ki]` 表示第 `i` 个人的身高为 `hi` ，前面 **正好** 有 `ki` 个身高大于或等于 `hi` 的人。
  >
  > 请你重新构造并返回输入数组 `people` 所表示的队列。返回的队列应该格式化为数组 `queue` ，其中 `queue[j] = [hj, kj]` 是队列中第 `j` 个人的属性（`queue[0]` 是排在队列前面的人）。
  >
  > example:
  >
  > ```
  > 输入：people = [[7,0],[4,4],[7,1],[5,0],[6,1],[5,2]]
  > 输出：[[5,0],[7,0],[5,2],[6,1],[4,4],[7,1]]
  > ```

- 思路：

  > 排序 以h从小到大，k从大到小排序（同值h的k是从大到小的），再逆序取出
  >
  > SB树

- 代码：

  ```java
  	public static int[][] reconstructQueue1(int[][] people) {
  		int N = people.length;
  		Unit[] units = new Unit[N];
  		for (int i = 0; i < N; i++) {
  			units[i] = new Unit(people[i][0], people[i][1]);
  		}
  		Arrays.sort(units, new UnitComparator());
  		ArrayList<Unit> arrList = new ArrayList<>();
  		for (Unit unit : units) {
  			arrList.add(unit.k, unit);
  		}
  		int[][] ans = new int[N][2];
  		int index = 0;
  		for (Unit unit : arrList) {
  			ans[index][0] = unit.h;
  			ans[index++][1] = unit.k;
  		}
  		return ans;
  	}
  
  	public static class Unit {
  		public int h;
  		public int k;
  
  		public Unit(int height, int greater) {
  			h = height;
  			k = greater;
  		}
  	}
  
  	public static class UnitComparator implements Comparator<Unit> {
  
  		@Override
  		public int compare(Unit o1, Unit o2) {
  			return o1.h != o2.h ? (o2.h - o1.h) : (o1.k - o2.k);
  		}
  
  	}
  ```

  

#### PathSumIII

- 链接：https://leetcode.cn/problems/path-sum-iii/description/

- 内容：

  > 给定一个二叉树的根节点 `root` ，和一个整数 `targetSum` ，求该二叉树里节点值之和等于 `targetSum` 的 **路径** 的数目。
  >
  > **路径** 不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

- 思路：

  > 利用前缀和及map存储前缀和及其数目

  ![](img/cfgo_37_7.png)

- 代码：

  ```java
  public static int pathSum(TreeNode root, int sum) {
  		HashMap<Long, Integer> preSumMap = new HashMap<>();
  		preSumMap.put(0L, 1);
  		return process(root, sum, 0, preSumMap);
  	}
  
  	// 返回方法数
  	public static int process(TreeNode x, int sum, long preAll, HashMap<Long, Integer> preSumMap) {
  		if (x == null) {
  			return 0;
  		}
  		long all = preAll + x.val;
  		int ans = 0;
  		if (preSumMap.containsKey(all - sum)) {
  			ans = preSumMap.get(all - sum);
  		}
  		if (!preSumMap.containsKey(all)) {
  			preSumMap.put(all, 1);
  		} else {
  			preSumMap.put(all, preSumMap.get(all) + 1);
  		}
  		ans += process(x.left, sum, all, preSumMap);
  		ans += process(x.right, sum, all, preSumMap);
  		if (preSumMap.get(all) == 1) {
  			preSumMap.remove(all);
  		} else {
  			preSumMap.put(all, preSumMap.get(all) - 1);
  		}
  		return ans;
  	}
  ```

#### DayCount-前置拓扑排序

- 链接：网易

- 内容：

  > 刚入职网易互娱，新人mini项目便如火如荼的开展起来。为了更好的项目协作与管理，小易决定将学到的甘特图知识用于mini项目时间预估。小易先把项目中每一项工作以任务的形式列举出来，每项任务有一个预计花费时间与前置任务表，必须完成了该任务的前置任务才能着手去做该任务。
  >  作为经验PM，小易把任务划分得井井有条，保证没有前置任务或者前置任务全数完成的任务，都可以同时进行。
  >
  > 小易给出了这样一个任务表，请作为程序的你计算需要至少多长时间才能完成所有任务。
  >  输入第一行为一个正整数T，表示数据组数。
  >  对于接下来每组数据，第一行为一个正整数N，表示一共有N项任务。
  >  接下来N行，每行先有两个整数Di和Ki，表示完成第i个任务的预计花费时间为Di天，该任务有Ki个前置任务。之后为Ki个整数Mj，表示第Mj个任务是第i个任务的前置任务。
  >  数据范围：对于所有数据，满足1<=T<=3, 1<=N, Mj<=100000, 0<=Di<=1000, 0<=sum(Ki)<=N*2。

- 思路：

  > 拓扑排序

- 代码：

  ```java
  public static int dayCount(ArrayList<Integer>[] nums, int[] days, int[] headCount) {
  		Queue<Integer> head = countHead(headCount);
  		int maxDay = 0;
  		int[] countDay = new int[days.length];
  		while (!head.isEmpty()) {
  			int cur = head.poll();
  			countDay[cur] += days[cur];
  			for (int j = 0; j < nums[cur].size(); j++) {
  				headCount[nums[cur].get(j)]--;
  				if (headCount[nums[cur].get(j)] == 0) {
  					head.offer(nums[cur].get(j));
  				}
  				countDay[nums[cur].get(j)] = Math.max(countDay[nums[cur].get(j)], countDay[cur]);
  			}
  		}
  		for (int i = 0; i < countDay.length; i++) {
  			maxDay = Math.max(maxDay, countDay[i]);
  		}
  		return maxDay;
  	}
  
  	private static Queue<Integer> countHead(int[] headCount) {
  		Queue<Integer> queue = new LinkedList<>();
  		for (int i = 0; i < headCount.length; i++) {
  			if (headCount[i] == 0)
  				queue.offer(i); // 没有前驱任务
  		}
  		return queue;
  	} 
  ```

  

#### GameForEveryStepWin

- 链接： 字节

- 内容：

  >
  > 扑克牌中的红桃J和梅花Q找不到了，为了利用剩下的牌做游戏，小明设计了新的游戏规则
  >
  >  1) A,2,3,4....10,J,Q,K分别对应1到13这些数字，大小王对应0
  >  2) 游戏人数为2人，轮流从牌堆里摸牌，每次摸到的牌只有“保留”和“使用”两个选项，且当前轮必须做出选择
  >  3) 如果选择“保留”当前牌，那么当前牌的分数加到总分里，并且可以一直持续到游戏结束
  >  4) 如果选择“使用”当前牌，那么当前牌的分数*3，加到总分上去，但是只有当前轮，下一轮，下下轮生效，之后轮效果消失。
  >  5) 每一轮总分大的人获胜
  >  假设小明知道每一轮对手做出选择之后的总分，返回小明在每一轮都赢的情况下，最终的最大分是多少
  >     如果小明怎么都无法保证每一轮都赢，返回-1

- 思路：

  > 递归 可改成动态规划的记忆化搜索方法

- 代码：

  ```java
  	// 当前来到index位置，牌是cands[index]值
  	// 对手第i轮的得分，sroces[i]
  	// int hold : i之前保留的牌的总分
  	// int cur : 当前轮得到的，之前的牌只算上使用的效果，加成是多少
  	// int next : 之前的牌，对index的下一轮，使用效果加成是多少
  	// 返回值：如果i...最后，不能全赢，返回-1
  	// 如果i...最后，能全赢，返回最后一轮的最大值
  	
  	// index -> 26种
  	// hold -> (1+2+3+..13) -> 91 -> 91 * 4 - (11 + 12) -> 341
  	// cur -> 26
  	// next -> 13
  	// 26 * 341 * 26 * 13 -> ? * (10 ^ 5)
  	public static int f(int[] cands, int[] sroces, int index, int hold, int cur, int next) {
  		if (index == 25) { // 最后一张
  			int all = hold + cur + cands[index] * 3;
  			if (all <= sroces[index]) {
  				return -1;
  			}
  			return all;
  		}
  		// 不仅最后一张
  		// 保留
  		int all1 = hold + cur + cands[index];
  		int p1 = -1;
  		if (all1 > sroces[index]) {
  			p1 = f(cands, sroces, index + 1, hold + cands[index], next, 0);
  		}
  		// 爆发
  		int all2 = hold + cur + cands[index] * 3;
  		int p2 = -1;
  		if (all2 > sroces[index]) {
  			p2 = f(cands, sroces, index + 1, hold, next + cands[index] * 3, cands[index] * 3);
  		}
  		return Math.max(p1, p2);
  	}
  
  	// 26 * 341 * 78 * 39 = 2 * (10 ^ 7)
  	public static int process(int[] cards, int[] scores, int index, int hold, int cur, int next) {
  		if (index == 25) {
  			int all = hold + cur + cards[index] * 3;
  			if (all > scores[index]) {
  				return all;
  			} else {
  				return -1;
  			}
  		} else {
  			int d1 = hold + cur + cards[index];
  			int p1 = -1;
  			if (d1 > scores[index]) {
  				p1 = process(cards, scores, index + 1, hold + cards[index], next, 0);
  			}
  			int d2 = hold + cur + cards[index] * 3;
  			int p2 = -1;
  			if (d2 > scores[index]) {
  				p2 = process(cards, scores, index + 1, hold, next + cards[index] * 3, cards[index] * 3);
  			}
  			return Math.max(p1, p2);
  		}
  	}
  	
  	
  	
  	// cur -> 牌点数    ->  * 3 之后是效果
  	// next -> 牌点数   ->  * 3之后是效果
  	public static int p(int[] cands, int[] sroces, int index, int hold, int cur, int next) {
  		if (index == 25) { // 最后一张
  			int all = hold + cur * 3 + cands[index] * 3;
  			if (all <= sroces[index]) {
  				return -1;
  			}
  			return all;
  		}
  		// 不仅最后一张
  		// 保留
  		int all1 = hold + cur * 3 + cands[index];
  		int p1 = -1;
  		if (all1 > sroces[index]) {
  			p1 = f(cands, sroces, index + 1, hold + cands[index], next, 0);
  		}
  		// 爆发
  		int all2 = hold + cur * 3 + cands[index] * 3;
  		int p2 = -1;
  		if (all2 > sroces[index]) {
  			p2 = f(cands, sroces, index + 1, hold, next + cands[index], cands[index]);
  		}
  		return Math.max(p1, p2);
  	}
  	
  	// 改出动态规划，记忆化搜索！
  ```

  
