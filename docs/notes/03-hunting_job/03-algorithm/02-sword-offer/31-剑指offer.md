---
layout:  post
category:  algorithm
title:  No31、整数中1出现的次数
tagline:  by 阿秀
tags:
    - 原创
    - 剑指offer
    - 数据结构与算法
    - 算法
    - 社招
    - 校招
    - 阿秀
excerpt: No31、整数中1出现的次数
comment: false
---

<h1 align="center">带你快速刷完67道剑指offer</h1>

<div align="center">
  <a href="/notes/05-xiustar/01-xiustar_reading_guide/01-introduce.html#阿秀组建了一个校招学习圈子">
      <img src="https://axiu-image-bed.oss-cn-shanghai.aliyuncs.com/img/202206190108471.png">
  </a></div>


> 如果你想在校招中顺利拿到更好的offer，阿秀建议你多看看<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[前人的经验](/notes/05-xiustar/01-xiustar_reading_guide/01-introduce.md)</font> ，比如<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[准备](/notes/05-xiustar/02-campus_prepare/02-01-校招重要时间点科普.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[简历](/notes/05-xiustar/03-resume/01-00-简历开篇词.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[实习](/notes/05-xiustar/04-school_practice/20220320-从公司角度来看，为什么要招实习生.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[上岸经历](/notes/05-xiustar/09-question_answer/20220817.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[校招总结](/notes/05-xiustar/05-campus_recruitment/2020-12-16-双非渣硕的秋招之路总结（已拿抖音研发岗SP）.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[阿里、字节、腾讯、美团等一二线大厂真实面经](/notes/07-resources/01-free/04-schoolSchample.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[也欢迎来一起参加秋招打卡活动](/notes/05-xiustar/01-xiustar_reading_guide/01-introduce.html#阿秀组建了一个校招学习圈子)</font> 等；如果你是计算机小白，学习/转行/校招路上感到迷茫或者需要帮助，可以<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[点此联系阿秀](/notes/08-other/02-question.md#_4、阿秀-如何才能联系到你)</font>；免费分享阿秀个人学习计算机以来的收集到的好资源，<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[点此白嫖](/notes/07-resources/01-free/01-introduce.md)</font>；如果你需要《阿秀的学习笔记》网站中求职相关知识点的**PDF版本**的话，可以<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[点此下载](/notes/08-other/02-question.md#_5、如何下载阿秀的学习笔记内容pdf版本)</font> 




## **No31、整数中1出现的次数（ 从1 到 n 中1出现的次数 ）**

<font style="font-weight:normal; color:#4169E1;text-decoration:underline;" target="_blank">[牛客网原题链接](https://www.nowcoder.com/practice/bd7f978302044eee894445e244c7eee6?tpId=13&&tqId=11184&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)</font>

### **题目描述**

求出1-13的整数中1出现的次数,并算出100-1300的整数中1出现的次数？

为此他特别数了一下1~13中包含1的数字有1、10、11、12、13因此共出现6次,但是对于后面问题他就没辙了。

ACMer希望你们帮帮他,并把问题更加普遍化,可以很快的求出任意非负整数区间中1出现的次数（从1 到 n 中1出现的次数）。 

**输入**

```
13
```
**返回值**

```
6
```



### **1、经典方法吗，真的想不到这种方法，我服了**

执行用时：0 ms, 在所有 C++ 提交中击败了100.00%的用户

内存消耗：5.8 MB, 在所有 C++ 提交中击败了100.00%的用户

分两种情况，例如：1234和2234，high为最高位，pow为最高位权重
在每种情况下都将数分段处理，即0-999，1000-1999，...，剩余部分

 case1：最高位是1，则最高位的1的次数为last+1（1000-1234）
               每阶段即0-999的1的个数1*countDigitOne(pow-1)
               剩余部分1的个数为countDigitOne(last)--最高位已单独计算了

 case2：最高位不是1，则最高位的1的次数为pow（1000-1999）
               每阶段除去最高位即0-999，1000-1999中1的次数为high*countDigitOne(pow-1)
               剩余部分1的个数为countDigitOne(last)
              发现两种情况仅差别在最高位的1的个数，因此单独计算最高位的1（cnt），合并处理两种情况

~~~cpp
 int NumberOf1Between1AndN_Solution(int n)
    {
    if (n <= 0) return 0;
	if (n < 10) return 1;
	int high = n, pow = 1;// // 取出最高位 以及 最高位的权重
	while (high >= 10) {
		high /= 10;
		pow *= 10;
	}
	int last = n - high * pow;// 除最高位的数字
	int cnt = high == 1 ? last + 1 : pow;// high是否为1，最高位的1个数不同
	return cnt + high * NumberOf1Between1AndN_Solution(pow - 1) + NumberOf1Between1AndN_Solution(last);

    }
~~~



### **二刷：**

### **超级好的方法**

运行时间：2ms  占用内存：376k

~~~cpp
    int NumberOf1Between1AndN_Solution(int n)
    {
        if(n <= 0) return 0;
        if(n < 10) return 1;
        int high = n,pow = 1;//首选求的最高位high和权重pow 10 还是100 还是 100 呢
        while(high>=10){
            high = high /10;
            pow = pow * 10;
        }
        int last = n - high*pow;
        int cut = (high == 1? last + 1:pow );
        return cut + high*NumberOf1Between1AndN_Solution(pow - 1) + NumberOf1Between1AndN_Solution(last);
    }
~~~



### **三刷：**

~~~cpp
    int NumberOf1Between1AndN_Solution(int n)
    {
        if(n <= 0) return 0;
        if(n< 10 ) return 1;
        if(n == 10) return 2;
        int pow = 1, high = n,last = 0;
        while(high >= 10){
            high = high/10;
            pow *=10;
        }
        last = n - high*pow;// 除去最高位的数字，还剩下多少 0-999 1000- 1999 2000-2999 3000 3345
        int cut = high == 1 ? last+1: pow;
        
        return cut + high*NumberOf1Between1AndN_Solution(pow-1) + NumberOf1Between1AndN_Solution(last);

    }
~~~

<font style="font-weight:normal; color:#4169E1;text-decoration:underline;" target="_blank">[力扣](https://leetcode-cn.com/problems/number-of-digit-one/submissions/)</font>上有类似的题目


<p id = "整数中1出现的次数"></p>

