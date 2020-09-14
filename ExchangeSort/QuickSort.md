# 快速排序(QuickSort)

- 核心操作：Partition

- Partition的过程：

    - 基准值的选取：可以选择第一个元素也可以选择最后一个元素，如果要选择中间的元素，就必须把这个中间元素交换到最前后或者最后面。

    

    

    - 让left从左往右找到一个比基准值大的元素
    - 让right从右往左找到一个比基准值小的元素
    - 交换left和right位置的元素（**交换之后left指向比基准值小的，right指向比基准值大的**）
    - 重复刚才的过程直到left和right重合

    

    

    - 当left和right重合的时候，此时left和right所指向的元素一定是大于基准值的元素

    

    - 接下来就把重合位置和基准值(最后一个元素)进行交换

    

    

    ```java
    public int partition(int[] array, int left, int right){
        //选取最右边的元素为基准值
        int pivot = right;
        while(left < right){
        	while(left < right && array[left] <= array[pivot]){
            	left++;
        	}
            
            while(left < right && array[right] >= array[pivot]){
                right--;
            }
            
            //交换array[left] 和 array[right]
            //交换前array[left] 比 array[pivot]大同时array[right]比array[pivot]小
            if(left < right){
            	int temp = array[left];
            	array[left] = array[right];
            	array[right] = temp;
            }
    
            //交换后array[left] 比 array[pivot]小同时array[right]比array[pivot]大
            
        }//while循环结束的时候left一定是等于right的，此时array[left]即array[right]一定是大于等于array[pivot]
        //理由：
        //1.left++导致left ==right,上次循环结束array[left]和array[right]交换之后array[right]是大于(如果发生交换的话)等于(如果没有发生交换)arry[pivot]的
        //2.right--导致left == right，本次循环中array[left]一定是大于arry[pivot]的
        //因此，无论如何while循环结束也即一次partition操作结束的时候array[left]也即array[right]一定是大于等于array[pivot]的
        
        int temp = array[left];
        array[left] = array[pivot];
        array[pivot] = temp;
        
    return left;//由于left == right，所以return right;也可以
    }
```
    
    - 快速排序的代码：
    
        ```java
        public void quickSort(int[] array){
            quickSortHelper(array, 0, array.length - 1);
        }
        public void quickSortHelper(int[] array, int left, int right){
            if(left >= right){
                return;
            }
            int index = partition(array, left, right);
            quickSortHelper(array,left, index - 1);
            quickSortHelper(array, index + 1, right);
        }
        ```


​          

- 性能分析：
    - 时间复杂度：最坏情况下O(N^2)，平均情况下O(NlongN)        
    - 空间复杂度：最坏情况下O(N),平均情况下O(logN)    
    - 稳定性：不稳定
