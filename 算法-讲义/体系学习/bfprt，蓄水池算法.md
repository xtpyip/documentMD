# bfprt，蓄水池算法

## 基本内容

- bfprt算法

  > 常规快排：
  >
  > ​	随机在数组中选择一个数作为划分值（number），然后进行快排的partation过程
  >
  > ​		将小于number的数放到数组左边
  >
  > ​		等于number的数放到数组中间
  >
  > ​		大于number的数放到数组右边
  >
  > ​	然后判断k与等于number区域的相对关系
  >
  > ​		如果k正好在等于number区域，那么数组第k小的数就是number
  >
  > ​		如果k在等于number区域的左边，那么我们递归对左边再进行上述过程
  >
  > ​		如果k在等于number区域的右边，那我们递归对右边再进行上述过程。
  >
  > 划分值的好坏严重影响了算法的好坏，虽然有使用随机数来作为划分值，但不能准确求出其时间复杂度
  >
  > bfprt算法：
  >
  > ​	求取划分值，以五个一组划分，不足五个自成一组
  >
  > ​	得到每组的中位数，以此排序后的中位数数组的中位数为划分值
  >
  > ​	此值保证了至少大于了3N/10
  >
  > ​	根据master公式
  >
  > ​	T(N) = T(N/5) + T(7N/10) +O(N) 收敛到O(N)

- 蓄水池算法 

  > 蓄水池抽样算法通过一种随机的方式从数据流中抽取样本，保持样本的随机性和公平性。
  >
  > 算法适用于以下场景：
  >
  > - 数据集大小未知或过大，无法一次性加载到内存中
  > - 需要等概率地从数据集中抽取样本。
  >
  > 算法思想：
  >
  >   从数据流中逐个读取元素，
  >
  >   当读取第i个元素时，以1/i的概率选择该元素作为样本，
  >
  >   或者以1-1/i的概率保持原有的样本。
  >
  >   这样，每个元素被选择的概率都是相等的

## 问题集合

### FindMinKth

- 链接：<a href="https://github.com/xtpyip/blog-alogrithm/blob/main/alogrithm/src/main/java/blog/wstx/class29/Code01_FindMinKth.java">测试链接</a>

- 内容：

  > 给定一个混乱数组，求这个数组中的第k小的数
  
- 思路：

  > 思路1：全体排序，取第k小，**略** O(NlogN)
  >
  > 思路2：利用大根堆（小根堆） O(NlogN)
  >
  > 思路3：改写快排（递归，迭代） O(N)
  >
  > 思路4：bfprt算法（同思路3，不过取flag值使用的是bfprt，使概率随机变成可计算）O(N) （**了解即可**）
  
- 代码：

  <details>
  <summary>大根堆</summary>
  <p> - 数组中第k小的数</p>
  <pre><code>// 利用大根堆，时间复杂度O(N*logK)
  	public static int minKth1(int[] arr, int k) {
  		PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a,b)->{return b-a;});
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
  	}</code>  </pre>
  </details>
  
  <details>
  <summary>改写快排</summary>
  <p> - 数组中第k小的数</p>
  <pre><code>// 改写快排，时间复杂度O(N)
  	// k >= 1
  	public static int minKth2(int[] array, int k) {
  		int[] arr = copyArray(array);
  		return process2(arr, 0, arr.length - 1, k - 1);
  	}
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
  	}</code>  </pre>
  </details>
  
  <details>
  <summary>bfprt</summary>
  <p> - 数组中第k小的数</p>
  <pre><code>// 利用bfprt算法，时间复杂度O(N)
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
  	}</code>  </pre>
  </details>

### MaxTopK

- 链接：<a href="https://github.com/xtpyip/blog-alogrithm/blob/main/alogrithm/src/main/java/blog/wstx/class29/Code02_MaxTopK.java">测试链接</a>

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

  <details>
  <summary>排序</summary>
  <p> - 前k个大的数字</p>
  <pre><code>// 时间复杂度O(N*logN)
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
  </code>  </pre>
  </details>

  <details>
  <summary>大根堆</summary>
  <p> - 数组中第k小的数</p>
  <pre><code>// 方法二，时间复杂度O(N + K*logN)
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
  	}</code>  </pre>
  </details>

  <details>
  <summary>bfprt</summary>
  <p> - 前k个大的数字</p>
  <pre><code>// 方法三，时间复杂度O(n + k * logk)
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
  </code>  </pre>
  </details>

### ReservoirSampling

- 链接：<a href="https://github.com/xtpyip/blog-alogrithm/blob/main/alogrithm/src/main/java/blog/wstx/class29/Code03_ReservoirSampling.java">测试链接</a>

- 内容：

  > 给定一个数据输入流，要让当前及之前的所有的数据都要以同样的概率放入袋子中
  >
  > 假设此袋子的长度为k，当前数为n，则1~n的每个数据都要以相同概率进入
  >
  > 等价于n个数据选入10个数据。

- 思路：

  > 先让前k个数据直接入袋
  >
  > 当前数据为i,以**k/i**的概率决定要不要入袋，如果不入，则进入下一个i+1数据进行判断
  >
  > 如果进入，以1/k的概率选中要进入哪个位置
  >
  > 即此数据以**k/i * 1/k**的概率要入袋，即**1/i**的概率要入袋，前1~i的数据均是如此。

- 代码：

  <details>
  <summary>对数据流采用相同概率决定存弃</summary>
  <p> - 蓄水池算法</p>
  <pre><code>public static class RandomBox {
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
  	}</code>  </pre>
  </details>
