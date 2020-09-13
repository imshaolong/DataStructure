# 归并排序（MergeSort）

基本思路：两个有序数组的归并（类似于两个有序链表的归并）

```java
public void mergeSort(int[] array){
    //[0, length)注意这里是左闭右开
    mergeSortHelper(array, 0, array.length);
}
public void mergeSortHelper(int[] array, int left, int right){
    if(left + 1 >= right){//当区间中有1个或0个元素的时候，不能进行排序
        return;
    }
    //针对[left, right)区间，分成对等的两个区间
    int mid = (left + right) / 2;
    //两个区间分别是：
    //[left, mid) 和[mid, right)
    mergeSortHelper(array, left, mid);
    mergeSortHelper(array, mid, right);
    //通过上面的递归，我们认为这两个区间排好序了，接下来就可以进行合并了
    merge(array, left, mid, right);
}
public void merge(int[] array, int left, int mid, int right){
    //临时数组temp用来存储两个数组合并后的结果
    int[] temp = new int[right - left];//由于左闭右开的缘故这里是right - left
    //index用来记录当前temp数组中插入到了什么位置
    int index = 0;
    //当前有两个有序数组:[left, mid) 和 [mid, right)
    int cur1 = left;
    int cur2 = mid;
    
    while(cur1 < mid && cur2 < right){
        if(array[cur1] <= array[cur2]){
            //把cur1位置的元素插入到temp中
            temp[index] = array[cur1];
            index++;
            cur1++;
        }else{
            temp[index] = array[cur2];
            index++;
            cur2++;
        }          
    }
    
    while(cur1 < mid){
        temp[index] = array[cur1];
        cur1++;
        index++;
    }
    
    while(cur2 < right){
        temp[index] = array[cur2];
        cur2++;
        index++;
    }
    
    for(int i = left; i <right; i++){
        array[i] = temp[i - left];
    }
    
}
```

