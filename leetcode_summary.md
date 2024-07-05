#2024.5.16  

**今日主题：链表**  
常用技巧  设置一个哑节点  
、、、
ListNode* pre = new ListNode(val,head)  
、、、

**新算法：快慢指针：** 
1.通过设置一个慢指针，一个快指针，初始化快指针在慢指针前一步，慢指针一次走一步，快指针一次走两步，当他们再次相遇时，说明出现环；
2.通过设置一个慢指针和一个快指针，判断前后元素，实现数组重复元素的删除；

**买卖股票的最佳时机：**  
动态规划思想，只遍历一次数组，维护一个价格最小值和利润最大值，每次假设以prices[i]卖出，更新最大利润；  
注意：需要先更新利润最大值，再更新价格最小值；



#2024.5.21

**每日一题：**  
2769：找出最大的可达成数字，简单数学题，每次靠近两个单位，故答案为num+2*t;

#2024.5.22

**每日一题**
2225：找到输掉零场或者一场比赛的玩家，思路很简单，用哈希表记录每个玩家胜利和失败的场次，再遍历所有玩家，将符合条件的分别加入answer数组。小问题：注意数组的初始化为0，动态数组要标注维度
  
189:轮转数组：核心思想为新数组的第（i+k）%n项为原数组的第i项，复制数组：  
nums.assign(answer.begin(),answer.end());  
小问题：当需要使用动态数组的未加入的长度时，初始化时需要先规定长度。

#2024.5.25

**每日一题**
2903：找出满足差值条件的下标，通过题意用下标关系控制循环，再用值来判断条件即可，最后记得特判

122.买卖股票的最佳时机Ⅱ，因为买卖机会无限，所以所有上升趋势的利润均可获得，差值大于0加上即可

55.跳跃游戏，遍历数组，维护能跳到的最大值，若遍历的值大于了最大值，则返回false

45.跳跃游戏Ⅱ，一层循环遍历数组，一层循环遍历可跳到的地方，更新每个最小次数  
dp[i+j]=min(dp[i+j],dp[i]+1);  
小问题：发现在类中不适合用memset，最好用动态数组 vector<int> a(n,int_max);  
  
274.H指数，该题的思想为h是符合条件数目和引用次数共同的参数，所以先排序，通过从引用次数最高的开始判断，往低遍历，符合条件的数目也同时增长，当遍历到的不再大于h，就停止。

#2024.5.28
**每日一题**
2951.找出峰值：正解为从1~n-1遍历一次数组，当元素同时大于两端元素时，即为峰值。刚开始想法为遍历数组，上升则继续，遇到下降时标记，当遇到再次上升时加入峰值并重新遍历，该方法边界难判定。  
  
283.移动零：双指针题，left指针代表处理完毕的标志，left往左的都为非零元素，right一直往右移动，每次遇到非零元素时都会和left交换，直到遍历完毕。开始阶段可以理解为，若遇到非零元素，左右指针同时移动，则为自交换不改变，遇到零元素时右指针开始移动得更快。  该题型可理解为数组处理问题，可利用标记处理进度的方式解题。

136.只出现一次的数字；先排序，再遍历数组，若和两侧的都不相同，则为答案；因为要防止数组越界，所以需要特殊判断第一个和最后一个元素；最后还需要一个特判，当只有一个元素时直接输出。

#2024.5.29  

238.除自身以外数组的乘积，一看到这道题O(n)的时间复杂度就想着要用前缀积处理，用前缀积除以当前元素，但是题目明显指出不能用除法，故放弃。既然如此，可以顺着前缀积的思路，预处理每个元素的左边的前缀积和右边的后缀积，这样用两边相乘即可得到答案。但是题目有要求O(1)的空间复杂度，所以只能利用答案数组，答案数组可以先存前缀积，在循环遍历的同时动态更新后缀积，即可实现。

28.找出字符串中第一个匹配项的下标，思路很简单，遍历主字符串，当遇到首字母相同时，判断接下来的一定长度内每个字母是否都相同，若出现不同则验证下一个，若都相同则可以输出答案。初始化答案为-1.

#2024.5.30

58.最后一个单词的长度，逆向思维，从字符串尾部往前遍历，找到第一个不为空的字符即为最后一个单词的尾部，往前找到第一个为空的下标，之间即为长度。

53.最大子数组和，最开始想到利用前缀和的方法，但是时间复杂度过高，所以我们借用其思想，思考更优的方法，即通过O(n)的时间复杂度，预处理或者维护一个最大值。最后选择了动态维护一个最大前缀并且动态维护答案。主要代码如下：
、、、  
cnt = max(cnt+nums[i],nums[i]);
ans = max(ans,cnt);
、、、

2024.5.31

**每日一题**
2965.找出缺失和重复的数字，最简单思路即为哈希表，遍历数组，记录出现的频次，再次遍历哈希表找出值为0和2的下标即可，该方法时间复杂度和空间复杂度都为O(n²)。所以我们应该思考更优的方法，刚看到这道题时，其实就想到了矩阵求和有什么性质，假设a出现了两次，b出现了零次，此时矩阵的和减去数列1~n²的和，差值为a-b;得到了一个式子还不足以解出答案，所以我们应该寻找另一个表达式的值，所以我们想到了利用矩阵元素的平方和，用当前矩阵的平方和减去数列1~n的平方和，差值为a²-b²=(a+b)*(a-b),所以这时我们就可以联立方程组进行求解了。假设第一个差值为d1，第二个差值为d2，则a=(d2/d1+d1)/2,b=(d2/d1-d1)/2,顺利结束。这个算法只用了O(1)的空间。小问题：1.注意n²求和的范围，需要开longlong  2.数组长度为n，但是最大数为n².

2966.划分数组并满足最大差限制，看到这题的意思，就能想到是考虑相邻k个数的关系，所以我们选择先对数组排序，原数组肯定为3的倍数。之后就开始遍历数组，i每次+3，先判断两端数字的差是否满足条件，若满足，则将这三个数字作为一个数组插入到答案数组中，当然，我们还需要一个标记，当出现不满足的数字时，我们返回空数组。小问题：二维数组初始化可以只定义行数，也可以都定义。当我们定义了长度之后，相当于数组已经存在了n个0，所以这时进行替换操作更好，如果我们要在末尾加入，则原始的0还存在，所以这时不建议初始化长度。

2024.6.1

**每日一题**
2928.给小朋友们分糖果 Ⅰ，考虑到数据范围较小，本题可以直接通过枚举两个小朋友得到的糖果数，再判断第三个是否满足条件就可以。当然对于数据范围较大的情况下时，本方法就不适用。可以通过数学中的容斥定理求解。

2929.给小朋友们分糖果 Ⅱ，这时数据范围变大，我们需要改进枚举的方法，只能使用O(n)的时间复杂度，所以我们只枚举第一个小朋友得到的糖果数量，之后我们需要判断当前情况是否能继续分，当n-i>2*limit时，说明肯定不满足，continue;如果满足，我们则需要算出当前所有的方案数，因为确定第二个小朋友的糖果数量后第三个就自然确定，所以方案数就等于第二个小朋友可能获得的糖果数，所以我们找到肯能得到的最多糖果和最少糖果进行作差即可得出答案。
ans+=min(n-i,limit)-max(0,n-i-limit)+1;

2024.6.2

**周赛题目**
100307.候诊室中的最少椅子数，设置两个变量，ans代表一共需要的椅子，cnt代表现有可用的椅子，判断三个状态即可，当读取到'E'时，若cnt==0，ans++，若cnt>0,，cnt--;
当读取到'L'时,cnt--;最后返回ans即可。

100311.无需开会的工作日,思路为先排序数组，然后遍历时间数组，维护一个上次会议的结束时间，每次判断开始时间是否大于上次的结束时间，如果大于，则把他们的差值加上，然后重新更新结束时间，注意，最后一次会议需要再判断一次。

100322.删除星号以后字典序最小的字符串,开一个大小为26的动态二维数组，负责存储每个字母出现的次数，以及每次出现的下标，遍历数组，如果遇到'*'，则遍历哈希数组，最小不为空的字符把最后一次出现的位置弹出，若没遇到，则把字符的下标存入。再定义一个答案字符串，遍历字符数组中出现的位置，将存在的下标对应的字母逐个加入到答案中。

**每日一题**

575.分糖果，根据题意，最多的数目肯定不会超过n/2，也不会超过所有糖的种类数。所以我们只需要比较两者的大小关系即可，关键是求出种类数。我们利用C++中的数据结构set，
return min(unordered_set<int>(candyType.begin(), candyType.end()).size(), candyType.size() / 2);
set可以自动去除重复的元素，它的长度就代表了种类数。

2024.6.3

**每日一题**

1103.分糖果 Ⅱ，根据题意模拟即可，维护一个当前应发的糖果值，当糖果数不为0时，遍历数组，判断当前剩余和应发的大小关系，更新答案数组和剩余值及应发值。

1109.航班预订统计，该题考查的是大量的区间修改后查询区间的值。我们采用的是差分数组的方法，先初始化一个差分数组，由于刚开始原数组都为0，所以差分数组初始化也都为0。每当有一个修改操作进行时，传入三个参数l，r，w，执行以下操作：
a[l]+=w;
a[r+1]-=w;
即可得到差分数组，将区间修改操作时间复杂度降至常数级。
得到差分数组之后，进行前缀和操作即可恢复原数组。
做前缀和时，可以不用开新的空间，在原数组操作即可。

2024.6.4

**每日一题**

3069.将元素分配到两个数组中 Ⅰ，按照题意模拟即可，新建两个数组，依次判断加入，最后合并最终答案数组即可。

3070.元素和小于等于k的子矩阵的数目，根据题意，很明显想到前缀和的知识，这里其实是二位前缀和的模板，算出所有前缀和并判断条件即可。
sum[i+1][j+1]=sum[i][j+1]+sum[i+1][j]+grid[i][j]-sum[i]

2024.6.5

**每日一题**
392.判断子序列，利用双指针的思想，遍历主字符串，当遇到相等的字母，目标字符串下标+1.判断最后的下标，若刚好为字符串的长度，即为正确。

383.赎金信，利用哈希表的思想，先构建一个字符计数数组，负责统计ransomNote中字符出现的次数，然后再遍历magazine数字，如果每个字符对应的计数数组都够用，那么证明可以完成。

2024.6.6

**每日一题***
2938.区分黑球和白球，刚开始没认真审题，没发现只能交换相邻的球，所以写了一个头尾的双指针，导致了错误，但是还是有两个收获，第一个是利用while写头尾双指针的题目时，一定要加上边界判断，及时跳出循环，否则会一直超时;第二个是对于一个数字字符串赋值或者判断值时，一定要用引号，不能直接给出数字。弄清楚题意之后，可以利用贪心的思想，我们发现从左遍历字符串，每次遇到一个0，就要把它移动到左边，移动的次数为它左边1的个数，因为1肯定要越过最右边的0，所以我们只需要维护一个当前状态下遇到1的个数，再维护一个当前移动的次数，每次遇到1时，sum++，遇到0时，ans+=sum.

209.长度最小的子数组，该题最差的算法为循环暴力求解，每次更新最小值；再其次到前缀和+二分查找的方法，该方法也需要每次从起点开始遍历;最优算法为滑动窗口，从0开始，累加至>=target，此时开始判断，若start往前还是满足和的条件，则不断尝试更新当前子数组的和以及最小长度，若不满足和的条件，则数组末尾继续往前，一直延申至数组末尾。

2024.6.7

**每日一题**
3038.相同分数的最大操作数目 Ⅰ，该题为简单模拟题，先计算出前两个元素的和，依次往后遍历两个元素，若它们和与之前的相同，则答案++，若不同则直接跳出，结束。

134.加油站,该题最开始想到令每个加油站作为起点遍历一次数组，若能回到原点，则证明它为答案；但是该方法时间复杂度过高，我们需要进行优化，我们可以进行数学推导，若从i出发，到达j时不满足条件，不能继续前进，那么从i-j之间任何一个加油站出发都无法满足条件，所以我们直接从j+1个开始向前判断，降低了时间复杂度。每次遍历一个节点时，新建一个cnt向前，当向前超过数组最大数量时，我们需要用取余代表取回前面的节点。

135.分发糖果，从题目出发，刚开始理解为找到数组中最大的值，依次往两边递减，但是不好实现，所以作罢;后面又考虑到可以通过计算左边的上升子序列的长度和右边下降子序列的长度，再求其中的最大值求解，为了降低时间复杂度，所以我们可以通过两次遍历数组来代替二重循环;第一次从左到右遍历，算出每个元素连续左边上升序列的长度，第二次从右往左，算出每个元素右边连续下降序列的长度。同时，可以只开一个数组，第二次遍历用一个变量储存当前值，可以降低空间复杂度。

2024.6.8

**每日一题**
3040.相同分数的最大操作数目 Ⅱ，通多题意可知，该题最多有三种操作分数，分别是前两个，最后两个，以及第一个和最后一个的和。从这里也可以看出一共有三种状态转移方式，所以我们可以利用DP或者记忆化搜索的方式来求解。对三种操作分数分别求最大次数，再求他们的最大值。依次判断三个状态，当前区间的前面两个，最后两个，以及第一个和最后一个，直到遍历区间长度为1就可以求出整个区间的答案。

516.最长回文子序列，该题是一个区间求最值问题，我们自然地想到可以通过小区间转移到大区间来进行求解，状态转移就对应着动态规划或者搜索算法。在本题中我们使用DP思想，从尾部开始遍历字符串，对于每个字符再遍历它之后的元素，一共有三种状态，当i==j时，令数组为1;当s[i]==s[j]时，我们还要分情况讨论，如果i==j-1，此时直接令数组为2，因为下一个状态i>j;如果i！=j-1，那么f[i][j]=f[i+1][j-1]+2;
最后一种情况是，当两个字符不构成回文子串时，我们选择上一个状态下最大的一端继续前进，  
f[i][j]=max(f[i+1][j],f[i][j-1]);

2024.6.9

**每日一题**
312.戳气球，根据题目的意思，我们需要依次戳破区间内的所有气球，得出最后的答案，那么我们可以看出本题的思想为动态规划的状态转移，枚举每个可能作为最后一个戳破的气球k，ij为区间的两个端点，每次区间的长度从3开始往后枚举，模拟从戳破最后一个气球开始往回倒推的过程。刚开始时需要新建一个数组加入前后两个端点值。状态转移方程如下：
 f[i][j]=max(f[i][j],f[i][k]+f[k][j]+cnt[i]*cnt[j]*cnt[k]);

周赛题：
100325，找出K秒后拿着球的孩子，本题为简单模拟，我们只需要遍历时间，每次更新当前拿着球的孩子即可，但是传球的方向会改变，所以我们需要定义一个方向变量，当回到第一个时方向为1，到达最后一个时方向为-1.

双周赛题：
100324，清楚数字，本题为简单模拟题，可以理解为当遇到字母时就将该元素入栈，遇到数字时就出栈，模拟完成即可。  

定义栈：        std::stack<char> charStack; 
判断元素是数字或字母：isdigit(),isalpha()
栈相关操作：Stack.pop(),Stack.empty(),Stack.push()
最后需要将栈转为字符串，定义一个空字符串，将Stack.top()依次加上

2024.6.10

**每日一题**
881.救生艇，依据题意可以看出这道题是一道贪心的题目，即越多地安排两个人坐一艘船更好，所以我们想到每次都用最小和最大的组合，判断是否能够合并，故需要先进行排序，然后利用双指针的特性，如果前后两个可满足，那么就共同向中间靠近，如果不满足，就后面的往前一个单位。最后需要注意的是，需要判断当最后只剩一个人的时候 ，再加上一条船。

125.验证回文串，依据题意模拟即可，首先新建一个字符串，将原字符串的数字元素保留，字母元素转为小写之后保留，再利用双指针方法逐次向中间靠拢，只要有一组不相同，直接返回false，直到遍历整个字符串。

if(isdigit(s[i])) ans+=s[i];
if(isalpha(s[i])) ans+=tolower(s[i]);

167.两数之和Ⅱ-输入有序数组，该题数组已经排序好了，且答案只有一种可能，那么我们只需要遍历数组，找到一个正确的答案就退出即可。为了降低时间复杂度，我们可以通过二分查找或者双指针的方法来求解。利用二分查找的方法时，我们只需要遍历一次数组，定义一个low，一个high指针，分别判断每次和的结果，如果等于目标则直接输出，若大于，则high=mid-1，若小于，则low=mid+1，可以快速完成数组的查找，最后如果都没有找到就返回-1。当我们使用双指针方法时，我们只需要定义头尾两个指针，依次向中间靠拢，如果等于目标值就返回，如果大于就后者往前，小于就前者向后，注意题目中下标从1开始，所以答案需要+1再输出。

2024.6.11

**每日一题**
419.甲板上的战舰，一看题目，就感觉是用dfs来求解，但是再想想更简易的方法。我们可以看到战舰是一个特殊的连通块，即一列或者一行，并且没有相邻的战舰，所以我们可以通过枚举战舰起点的方式来求解。遍历二维数组，如果找到'X',只需要判断其左边或者上面是否有'X'就可以判断出它是否是战舰的起点，如果是起点，那么答案加一。

15.三数之和，这一题我的方法是利用三种循环实现，但是最后会超时，于是我增加了一些剪枝操作，当一些情况下提前退出循环，但是始终无法通过，于是我发现了自己对于双指针的理解还没有很彻底。我认为我的代码实现了双指针，双循环枚举起点和终点，用while不断将mid向前，但是分析一下逻辑，这实际上还是三重循环，并没有真正实现双指针，所以这告诉我们，实现双指针不是用特定的代码结构就可以，而是真正的代码逻辑层面实现。所以我们应该通过枚举起点，固定终点，再枚举中间点，逐步寻找满足条件的三元组即可。

2024.6.12

**每日一题**
2806.取整购买后的账户余额，这题是个简单模拟题，我们只需要，算出两个数一个是购买金额除10，一个是除10后的余数，再判断余数的大小，如果大于等于5就需要购买(n+1)*10,否则购买n*10.

2810.故障键盘，简单模拟，新建一个字符串，遍历原字符串，当不为'i'时，字符加入新字符串，若读取到'i'，则反转字符串  
reverse(ans.begin(),ans.end());

104.二叉树的最大深度：本题的用意是学习递归和二叉树结构，在函数中，只有传递的节点为空时，我们才会返回，否则我们会继续往下寻找，并且每次递归时答案+1，只有最后一步才处理，答案在过程中递增。

70.爬楼梯，递归模板，动态规划模板，初始化第一和第二的答案，后续的答案为前两个相加即可。

242.本题为简单哈希表题目，先判断两字符串的长度是否相同，若不同，则直接返回false，如果相同，我们先统计s的字符哈希表，再遍历t字符串，如果不够用了，则返回false，否则返回true.

2024.6.13

**每日一题**
2813.子序列最大优雅度，本题利用了贪心的思想，首先将items按照profit从大到小进行排序，当子序列为前k个项目时，子序列的利润总和最大，但是总优雅度不一定最大，所以此时我们向后遍历，当下一个元素的类别出现两次以上，取利润最小的项目进行替换即可增加总优雅度，用栈来维护整个序列。

2879.显示前三行，这个是python中pandas库的使用，直接返回.head(n)即可

2894.分类求和并作差，这个是一个简单模拟题，遍历1到n，刚开始可能想到用两个变量来存，后面发现用一个变量也能完成，不整除的加上，整除的减去即可。

2024.6.14

**每日一题**
2786.访问数组中的位置使分数最大，看到这题就想到动态规划的思路，遍历数组，每次选择移动该元素时能获得到的最大值，分别考虑最后一个的元素为奇数/偶数的最大值，用长度为2的数组来储存这两个值，每次遍历到一个值就更新。

2652.倍数求和，该题一看就是简单模拟题，遍历一次当能整除就加上即可。但是这样时间复杂度太高，所以考虑数字中的容斥原理。只考虑整除一个数时，答案数列是一个等差数列。根据容斥原理，最后答案为三个数的答案，减去两两结合的答案，再加上三个一起的答案。

2024.6.16

**周赛题目**
100304.构成整天的下标对数目 Ⅰ，简单模拟题，遍历数组，若找到两个下标对应的数加起来为24的倍数，那么ans++.

100301.构成整天的下标对数目 Ⅱ，上题的数据增强版，这里我们考虑查询和维护即可，遍历数组，当每次加上能满足条件的数组的下标个数，再更新当前的数组值
 ans += cnt[(24 - t % 24) % 24];
 cnt[t % 24]++;

**每日一题**
521.最长特殊序列 Ⅰ，脑筋急转弯，其实这里的特殊序列只要是自己的字串即可，那么我们直接取本身就是最长，如果两个字符串不相等，直接取两者的长度最大值就好，如果相等，就返回-1.

221.最大正方形，二维前缀和模板，先处理出二维前缀和数组，再进行二分查找降低复杂度。

2024.6.17

**每日一题**
522.最长特殊序列 Ⅱ，本题为前者的升级版，从两个字符串变成一个字符串序列了，所以我们需要依次枚举字符串来进行判断。先写一个判断两字符串是否相等的函数，然后枚举字符串逐个判断是否相等，若不相等则更新长度。

326.3的幂，简单模拟题，不断判断是否为3的倍数将数除3，判断最后是否为1，若不是则输出false.

389.找不同，本题为哈希表的简单应用，只需要先统计s字符串的哈希表值，再遍历t字符串，当遇到哈希值为的字符就返回.

455.分发饼干，简单排序+双指针的题目，首先对两个数组进行排序，之后利用双指针分别指向两个数组的起点，若满足条件，则一起前进，若不满足，则S数组的指针前进。

2024.6.18

**每日一题**
2288.价格减免，这是一道纯字符串的题目，我们的目标是识别出字符串中的价格并将它替换为折扣后的数字。这道题利用了一些字符串的关键字：
stringstream 是C++标准库中的一个类，属于 <sstream> 头文件。它提供了一种方式来处理字符串，就像使用流一样，可以轻松地将数据读入或写出到字符串。
#include <sstream>
stringstream ss; // 创建 stringstream 对象
ss << "Some data"; // 向 stringstream 对象写入数据
string data;
ss >> data; // 从 stringstream 对象读取数据

all_of 是C++算法库中的一个函数，位于 <algorithm> 头文件。它用于检查给定范围内的所有元素是否都满足特定的条件。
#include <algorithm>
string s = "12345";
if (all_of(s.begin() + 1, s.end(), ::isdigit)) {
    // 从 s.begin() + 1 开始到 s.end() 所有的元素都满足 ::isdigit 条件
}

fixed：指定浮点数应该以固定的小数点格式输出。
setprecision(2)：设置小数点后保留两位数字。
stoll(w.substr(1))：将字符串 w 去掉第一个字符后的剩余部分转换为长长整型（long long）


219.存在重复元素，这道题的本质上是滑动窗口的模板题，我刚开始的想法是遍历数组再同时向前遍历k个元素来判断，此时时间复杂度为N*K，为了降低，应使用set结构。
set的基本语法：
unordered_set<int> s  定义初始化
s.emplace(nums[i]) ：插入元素
s.erase(nums[i - k - 1]) ： 删除元素
s.count(nums[i]) ：判断s中是否已经存在该元素


2024.6.19

**每日一题**
2713.矩阵中严格递增的单元格数，这题是一道动态规划问题，因为可以跳转到同一行同一列的任意位置，所以我们不需要记录前一个状态，只需要记录更新到每个位置能得到的最大值即可，同时更新每列和每行的最大值。

35.搜索插入位置，本题为二分查找模板题，目的是掌握二分的正确写法，这里就列出三种区间下的二分写法：
  // 闭区间写法
    int lower_bound(vector<int> &nums, int target) {
        int left = 0, right = (int) nums.size() - 1; // 闭区间 [left, right]
        while (left <= right) { // 区间不为空
            // 循环不变量：
            // nums[left-1] < target
            // nums[right+1] >= target
            int mid = left + (right - left) / 2;
            if (nums[mid] < target)
                left = mid + 1; // 范围缩小到 [mid+1, right]
            else
                right = mid - 1; // 范围缩小到 [left, mid-1]
        }
        return left; // 或者 right+1
    }

    // 左闭右开区间写法
    int lower_bound2(vector<int> &nums, int target) {
        int left = 0, right = nums.size(); // 左闭右开区间 [left, right)
        while (left < right) { // 区间不为空
            // 循环不变量：
            // nums[left-1] < target
            // nums[right] >= target
            int mid = left + (right - left) / 2;
            if (nums[mid] < target)
                left = mid + 1; // 范围缩小到 [mid+1, right)
            else
                right = mid; // 范围缩小到 [left, mid)
        }
        return left; // 或者 right
    }

    // 开区间写法
    int lower_bound3(vector<int> &nums, int target) {
        int left = -1, right = nums.size(); // 开区间 (left, right)
        while (left + 1 < right) { // 区间不为空
            // 循环不变量：
            // nums[left] < target
            // nums[right] >= target
            int mid = left + (right - left) / 2;
            if (nums[mid] < target)
                left = mid; // 范围缩小到 (mid, right)
            else
                right = mid; // 范围缩小到 (left, mid)
        }
        return right; // 或者 left+1
    }


2024.6.20

**每日一题**

2748.美丽下标对的数目，这道题可以通过暴力求解，也可以使用哈希表来求解，同时通过本题，我发现了C++的gcd函数可以直接调用.暴力方法为两重循环遍历，判断他们的gcd是否为1；哈希表的方法为，不提前处理出哈希表的值，而是遍历数组的同时，对于每个当前数字的第一个，寻找哈希表中互质的数字是否存在，若存在则把所有答案加上，做完这个操作后再将当前的数字加入哈希表(即哈希表中存的是当前元素之前的元素最后一个数字的相应出现次数，保证了有序性),从这题可以得出一个启示，在一些需要保证顺序的题目里，我们可以在遍历的途中同时更新表值，gcd函数:gcd(x,y)

118.杨辉三角，这是一道动态规划的入门题目，依题意每个元素等于它上面的两个元素求和，所以我们首先规定每行第一个和最后一个元素为1，然后再依次遍历这一行每一个元素，令其为它左上角和右上角元素的和即可，注意控制数组的大小。

2024.6.22

**每日一题**

2663.字典序最小的美丽字符串，该题考察了回文串的性质，一个回文串去掉首尾字母后，仍然是回文串，可以根据这一性质得到如果没有长度为m-2的回文串，那么就不会有长度为m的回文串.由答案取的是最小字典序进一步推论得，不可能存在s[i]==s[i-1]以及s[i]==s[i-2].

560.和为K的子数组，该题中的子数组是连续的，所以可以看做是滑动窗口的模板，在这我们使用的是哈希表+前缀和的思想，两个下标的前缀和数组相减即为他们之间元素的和，我们只需要遍历依次数组，同时检查哈希表中是否有符合条件的键值，若存在，则把对应的值加上，同时更新哈希表的值.

2024.6.23

**每日一题**

520.检测大写字母，本题是简单模拟题，考察了ASCLL码相关的知识，根据题意，本题对于字符串有三种正确的用法，所以我们分三类来讨论，先根据首字母的大小写来分类，如果首字母大写我们计数剩下字母串大写字符的数量，如果为0或者为n-1就成立;对于首字母小写的情况，我们同样计数，若后续大写字母为，则符合.判断大小写可以用用字符-'a'的数值来判断，也可以直接和字符判断
if(word[i]>='A'&&word[i]<='Z') ans++;

**周赛题目**
100342.最小元素和最大元素的最小平均值，这道题本来想用简单数学的方法来求解，认为最后两个移除的元素肯定是最小值，也就是答案，后面才发现自己的想法出问题了，会有特殊情况，所以必须依次比较。设置头尾双指针，依次计算平均值取最小，计算后两端向中间靠拢，最后输出答案。注意数据格式。

2024.6.24

**每日一题**
503.下一个更大元素 Ⅱ，刚开始思考时，会想到坐标变换，进而想到每个数字追多遍历数组的两倍长度，即我们可以把数组整体往后复制一遍，遍历查询即可，但是时间复杂度太高，考虑其他算法;使用单调栈，单调栈中保存的是下标，该下标数组在原数组对应的值是单调不升的，每次我们移动到数组中的一个新的位置 iii，我们就将当前单调栈中所有对应值小于 nums[i] 的下标弹出单调栈，这些值的下一个更大元素即为 nums[i]（证明很简单：如果有更靠前的更大元素，那么这些位置将被提前弹出栈）。随后我们将位置 iii 入栈。
但是注意到只遍历一次序列是不够的，例如序列 [2,3,1][2,3,1][2,3,1]，最后单调栈中将剩余 [3,1][3,1][3,1]，其中元素 [1][1][1] 的下一个更大元素还是不知道的。

2024.6.25

**每日一题**

2723.找到矩阵中的好子集，该题考察了一定的数学推导能力，如果答案只有一行，那么必须全0，如果是2-3行，那么每列只能有一个1，如果答案超过四行时，每一行的和最多是k/2，任意两行的AND均不为0，每一行的1的个数的平均值是n/2。遍历每行，算出一个二进制数，去重保存到哈希表中，如果有一行全为0，则返回该行的行号，否则写一个二重循环，枚举哈希表中选两个数的所有组合，若出现AND等于0，那么返回行号。

20.有效的括号，这题是一个栈的模板题，我们先用map储存相应的括号对应情况，只存后括号，前面的不需要匹配，直接入栈即可，判断的时候需要判断栈顶元素是否和相应的键值匹配。

2024.6.26

**每日一题**

526.优美的排列，该题考察的是状压dp的知识，用一个n位的二进制数表示排列中的数被选取的情况，若为1，则表示该位被选取，若为0，则表示该位没有被选取，用一个数组来存储当前情况下的排列数，当前的状态应该由以下所有情况转移而来:枚举当前二进制数中1的位置，若该位置往后一位满足题目的条件，那么就加上这个状态的排列数，遍历所有，最后输出f[(1<<n)-1];
__builtin_popcount(mask)
该函数的作用是返回该二进制数中1的个数.

2741.特别的排列，这题跟上题有些相似，不过这些数字不是依次增大的，利用递推的方法，不断寻找前一个状态的值，并且累加。

2024.6.27

**每日一题**

2734.执行子串操作后的字典序最小的字符串，根据题意，只会出现一次操作，令一个区间内的字符变成自己的前一个字母，所以只有'a'是特例，其他都符合条件，那么我们先判断字符串是否为全a，如果是那么就只用把最后一个a换成z即可；如果不是全a，我们就需要找到第一个不为a的字母，开始遍历，直到找到下一个a字母，这之间都需要改变，对于该题中的字母变换，只需要s[i]--即可完成变换。

50.Pow(x,n),本题考察的是快速幂算法，利用了递归的思想，计算x的n次方时，可以先计算出y=n/2次方，判断N是奇数还是偶数，如果是偶数就是y*y，奇数则为y*y*x.递归边界为N=0.

2024.6.28

**每日一题**

2742.给墙壁刷油漆，根据题意，可以得出几个结论，首先是付费刷墙的总时间要大于等于免费刷墙的个数，其次是付费刷墙个数与免费刷墙个数之和为n，结合之后得到付费刷墙时间之和大于等于n-付费刷墙个数，即[付费刷墙时间+1]之和大于等于n，所以我们把这个看作一个01背包的题目，时间+1作为体积，花费作为价值。

190.颠倒二进制位，本题考察的是基础的位运算性质，相关解释如下：
 uint32_t rev = 0;
 uint32_t 这个是用来定义一个32位的二进制串
 rev|=(n&1)<<(31-i);
 n>>=1;
 上述代码的意思是每一取n中的最低位，并且将它移动到最前面，用答案字符串进行或运算，因为它本身为全0，所以答案的每一位全部取决于原二进制位，每次操作之后将原字符串右移一位，表示最低位处理完毕，舍弃之后对下一位 继续处理。

 2024.6.29

**每日一题**

2710.移除字符串中的尾随零，本题是一个简单模拟题，考察一些字符串的基本操作，最直接的思想就是从后往前遍历，标记第一个不为0的下标，然后取这个下标之前的数即可。
return num.substr(0, num.find_last_not_of('0') + 1);

substr的作用是只保留范围内的字符，find_last_not_of的作用是找到最后一个不为0的位置，也可以手写循环代替。
string res(num,0,i+1) 
这个和以下代码等效
num.substr(0,i+1);

2024.6.30

**周赛题目**

100340.三角形的最大高度，本题是一个简单模拟题，根据题意，一共有两种情况，分别是蓝球和红球在第一层的情况，所以我们只需要分别执行这两种情况来计算高度，答案是这两种情况下的更大的一方，通过判断层数的奇偶性来判断即可。

**每日一题**

494.目标和，利用动态规划的思想，假设neg是所有添加负号元素的和，那么可推出，如果整个数组的元素的和减去目标元素不是偶数就直接返回零;现在问题就转变为通过从数组中选取若干元素作为添加负号的元素，他们的和要与全部元素的和减去目标值再除以2相等，所以就转换为动态规划问题，dp[i][j]表示从前i个数种选取元素使得与j相等的方案数，最终答案为dp[n][(sum-target)/2];

2024.7.1

**每日一题**

2065.最大化一张图中的路径价值，本题可以从数据范围得到思路的参考，根据总最大时间和单个最小时间得到最多可以有十条边，即搜索树有11层，每个节点最多有4个儿子，可视为一棵层数至多为11的四叉树上递归。本题还可以利用Djikstra最短路算法进行剪枝，提前处理好起点到每个节点的最短路，同时也是每个节点到起点的最短路，在递归到下一个节点之前，判断下一个节点在走最短路的前提下，能否在maxTime时间内回到起点0，若不能，则不递归。

11.盛最多水的容器，本题是一个双指针的题目，依据题意得，水量等于两边高度更小的一边乘上下标之差，所以我们只需要利用双指针遍历一次数组即可得出最终答案，每次更新当前最大值，并且令两端更小的向中间靠拢，本质上是一个贪心的思想。

380.O(1)时间插入、删除和获取随机元素，本题是利用unordered_map数据结构来存储对应值和下标的键值对，该数据结构可用来当作哈希表，插入为insert，删除为erase，并且用末尾元素填充。获取随机元素的函数：rand()

2024.7.2

**每日一题**

3115.质数的最大距离，本道题是一个简单的模拟题，题意是找到数组中第一个质数和最后一个质数，可以通过写一个质数筛来预处理标记质数再输出即可;由于本题的数据范围较小，所以我们只需要用最简单的指数判断方法即可，每个数都遍历到它的根号范围，然后分别通过正向和反向遍历找到第一个和最后一个质数，输出他们的下标差即可。

1441.用栈操作构建数组，本题是一个简单模拟题，遍历n，当我们的目标数字在target中就只用Push，否则需要先Push再Pop，维护一个prev记录上一次操作时栈顶的索引值。

2024.7.3

**每日一题**

3099.哈沙德数，简单数学题，我们的目的是计算出每一位数的和，所以我们每次取数模10的结果，然后令其除10，最后判断是否能整除即可。

205.同构字符串，本题是考察哈希表的知识，根据题意，同构的条件是s的字符都按照某种映射关系得到t，所以我们通过构建两个哈希映射，分别代表s到t和t到s的映射，然后遍历字符串，如果出现映射不同的情况，则不满足条件，直接退出。

31.下一个排列，本道题考察的是双指针，题目的意思是找到下一个字典序更大的排列，所以我们的任务是把一个数组右边的一个较大数与数组左边的一个较小数交换，并且它们的距离应当尽量近，所以算法的步骤就是首先从后往前查找第一个顺序对，不满足降序的关系，标记为i.然后在i+1到n从后往前查找第一个下标j满足后数大于前数，然后交换两个数，并且将i+1到n之间的序列反转.

2024.7.4

**每日一题**

3086.拾起k个1需要的最少行动次数，在这道题我们可以把0看成空位，第二种操作相当于把一个1移动到和它相邻的空位上，而第一种操作则是贪心地把和当前下标相邻的0变成1;当maxchanges较大时，优先使用第一种操作+第二种操作;maxchanges较小的情况是，几所所有长为k-maxchanges的子数组的货仓选址问题，再取最小值。

78.子集，这道题用的是回溯的算法，也可以说是深度优先搜索。通过设置一个当前遍历的元素个数和需要遍历的数组来维护dfs函数，维护一个当前的集合和答案集合，当个数达到原数组大小时返回，遍历时包含两种情况，分别是考虑当前元素和不考虑当前元素，每次都先达到了最大元素个数，再依次返回。

2024.7.5

**每日一题**

3033.修改矩阵，本题为简单模拟题，题意是找到每列的最大值，然后把值为-1的更换即可，所以我们需要遍历两次数组，第一次把不是-1的点写入并且维护列的最大值，第二次把-1的点用列最大值更换即可。

228.汇总区间，这道题可以看作一个双指针的题目，任务是遍历数组，当找到不是逐个递增的元素时就把此前的范围按规则加入字符串，所以我们需要标记左指针和遍历找到右指针，找到右指针后更新字符串并且更新左指针。这道题要注意一个细节，当我们判断相邻元素是不是相差1时，不要用减法，而是用加法，因为减法会导致数据范围越界的问题。

202.快乐数，这道题直接看就是通过判断一个数通过规则变换能不能最终回到1或者是进入无限循环，如果我们根据路线就可以得出是判断有没有环的题目，所以我们可以使用快慢指针的方法，若循环，即出现环时，快指针会追上慢指针。初始化为快指针在慢指针前面一步，然后每次快指针走两步，慢指针走一步，如果追上了，证明有循环，否则快指针会回到1.