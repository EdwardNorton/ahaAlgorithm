# ahaAlgorithm
====================================
最快最简单的排序——桶排序
------------------------------------------------
期末考试完了老师要将同学们的分数按照从高到低排序。小哼的班上只有5 个同学，
###这5 个同学分别考了5 分、3 分、5 分、2 分和8 分（满分是10 分）。接下来将分数进行从大到小排序，排序后是8 5 5 3 2
首先我们需要申请一个大小为 11 的数组int a[11]。OK，现在你已经有了11 个变量，编号从a[0]~a[10]。
刚开始的时候，我们将a[0]~a[10]都初始化为0，表示这些分数还都没有人得过。例如a[0]等于0 就表示目前还没有人得过0 分，
同理a[1]等于0 就表示目前还没有人得过1 分……a[10]等于0 就表示目前还没有人得过10 分。
下面开始处理每一个人的分数，第一个人的分数是5 分，我们就将相对应的a[5]的值在原来的基础增加1，
即将a[5]的值从0 改为1，表示5 分出现过了一次。第二个人的分数是 3 分，我们就把相对应的a[3]的值在原来的基础上增加1，即将a[3]
的值从0 改为1，表示3 分出现过了一次。第三个人的分数也是5 分，所以a[5]的值需要在此基础上再增加1，即将a[5]
的值从1 改为2，表示5 分出现过了两次。

   #include <stdio.h>
   int main()
   {
. int a[11],i,j,t;
. for(i=0;i<=10;i++)
. a[i]=0; //初始化为0
. for(i=1;i<=5;i++) //循环读入5个数
scanf("%d",&t); //把每一个数读到变量t中
a[t]++; //进行计数
}
for(i=0;i<=10;i++) //依次判断a[0]~a[10]
 
  for(j=1;j<=a[i];j++) //出现了几次就打印几次
      printf("%d ",i);
getchar();getchar();
//这里的getchar();用来暂停程序，以便查看程序输出的内容

//也可以用system("pause");等来代替

return 0;

}
输入数据为：
5 3 5 2 8
刚才实现的是从小到大排序。但是我们要求是从大到小排序，这该怎么办呢？还是先自己想一想再往下看哦。其实很简单，
只需要将for(i=0;i<=10;i++)改为for(i=10;i>=0;i--)就OK 啦，快去试一试吧。这种排序方法我们暂且叫它“桶排序”。
因为其实真正的桶排序要比这个复杂一些，以后再详细讨论
如果需要对数据范围在0~1000 之间的整数进行排序，我们需要1001 个桶，来表示0~1000之间每一个数出现的次数，这一点一定要注意。
另外，此处的每一个桶的作用其实就是“标记”每个数出现的次数，因此我喜欢将之前的数组a 
换个更贴切的名字book（book 这个单词有记录、标记的意思），代码实现如下。
include <stdio.h>
int main()
{
int book[1001],i,j,t,n;
for(i=0;i<=1000;i++)
book[i]=0;
scanf("%d",&n);//输入一个数n，表示接下来有n个数
for(i=1;i<=n;i++)//循环读入n个数，并进行桶排序
{
scanf("%d",&t); //把每一个数读到变量t中
book[t]++; //进行计数，对编号为t的桶放一个小旗子
}
for(i=1000;i>=0;i--) //依次判断编号1000~0的桶
for(j=1;j<=book[i];j++) //出现了几次就将桶的编号打印几次
printf("%d ",i);
getchar();getchar();
return 0;
}
可以输入以下数据进行验证。
10
8 100 50 22 15 6 1 1000 999 0
运行结果是：
1000 999 100 50 22 15 8 6 1 0
最后来说下时间复杂度的问题。代码中第6 行的循环一共循环了m 次（m 为桶的个数），第9 行的代码循环了n 次（n 为待排序数的个数），
第14 行和第15 行一共循环了m+n 次。所以整个排序算法一共执行了m+n+m+n 次。我们用大写字母O 来表示时间复杂度，
因此该算法的时间复杂度是O(m+n+m+n)即O(2*(m+n))。我们在说时间复杂度的时候可以忽略较小的常数，
最终桶排序的时间复杂度为O(m+n)。还有一点，在表示时间复杂度的时候，n 和m通常用大写字母即O(M+N)。
现在分别有 5 个人的名字和分数：huhu 5 分、haha 3 分、xixi 5 分、hengheng 2 分和gaoshou8 分。
请按照分数从高到低，输出他们的名字。即应该输出gaoshou、huhu、xixi、haha、hengheng。
发现问题了没有？如果使用我们刚才简化版的桶排序算法仅仅是把分数进行了排序。最终输
出的也仅仅是分数，但没有对人本身进行排序。也就是说，我们现在并不知道排序后的分数
原本对应着哪一个人！这该怎么办呢？不要着急，请看下节——冒泡排序。
