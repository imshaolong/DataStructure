# 选择排序

- 基本思路：
    - 创建一个bound变量作为边界，通过bound将待排序序列分成两个部分[0, bound)和[bound, array.length)。
    - 其中，[0, bound)为已排序区间，[bound, length)为待排序区间。
    - bound所指向的元素为待排序元素，因此我们通过遍历待排序区间[bound,array.length)来选择出待排序区间的最小元素并将其与bound位置的元素进行交换，直到待排序区间为空。

```java
public void selectionSort (int[] array){
    for(int bound = 0; bound < array.length; bound++){
        int index = bound;
        int cur = bound;
        for(; cur < array.length; cur++){
            if(array[cur] < array[index]){
                index = cur;
            }
        }
        int temp = array[bound];
        array[bound] = array[index];
        array[index] = temp;
    }
}
```



- 时间复杂度：O(N^2)
- 空间复杂度：O(1)
- 稳定性：不稳定(eg: 6, 8, 6, 0)