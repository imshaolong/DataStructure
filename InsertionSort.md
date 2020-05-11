# 插入排序

- 待排序元素：array[length]
- 思路：将待排序的元素根据bound分成两部分：**已排序区间 ** 和 **待排序区间**即：[0, bound) 和[bound,length),每次将bound所指向的元素和已排序区间的元素从后往前依次比较的同时将已排序的元素不断向后移动，知道找到bound所指向元素的合适位置，并将bound所指向的待排序元素插入到所找到的合适位置。

```java
//以升序排序为例
public void insertSort(int[] array){
    //有序区间:[0, bound)
    //无序区间:[bound, size)
    for(int bound = 0; bound < array.length; bound++){
        int temp = array[bound];
        int cur = bound -1;
        for(; cur > 0; cur--){
            //如果这里的条件写成了array[cur] >= temp那此时就是不稳定的了
            if(array[cur] > temp){
                array[cur + 1] = array[cur];
            }else{
                break;
            }
        }
        array[cur + 1] = temp;
    }
}
```



- 插入排序的性能分析：
    - 时间复杂度：O(N^2)
    - 空间复杂度：O(1)
    - 稳定性：稳定排序