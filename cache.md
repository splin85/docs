# CPU cache
# 硬件原理
    -------------------------------------
    flag | tag1 | word1 word2 word3 word4
    flag | tag2 | word1 word2 word3 word4
    ------------------------------------
    
    CPU加载内存的一个cache line大小数据到cache.
    
    直接映射： 每组只有一个缓存块，CPU用索引定位到缓存，比较tag，再用块偏移定位到CPU需要的地址数据
               多个CPU地址对应一个缓存块，冲突率高；
    N路组相连：每组有N个缓存块，组内可以任意存储，比较tag，判断cache是否命中，减少了直接映射的冲突率，
               有效的利用了局部性原理；
    全相连：   相当于索引为0， CPU直接比较tag，判断cache是否命中，硬件比较电路延迟长；
    
    块偏移为地址的低位段， cache line=2^offset
    索引为地址的中间位段， 组数=2^index，如64组，则索引为6,2^6=64
    tag = cpu地址 - 索引 - offset
   
    例如： 
        data cache: 32-KB, 8-way set associative, 64-byte line size
        
        offset = 6, 64=2^6
        分组 = 32K/(8*64B)=64组
        tag = 32 - 6 - 6 = 20