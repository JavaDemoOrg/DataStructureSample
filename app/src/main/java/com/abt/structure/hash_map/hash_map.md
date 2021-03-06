
### HashMap    
1、HashMap 底层是基于数组和链表实现的。其中有两个重要的参数：    
- 容量       
- 负载因子       

容量的默认大小是 16，负载因子是 0.75，      
当 HashMap 的 size > 16*0.75       
时就会发生扩容(容量和负载因子都可以自由调整)。    

### put 方法   
首先会将传入的 Key 做 hash 运算计算出 hashcode,然后根据数组长度取模计算出在数组中的 index 下标。

由于在计算中位运算比取模运算效率高的多，所以 HashMap 规定数组的长度为 2^n 。这样用 2^n - 1 做位运算与取模效果一致，并且效率还要高出许多。

由于数组的长度有限，所以难免会出现不同的 Key 通过运算得到的 index 相同，这种情况可以利用链表来解决，HashMap 会在 table[index]处形成环形链表，采用头插法将数据插入到链表中。

### get 方法
get 和 put 类似，也是将传入的 Key 计算出 index ，如果该位置上是一个链表就需要遍历整个链表，通过 key.equals(k) 来找到对应的元素。

### 复杂度    
1、理想情况下HashMap的时间复杂度为O(1)，     
2、因为对于内存来说，访问任何地址的时间是一样的，      
3、即时间极短，相当于可以同时访问到所有地址。   
4、在时间复杂度为O(1)时，需要很大的内存空间，     
5、所以必须要对内存和时间进行取舍。     
6、咋取舍呢，hashmap在初始化的时候有俩值，     
7、初始大小和负载因子，默认是16和0.75，可以自己改，     
8、但是默认的就很合理了，除非你打算私人订制。      
9、大小不用解释，负载因子就是一个小数，扩容的时候用的，      
10、在put的时候，hashmap就检查一下自己的大小，       
11、是不是大于16x0.75（大小x负载因子），      
12、如果是，就扩容，扩容到2^n，为啥是这个呢，我看了很多资料，     
13、最合理的一种解释就是，hash值用二进制表示的，     
14、每次扩容增加一个二进制位，然后把oldmap放到newmap里，       
15、分配均匀，put的时候经过balabala的运算，      
16、可以减小冲突的几率，提高hashmap的性能。     
17、Java中的HashMap赋予每个键一个对应的映射即索引。   

### 参考文献    
0、[HashMap底层分析](https://github.com/crossoverJie/Java-Interview/blob/master/MD/HashMap.md)   
1、[hashmap时间复杂度](https://www.cnblogs.com/BBchao/p/7878699.html)     
2、[面试中关于HashMap的时间复杂度O(1)的思考](https://blog.csdn.net/donggua3694857/article/details/64127131)      
3、[Java7源码浅析——对HashMap的理解](https://blog.csdn.net/donggua3694857/article/details/52432906)    
4、[java中hashmap容器实现查找O(1)时间复杂度的思考](https://blog.csdn.net/u014633283/article/details/48549155)   
5、[JDK源码中HashMap的hash方法原理是什么？](https://www.zhihu.com/question/20733617)      