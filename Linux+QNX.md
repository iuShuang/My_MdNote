## 驱动程序编写流程

![image-20240516152201705](D:\A_Document\Routine_Document\实习\学习\image-20240516152201705.png)

## IIC

![image-20240517102757997](D:\A_Document\Routine_Document\实习\学习\image-20240517102757997.png)

![image-20240517104900090](D:\A_Document\Routine_Document\实习\学习\image-20240517104900090.png)

![image-20240517105334201](D:\A_Document\Routine_Document\实习\学习\image-20240517105334201.png)

## Linux可执行程序的结构主要包括以下几个部分:

1. ELF (Executable and Linkable Format) 头部:
   - 这部分包含了程序的基本信息,如程序入口地址、程序大小、程序类型(可执行程序、共享库等)等。
   - ELF头部是整个可执行程序的开头部分。

2. 程序头表(Program Header Table):
   - 程序头表描述了程序的各个段(section)的属性,如段的类型、内存地址、文件偏移等。
   - 操作系统通过读取程序头表来加载和执行程序。

3. 代码段(Text Segment):
   - 这部分包含了程序的可执行指令。
   - 代码段通常是只读的,并且会被映射到内存中执行。

4. 数据段(Data Segment):
   - 这部分包含了程序的静态数据,如全局变量、常量等。
   - 数据段可读写,并被映射到内存中。

5. 堆(Heap):
   - 程序运行时动态分配的内存区域,用于存储动态分配的变量和对象。

6. 栈(Stack):
   - 程序调用函数时使用的内存区域,用于存储函数调用信息和局部变量。
   - 栈的增长方向是从高地址向低地址。

7. 动态链接信息:
   - 如果程序使用了动态链接库,则会包含动态链接的相关信息。
   - 这部分信息描述了程序依赖的库函数及其地址。

综上所述,Linux可执行程序的结构包含了程序的基本信息、代码、静态数据、动态内存以及动态链接等关键组成部分。操作系统通过解析这些结构来加载和执行程序。

## USB

![image-20240517110828108](D:\A_Document\Routine_Document\实习\学习\image-20240517110828108.png)

![image-20240517111032941](D:\A_Document\Routine_Document\实习\学习\image-20240517111032941.png)

![image-20240517113357104](D:\A_Document\Routine_Document\实习\学习\image-20240517113357104.png)

![image-20240517113222812](D:\A_Document\Routine_Document\实习\学习\image-20240517113222812.png)

![image-20240517113304583](D:\A_Document\Routine_Document\实习\学习\image-20240517113304583.png)

![image-20240517113548518](D:\A_Document\Routine_Document\实习\学习\image-20240517113548518.png)

- 控制传输流程：
  - ![image-20240517114647862](D:\A_Document\Routine_Document\实习\学习\image-20240517114647862.png)

![image-20240517114128366](D:\A_Document\Routine_Document\实习\学习\image-20240517114128366.png)

![image-20240517114448175](D:\A_Document\Routine_Document\实习\学习\image-20240517114448175.png)

## pthread

Linux中的pthread(POSIX线程)是一组标准的C语言线程库,提供了丰富的线程管理功能。以下是一些常用的pthread函数:

1. 线程创建和终止:
   - `pthread_create()`: 创建一个新的线程
   - `pthread_exit()`: 终止当前线程
   - `pthread_cancel()`: 取消一个线程的执行

2. 线程同步:
   - `pthread_mutex_init()`, `pthread_mutex_lock()`, `pthread_mutex_unlock()`: 互斥锁相关函数
   - `pthread_cond_init()`, `pthread_cond_wait()`, `pthread_cond_signal()`: 条件变量相关函数
   - `pthread_rwlock_init()`, `pthread_rwlock_rdlock()`, `pthread_rwlock_wrlock()`, `pthread_rwlock_unlock()`: 读写锁相关函数

3. 线程属性管理:
   - `pthread_attr_init()`, `pthread_attr_destroy()`: 线程属性初始化和销毁
   - `pthread_attr_setdetachstate()`, `pthread_attr_getdetachstate()`: 设置和获取线程的分离状态

4. 线程同步对象管理:
   - `pthread_mutex_init()`, `pthread_mutex_destroy()`: 互斥锁初始化和销毁
   - `pthread_cond_init()`, `pthread_cond_destroy()`: 条件变量初始化和销毁
   - `pthread_rwlock_init()`, `pthread_rwlock_destroy()`: 读写锁初始化和销毁

5. 线程特定数据:
   - `pthread_key_create()`, `pthread_key_delete()`: 创建和删除线程特定数据键
   - `pthread_setspecific()`, `pthread_getspecific()`: 设置和获取线程特定数据

6. 其他:
   - `pthread_join()`: 等待线程终止
   - `pthread_detach()`: 设置线程为分离状态
   - `pthread_self()`: 获取当前线程ID

这些pthread函数为Linux下的多线程编程提供了丰富的功能支持,涵盖了线程的创建、同步、属性管理等各个方面。掌握这些函数的使用方法是Linux下多线程编程的基础。



## **18、设备驱动模型三个重要成员是？platfoem总线的匹配规则是？在具体应用上要不要先注册驱动再注册设备？有先后顺序没？**
设备驱动模型三个重要成员是 总线、设备、驱动；
platfoem总线的匹配规则是：要匹配的设备和驱动都要注册；