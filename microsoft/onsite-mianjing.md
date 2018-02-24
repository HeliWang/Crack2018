2018.2.23 Hiring Event -- Email and Query Intelligence \(Core AI\)

[https://careers.microsoft.com/jobdetails.aspx?ss=&pg=0&so=&rw=1&jid=345195&jlang=en&pp=ss](/h ttps://careers.microsoft.com/jobdetails.aspx?ss=&pg=0&so=&rw=1&jid=345195&jlang=en&pp=ss)



第一轮：印度SDE，聊了很久我做的游戏，问了一些AB Test和如果metric一个feature的成功与否

Coding: Word Break，用DP秒之

Follow Up: word break的string太长，memory装不下怎么办，我说分段，后来好像不分也差不多可以用



第二轮：

Coding: 给一个文件，里面内容未知，要求返回每个word的出现次数和出现行数，hashmap 加 array或者set

Followup: 这个文件特别大怎么办，我说shard之类的

Design: Web Crawler to get 1 million urls' page

大概就是先处理url，考虑很多短url会映射到同一个long url，然后shard一下这些url by domain，最终不同domain的page file会存到一起



第三轮：

大哥太羞涩了 coding 贼简单

Coding 1: 两个array，要求输出A\[i\] \* B\[j\] 的最大值，其中i &lt; j，一个for loop就可以了，维持一个maxA

Edge Case: 问了一下要不要考虑负数，大哥说太难了。。。其实也不难吧

还有就是A B 的size不一样

Coding 2: Sprial Matrix

Others: Node.js Benefit, async vs multithreading



第四轮:

前三轮feedback不错，这一轮明显变难

Coding: LC 727 我用moving window做的，后面看了下discuss，dp是最优的

System Design: 

说有一堆qps为y的worker，向一个网站，比如百度，发起query，上限是X

问怎么控制优化？

题都没太听懂，我瞎说了个load balancer or rate limiter，是真的没有get到他的点

