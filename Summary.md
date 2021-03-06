# Summary of [POJ](http://poj.org/problemlist) solutions
Recording according to [problem category](https://blog.csdn.net/lyy289065406/article/details/78702485)
## 基本算法
### 高精度算法
#### 1. [1503 Integer Inquiry](http://poj.org/problem?id=1503) / [Solution](https://github.com/HzhElena/POJ_solution/blob/master/POJ%201503.cpp)
> 求多个正数大数相加和

* 使用数组和 len 逆序表示各数，逐个相加
#### 2. [2109 Power of Cryptography](http://poj.org/problem?id=2109) / [Solution](https://github.com/HzhElena/POJ_solution/blob/master/POJ%202109(Math).cpp)

> For all such pairs 1<=n<= 200, 1<=p<10101 and there exists an integer k, 1<=k<=109 such that k^n = p. 求 k

* **[公式法]((https://github.com/HzhElena/POJ_solution/blob/master/POJ%202109(Math).cpp)):**  由于 C++ 中 double 范围有
类型          长度 (bit)           有效数字          绝对值范围
float             32                      6~7                  10^(-37) ~ 10^38

double          64                     15~16               10^(-307) ~10^308

long double   128                   18~19                10^(-4931) ~ 10 ^ 4932

可以直接用pow(n,1/p)  求 k.
* **[高精度二分法](https://github.com/HzhElena/POJ_solution/blob/master/POJ%202109(Math2).cpp)** 仍然需要使用到 double，采用二分查找 k . 
#### 3. [2389 Bull Math](http://poj.org/problem?id=2389) / [Solution](https://github.com/HzhElena/POJ_solution/blob/master/POJ%202389.cpp)
> 计算两大数乘积

* 可以先乘后计算进位
* res[pa+pb] += a[pa] * b[pb]

#### 4.[2602 Superlong sums](http://poj.org/problem?id=2602) / [Solution](https://github.com/HzhElena/POJ_solution/blob/master/POJ%202602.cpp)
> find the sum of two numbers with maximal size of 1.000.000 digits.
Output file should contain exactly N digits in a single line representing the sum of these two integers.

* 使用 4 位数字作为数组中的元素时，由于会自动进位，导致错误。(输出要求与输入位数相同)
* 使用 int 存储数组，在读数以及输出时会超时。
* 应该采用 char 存储数字。 if(num[i] >'9') num[i]-= 10; num[i-1] += 1 进行该运算以进位。整数的 %= 和 /= 需要 时间多，不可用。

#### 5. [3982 序列](http://poj.org/problem?id=3982) / [Solution](https://github.com/HzhElena/POJ_solution/blob/master/POJ%203982.cpp)
> 数列A满足An = An-1 + An-2 + An-3, n >= 3 . 编写程序，给定A0, A1 和 A2, 计算A99

* 由于需要覆盖原来的值，使用数组比较复杂(清零问题)。可以直接用 char* 设置\0 为结尾标志。同时计算sum时，可以直接赋值。
* 定义 add(char *a,char *b,char *c,char *ans)

* 第一次计算 ans 为 A3。循环计算 25 次,即可在 ans 中得到 A99
### 枚举
#### 1. [1753 Flip Game](http://poj.org/problem?id=1753) / [Solution](https://github.com/HzhElena/OJ/blob/master/POJ%201753(%E6%9E%9A%E4%B8%BE).cpp)
* 使用递归从反转0个棋子到1,2,...,16个逐步查找，如果可以达到目标状态则立刻返回步数。
* 使用 int 表示状态
* 最多 2^16 状态，因此可以使用枚举法
* 使用 [BFS](https://github.com/HzhElena/OJ/blob/master/POJ%202965(BFS).py) pre 指针记录路径会导致超时
#### 1. [2965 The Pilots Brothers' refrigerator](http://poj.org/problem?id=2965) / [Solution](https://github.com/HzhElena/OJ/blob/master/POJ%202965(%E6%9E%9A%E4%B8%BE).cpp)
> 一个冰箱有4*4矩阵排列的一共16个把手(handles)，每个把手只有'+'(关)和'-'(开)两种状态，当且仅当开关全部为'-',也即冰箱把手都为开启状态的时候冰箱才能被打开。搬动冰箱把手定义一种翻转，即：每次随机选取一个把手翻动，则其所在行和所在列的一共7个把手全部翻转。现在给出16个把手的初始状态（至少有一个把手为'+'），求至少翻动多少轮次，才能够把冰箱门打开，也即把手状态全部为'-'。
输出：达到冰箱开启，即全部把手状态为'-'的最小轮次。首行输出轮次，以下每行输出按次翻动的把手的行号和列号（之间用随意多个空格隔开即可）。

* 使用递归从反转0个门把手到1,2,...,16个逐步查找，如果可以达到目标状态则立刻返回步数。
* 使用 int 表示状态
* 最多 2^16 状态，因此可以使用枚举法。使用枚举法记录转动的把手行号和列号更加方便。
### 构造法
#### 1. [3239 Solution to the n Queens Puzzle](http://poj.org/problem?id=3239) / [Solution](https://github.com/HzhElena/OJ/blob/master/POJ%203239(%E6%9E%84%E9%80%A0).cpp)
由于n数值很大，不可以用回溯法。回溯法至多可以解决 n = 25 的问题。

一、当n mod 6 != 2 或 n mod 6 != 3时：
* (A1):[2,4,6,8,...,m], [1,3,5,7,...,m-1]            (m为偶) 
* (A2):[2,4,6,8,...,m-1], [1,3,5,7,...,m-2], [m]     (m为奇)

二、当n mod 6 == 2 或 n mod 6 == 3时
(当n为偶数,k=n/2；当n为奇数,k=(n-1)/2)

* (B1):[n,n+2,n+4,...,m], [2,4,...,n-2], [n+3,n+5,...,m-1], [1,3,5,...,n+1]        (m为偶,n为偶) 
* (B2):[n,n+2,n+4,...,m-1], [1,3,5,...,n-2], [n+3,...,m], [2,4,...,n+1]            (m为偶,n为奇) 
* (B3):[n,n+2,n+4,...,m-1], [2,4,...,n-2], [n+3,n+5,...,m-2], [1,3,5,...,n+1], [m] (m为奇,n为偶) 
* (B4):[n,n+2,n+4,...,m-2], [1,3,5,...,n-2], [n+3,...,m-1], [2,4,...,n+1], [m]     (m为奇,n为奇) 

(上面有六条序列。一行一个序列，中括号是我额外加上的，方便大家辨认子序列，子序列与子序列之间是连续关系，无视中括号就可以了。第i个数为ai，表示在第i行ai列放一个皇后；... 省略的序列中，相邻两数以2递增。)

### 贪心
#### 1. [1328 Radar Installation](http://poj.org/problem?id=1328) / [Solution](https://github.com/HzhElena/OJ/blob/master/POJ%201328(%E8%B4%AA%E5%BF%83).py)
* 错误的做法：考虑最左边的一个岛屿A，要用一个雷达去覆盖它，又要使得之后的岛屿会尽可能的都在这个雷达的范围里，那么雷达在覆盖A的条件下越往左放置越好，即A刚好在雷达扫描的边界上为最优，我们可以以此来求出雷达的坐标，然后判断继A之后有哪些岛屿在刚刚放置的雷达范围之中，若在便从队列中除去，若不在便以此岛屿再次执行与A一样的操作（即找下一个雷达的布置位置）。 后来发现这种做法是错误的，在放置第一个雷达时，在满足覆盖A的同时，并不是越往右放置越好，因为当雷达往右挪动时，会将不再覆盖左侧的一部分（如图阴影部分），此时B点将需要另外添加一个雷达来覆盖，故这种思路是错误的！
* 将所有的岛屿对应的这段区间记录下来，然后以区间左界从小到大排序就行，之后从第一个区间开始，如果第二个区间与其有交集，就更新这个交集，并从队列中除去区间1，2，如果第三个区间与这个交集又有交集，那么便更新交集并除去区间3直到不满足有交集为止。然后继续模拟这个过程就行了，每模拟以此这个过程ANS++（即区间选点问题）
## 动态规划
#### 最长递增序列(LIS)【模板】
> 给出一个数列，找出其中最长的单调递减（或递增）子序列。
例如，{10，22，9，33，21，50，41，60，80} 
LIS的长度是6和 LIS为{10，22，33，50，60，80}。

* [方法一](https://github.com/HzhElena/POJ_solution/blob/master/LIS_2.cpp): O(n^2) 对每一个A[N]中的元素都计算以他们各自结尾的最大递增子序列的长度，这些长度的最大值，就是我们要求的问题——数组A的最大递增子序列。
* [方法二](https://github.com/HzhElena/POJ_solution/blob/master/LIS.cpp): O(nlog n) 不仅可以得到最长序列长度，还可以得到最长子序列。维护单调递增栈，遍历数组。如果当前数大于栈顶，则加入栈。否则通过二分查找得到low 位置，将该位置栈中值设为当前值。不增加元素，仅改变栈数值。
#### 1. [1836 Alignment](http://poj.org/problem?id=1836) / [Solution](https://github.com/HzhElena/POJ_solution/blob/master/POJ%201836(LIS).cpp)
> 求删除最少的数，使得从序列中任取一个数h[i]，有h[1] ~ h[i]严格单增，或h[i] ~ h[n]严格单减.
* **分析**: 分别从左向右，从右向左求LIS，然后枚举最长合法序列in = LIS_left + LIS_right，则n－in就是最少需要删除的数
* 求最长递增序列可以用以上两种方法。记录以 i 结尾序列(可以不包括 i )的最长合法序列长度。

#### 2. [1837 Balance](http://poj.org/problem?id=1837) / [Solution](https://github.com/HzhElena/POJ_solution/blob/master/POJ%201837(DP).cpp)
> 给c（2<=c<=20）个挂钩，g（2<=g<=20）个砝码，求在将所有砝码（砝码重1~25）挂到天平(天平长  -15~15)上，并使得天平平衡的方法数.

* 将g个挂钩挂上的极限值：15 * 25 * 20==7500.在有负数的情况下是-7500\~7500. 以0为平衡点,可以将平衡点往右移7500个单位，范围就是0\~15000.在有负数的以及要装入数组处理的题目中，我们都可以尝试着平移简化问题.
* 每一各砝码均只可使用一次，为0/1背包问题
* 首先我们先要明确dp数组的作用，dp[i][j]中，i为放置的砝码数量，j为平衡状态，0为平衡,j<0左倾，j>0右倾，由于j作为下标不能是负数，所以我们要找一个新的平衡点，因为15 * 20 * 20 = 7500，所以平衡点设置为7500。
* 可以得出动态方程 dp[i][j+w[i]*c[k])+=dp[i-1][j];
#### 3. [1276 Cash Machine](http://poj.org/problem?id=1276) / [Solution](https://github.com/HzhElena/POJ_solution/blob/master/POJ%201276(DP).cpp)
> 给出一个值cash，然后给出n，代表n个方案，接着n对代表个数与价值，要求使用硬币和最接近sum，但不超过sum的价值

* 典型的多重背包问题，按照模板写即可。
* 此时cost和weight 均为 硬币值。
#### 4. [3267 The Cow Lexicon](http://poj.org/problem?id=3267) / [Solution](https://github.com/HzhElena/POJ_solution/blob/master/POJ%203267(DP).cpp)
> 给出一个长度为l的文本和一个由n个单词组成的字典。求至少从文本中去掉多少个字符才能使得这个文本全部由字典中的单词组成。

* 思路: 转移方程为dp[i]=min(dp[i-1]+1,dp[pos+1]+i-pos-1-tmp);   其中dp[i]为前i个字符中需要去掉的字符数量。
* 考虑每一个位置上向前匹配每一个字典中词所需要去掉字符的个数。
* 注意字符串下标和动态规划循环下标+1的关系

#### 5. [1159 Palindrome](http://poj.org/problem?id=1159) / [Solution](https://github.com/HzhElena/POJ_solution/blob/master/POJ%201159(DP).cpp)
> 给定字符串，求将该字符串变成回文串最小需要插入字符数

* 求解思路: 构造该字符串的逆字符串，求两者最长公共子串。字符串长度-最长公共子串长度 为结果。
* 相当于求该字符串的子回文串最大长度。
* 错误：直接用dp 求字符串的 子回文串长度 WA dp[i][j] = max(dp[i+1][j-1]+2,dp[i][j]) (a[i] == b[j]) 
* 正确：dp[i][j] = max(dp[i][j],dp[i-1][j-1]+1) (a[i] == b[j])
        dp[i][j] = max(dp[i][j],dp[i-1][j])
        dp[i][j] = max(dp[i][j],dp[i][j-1])
### [背包问题](https://blog.csdn.net/stack_queue/article/details/53544109)
#### 0/1 背包问题
> 有N件物品和一个容量为V的背包。第i件物品的费用是c[i]，价值是w[i]。求解将哪些物品装入背包可使价值总和最大.
这是最基础的背包问题，特点是：每种物品仅有一件，可以选择放或不放

用子问题定义状态：即f[i][v]表示前i件物品恰放入一个容量为v的背包可以获得的最大价值。则其状态转移方程便是：

f[i][v]=max{f[i-1][v],f[i-1][v-c[i]]+w[i]}
* 优化空间复杂度

以上方法的时间和空间复杂度均为O(N*V)，其中时间复杂度基本已经不能再优化了，但空间复杂度却可以优化到O(V)。

先考虑上面讲的基本思路如何实现，肯定是有一个主循环i=1..N，每次算出来二维数组f[i][0..V]的所有值。那么，如果只用一个数组f[0..V]，能不能保证第i次循环结束后f[v]中表示的就是我们定义的状态f[i][v]呢？f[i][v]是由f[i-1][v]和f[i-1][v-c[i]]两个子问题递推而来，能否保证在推f[i][v]时（也即在第i次主循环中推f[v]时）能够得到f[i-1][v]和f[i-1][v-c[i]]的值呢？事实上，这要求在每次主循环中我们以v=V..0的顺序推f[v]，这样才能保证推f[v]时f[v-c[i]]保存的是状态f[i-1][v-c[i]]的值。伪代码如下：
```+python
for i=1..N
    for v=V..0
        f[v]=max{f[v],f[v-c[i]]+w[i]};
def ZeroOnePack(F, C, W)
     for v ← V to C
     F[v] ← max(F[v], f[v − C] + W)
F[0..V ] ←0
for i ← 1 to N
ZeroOnePack(F, Ci, Wi)
```
针对不同题目要求，f初始值不同
* 如果要求背包恰好装满，那么此时只有容量为0的背包可能被价值为0的nothing“恰好装满”，其它容量的背包均没有合法的解，属于未定义的状态，它们的值就都应该是-∞了
* 如果背包并非必须被装满，那么任何容量的背包都有一个合法解“什么都不装”，这个解的价值为0，所以初始时状态的值也就全部为0了。
#### 完全背包问题
> 有N种物品和一个容量为V的背包，每种物品都有无限件可用。第i种物品的费用是c[i]，价值是w[i]。求解将哪些物品装入背包可使这些物品的费用总和不超过背包容量，且价值总和最大。


这个问题非常类似于01背包问题，所不同的是每种物品有无限件。也就是从每种物品的角度考虑，与它相关的策略已并非取或不取两种，而是有取0件、取1件、取2件……等很多种。如果仍然按照解01背包时的思路，令f[i][v]表示前i种物品恰放入一个容量为v的背包的最大权值。
仍然可以按照每种物品不同的策略写出状态转移方程，像这样：
```+python
f[i][v]=max{f[i-1][v-k*c[i]]+k*w[i]|0<=k*c[i]<=v}
```
这跟01背包问题一样有O(N*V)个状态需要求解，但求解每个状态的时间已经不是常数了，求解状态f[i][v]的时间是O(v/c[i])，总的复杂度是超过O(VN)的。
针对背包问题而言，比较不错的一种方法是：首先将费用大于V的物品去掉，然后使用类似计数排序的做法，计算出费用相同的物品中价值最高的是哪个，可以O(V+N)地完成这个优化.
* 最优化的算法
```+python
for i=1..N
    for v=0..V
        f[v]=max{f[v],f[v-cost]+weight}
```
在考虑“加选一件第i种物品”这种策略时，需要一个可能已选入第i种物品的子结果f[i][v-c[i]]，所以就可以并且必须采用v=0..V的顺序循环。
这个算法也可以以另外的思路得出。例如，基本思路中的状态转移方程可以等价地变形成这种形式：
```+python
f[i][v]=max{f[i-1][v],f[i][v-c[i]]+w[i]}

def CompletePack(F, C, W)
    for v ← C to V
    F[v] ← max{F[v], f[v − C] + W}

```
将这个方程用一维数组实现，便得到了上面的伪代码。
#### 多重背包问题
> 有N种物品和一个容量为V的背包。第i种物品最多有n[i]件可用，每件费用是c[i]，价值是w[i]。求解将哪些物品装入背包可使这些物品的费用总和不超过背包容量，且价值总和最大。

令f[i][v]表示前i种物品恰放入一个容量为v的背包的最大权值，则有状态转移方程：
```+python
f[i][v]=max{f[i-1][v-k*c[i]]+k*w[i]|0<=k<=n[i]}
```
复杂度是O(V*Σn[i])。
* 转化为01背包问题
将第i种物品分成若干件01背包中的物品，其中每件物品有一个系数。这件物品的费用和价值均是原来的费用和价值乘以这个系数。令这些系数分别为1，2，4...
```+python
def MultiplePack(F,C,W,M)
    if C · M ≥ V
        CompletePack(F,C,W)
        return
    k ← 1
    while k < M
        ZeroOnePack(kC,kW)
        M ←M − k
        k ← 2k
    ZeroOnePack(C · M,W · M)
```
* 当问题是“每种有若干件的物品能否填满给定容量的背包”，只须考虑填满背包的可行性，不需考虑每件物品的价值时，多重背包问题同样有O(V N)复杂度的算法.

设F[i, j]表示“用了前i种物品填满容量为j的背包后，最多还剩下几个第i种物品可用”，如果F[i, j] = −1则说明这种状态不可行，若可行应满足0 ≤ F[i, j] ≤ Mi
```+python
F[0, 1 . . . V ] ← −1
F[0, 0] ← 0
for i ← 1 to N
    for j ← 0 to V
        if F[i − 1][j] ≥ 0
            F[i][j] = Mi
        else
            F[i][j] = −1
    for j ← 0 to V − Ci
        if F[i][j] > 0
            F[i][j + Ci] ← max{F[i][j + Ci], F[i][j] − 1}
 ```
#### 混合三种背包问题
有的物品只可以取一次（01背包），有的物品可以取无限次（完全背包），有的物品可以取的次数有一个上限（多重背包）。
* 01背包与完全背包的混合
考虑到01背包和完全背包中给出的伪代码只有一处不同，故如果只有两类物品：一类物品只能取一次，另一类物品可以取无限次，那么只需在对每个物品应用转移方程时，根据物品的类别选用顺序或逆序的循环即可，复杂度是O(V N)。
```+python
for i ← 1 to N
if 第i件物品属于01背包
    for v ← V to Ci
        F[v] ← max(F[v], F[v − Ci] + Wi)
else if 第i件物品属于完全背包
    for v ← Ci to V
        F[v] ← max(F[v], F[v − Ci] + Wi)
else if 第i件物品属于多重背包
    MultiplePack(F,Ci,Wi,Ni)
```
#### 二维费用的背包问题
> 二维费用的背包问题是指：对于每件物品，具有两种不同的费用，选择这
件物品必须同时付出这两种费用。对于每种费用都有一个可付出的最大值（背
包容量）。问怎样选择物品可以得到最大的价值。
设第i件物品所需的两种费用分别为Ci和Di。两种费用可付出的最大值
（也即两种背包容量）分别为V 和U。物品的价值为W

费用加了一维，只需状态也加一维即可。设F[i, v, u]表示前i件物品付出两
种费用分别为v和u时可获得的最大价值。状态转移方程就是：
```+python
F[i, v, u] = max{F[i − 1, v, u], F[i − 1, v − Ci, u − Di] + Wi}
```
当每件物品只可以取一次时变量v和u采用逆序的循环，当物品有如完全背包问题时采用顺序的循环，当物品有如多重背包问题时拆分物品.
* 物品总个数的限制
有时，“二维费用”的条件是以这样一种隐含的方式给出的：最多只能
取U件物品。这事实上相当于每件物品多了一种“件数”的费用，每个物品的
件数费用均为1，可以付出的最大件数费用为U。换句话说，设F[v, u]表示付
出费用v、最多选u件时可得到的最大价值，则根据物品的类型（01、完全、多
重）用不同的方法循环更新，最后在f[0 . . . V, 0 . . . U]范围内寻找答案

####  分组的背包问题
> 有N件物品和一个容量为V 的背包。第i件物品的费用是Ci，价值是Wi。这
些物品被划分为K组，每组中的物品互相冲突，最多选一件。求解将哪些物品
装入背包可使这些物品的费用总和不超过背包容量，且价值总和最大

这个问题变成了每组物品有若干种策略：是选择本组的某一件，还是一
件都不选。也就是说设F[k, v]表示前k组物品花费费用v能取得的最大权值，则
有：
```+python
F[k, v] = max{F[k − 1, v], F[k − 1, v − Ci] + Wi| item i ∈ group k}
```
使用一维数组的伪代码如下：
```+python
for k ← 1 to K
    for v ← V to 0
        for all item i in group k
            F[v] ← max{F[v], F[v − Ci] + Wi}
```
这里三层循环的顺序保证了每一组内的物品最多只有一个会被添加到背包中

#### 输出方案
* 一般而言，背包问题是要求一个最优值，如果要求输出这个最优值的方
案，可以参照一般动态规划问题输出方案的方法：记录下每个状态的最优值是
由状态转移方程的哪一项推出来的，换句话说，记录下它是由哪一个策略推出
来的。便可根据这条策略找到上一个状态，从上一个状态接着向前推即可。

还是以01背包为例，方程为F[i, v] = max{F[i−1, v], F[i−1, v−Ci]+Wi}。
再用一个数组G[i, v]，设G[i, v] = 0表示推出F[i, v]的值时是采用了方程的前一
项（也即F[i, v] = F[i − 1, v]），G[i, v] = 1表示采用了方程的后一项。注意这
两项分别表示了两种策略：未选第i个物品及选了第i个物品。那么输出方案的
伪代码可以这样写（设最终状态为F[N, V ]）：
```+python
i ←N
v ← V
while i > 0
    if G[i, v] = 0
        print 未选第i项物品
    else if G[i, v] = 1
        print 选了第i项物品
    v ← sv − Ci
    i ← i − 1
```
采用方程的前一项或后一项也可以在输出方案的过程中根据F[i, v]的值实时地求出来。也即，不须纪录G数组，将上述代码中的G[i, v] = 0改成F[i, v] =
F[i − 1, v]，G[i, v] = 1改成F[i, v] = F[i − 1][v − Ci] + Wi也可
* 输出字典序最小的最优方案. 只是在输出方案时要注意，如果F[i, v] = F[i − 1, v]和F[i, v] =
F[i − 1][v − Ci] + Wi都成立，应该按照后者来输出方案.
####  求方案总数
对于一个给定了背包容量、物品费用、物品间相互关系（分组、依赖等）
的背包问题，除了再给定每个物品的价值后求可得到的最大价值外，还可以得
到装满背包或将背包装至某一指定容量的方案总数。

对于这类改变问法的问题，一般只需将状态转移方程中的max改成sum即
可。例如若每件物品均是完全背包中的物品，转移方程即为
```+python
F[i, v] = sum{F[i − 1, v], F[i, v − Ci]}
```
初始条件是F[0, 0] = 1
#### 最优方案的总数
这里的最优方案是指物品总价值最大的方案。以01背包为例。
结合求最大总价值和方案总数两个问题的思路，最优方案的总数可以这样
求：F[i, v]代表该状态的最大价值，G[i, v]表示这个子问题的最优方案的总数，
则在求F[i, v]的同时求G[i, v]的伪代码如下：
```+python
G[0, 0] ← 1
for i ← 1 to N
    for v ← 0 to V
        F[i, v] ← max{F[i − 1, v], F[i − 1, v − Ci] + Wi}
        G[i, v] ← 0
        if F[i, v] = F[i − 1, v]
            G[i, v] ← G[i, v] + G[i − 1][v]
        if F[i, v] = F[i − 1, v − Ci] + Wi
            G[i, v] ← G[i, v] + G[i − 1][v − Ci]
```
## Search
### BFS
#### 1. [1753 Flip Game](http://poj.org/problem?id=1753) / [Solution](https://github.com/HzhElena/OJ/blob/master/POJ%201753(BFS).py)
    > 有一4x4棋盘，上面有16枚双面棋子（一面为黑，一面为白）， 
     当翻动一只棋子时，该棋子上下左右相邻的棋子也会同时翻面。 
     以b代表黑面，w代表白面，给出一个棋盘状态， 
     问从该棋盘状态开始，使棋盘变成全黑或全白，至少需要翻转多少步   
* Bit operation ^= 异或操作符 使得int中某一特定位变为1 或 0。
* Use (step>16) to break loop 否则会无穷地循环下去。 
* BFS 内部每一个状态均翻转16个位。


