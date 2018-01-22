# Lecture II:  Consistent Hash & **Tiny URL system**

* [ ] Add Description of Consistent Hash

* [ ] Add solution of tiny url system

# Lecture III: **Distributed System **

就是用多台机器去解决一台机器上不能够解决的问题

Google 三剑客:

* Google File System 
* Map Reduce
* Bigtable

#### GFS Overview:

4S Rule: Scenario

**Scenario**: 用户写入一个文件，用户读取一个文件：支持多大的文件？越大越好，比如 &gt; 1000 T, 多台机器存储这些文件

**Service**: 多台机器怎么沟通

* 资本主义：master slave system

* 社会主义：server 平均分配负载

**Storage:**

* Q: How to store a 100gb video file in a operating system?

* A: Store the metadata and video context separately. Block Size. Then Merge it.

Write的方式是client端先分片好，然后再往chunk server里面写

| Client | Server |
| :---: | :---: |
| Browser | Webserver |
| Webserver | Database |
| Database | GFS |
| Webserver | GFS \(Goolgle File System\) |

**Scale**:

单Master够不够？

90%的系统都采用单master



