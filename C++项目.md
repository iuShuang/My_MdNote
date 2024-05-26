# 高并发内行池设计 (C++)

[实现高并发内存池 (C++)_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Q84y117Rd/?spm_id_from=333.337.search-card.all.click&vd_source=c4b26319211bc9ccc5ba3a0a22916e39)

## 或高并发实现高效内存管理

## 或高效内存池设计与实现

- 背景

  - 实现了高效的多线程内存管理，用于替代系统的内存 分配相关的函数（malloc 、 free ）
  - C/C++ 、数据结构（链表、哈希桶）、操作系统内存管理、单例模式、多线程、互斥锁

- 我的工作

  - 模拟实现出一个自己的高并发内存池

  - **a.**  性能问题

    **b.**  多线程环境下，锁竞争问题

    **c.**  内存碎片问题

- 实现结果

  

  - 增加动态申请的效率
  - 减少陷入内核的次数
  - 减少系统内存碎片
  - 提升内存使用率
  - 尽量减少锁竞争
  - 应用于多核多线程场景



目前许多开发场景都是多核多线程，在申请内存的场景下，存在激烈的所竞争问题，tcmalloc在多线程高并发场景下更好用，所以实现的内存池需要考虑以下方面：
1.性能问题
2.多线程环境下，锁的竞争问题
3.内存碎片问题；

高并发内存池设计主要由3各部分组成：

1. 为每个线程创建一个固定大小的独享线程缓存thread cache，线程从这里申请内存不需要加锁，以实现并发线程池的高效性能。

2. 实现一个中心缓存central cache， 其存储结构设计为哈希桶，为所有线程锁共享。Thread cache是按需访问central cache中大小不同的桶。采用单例模式并实现对桶加锁，以避免多线程访问下的锁的竞争问题。

3. 实现一会页缓存page cache，以实现对central cache的资源补充、向操作系统申请资源和资源回收。采用基数树实现空间回收。回收span对象时合并相邻的页，以组成更大的页，缓解内存碎片的问题

   

4. 向central cache分配时，实现对span定长大小的小块内存切割，

   

   central合适的试剂回收thread cache中的对象，避免一个线程占用了太多的内存，而其他线程的内存不够用，达到内存分配在多线程中更均衡的按需调度的目的。central cache 是存在竞争的所以从这里取内存对象是需要加锁的。首先者利用的是桶锁，其次只有thread cache的没有内存对象时才会找central cache，所以这里竞争不会很激烈。

3. page cache：页缓存是在central cache缓存上面的一层缓存，存储的内存是以页单位存储及分配的，central cache没有内存对象时，从page cache分配处一定数量的page，并切割成定长大小的小块内存，分配给central cache。当一个span的几个跨度页的对象都回收以后，page cache会回收central cache满足条件的span对象，并且合并相邻的页，组成更大的页，缓解内存碎片的问题。

管理页数的span

模拟实现出一个自己的高并发内存池，在多线程环境下缓解了锁竞争问题，相比于malloc/free效率提高了25%左右，将内存碎片保持在10%左右。



![image-20240405132537566](D:\A_Document\Routine_Document\实习\学习\image-20240405132537566.png)

![image-20240405132735498](D:\A_Document\Routine_Document\实习\学习\image-20240405132735498.png)

![image-20240405134137726](D:\A_Document\Routine_Document\实习\学习\image-20240405134137726.png)

![image-20240405134151384](D:\A_Document\Routine_Document\实习\学习\image-20240405134151384.png)

![image-20240405134204269](D:\A_Document\Routine_Document\实习\学习\image-20240405134204269.png)

![image-20240405134723299](D:\A_Document\Routine_Document\实习\学习\image-20240405134723299.png)

![image-20240405134802777](D:\A_Document\Routine_Document\实习\学习\image-20240405134802777.png)