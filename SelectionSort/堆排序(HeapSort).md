# 堆排序(HeapSort)

- 堆排序是基于堆(假设用大根堆)的特性进行排序的方法(大根堆的堆顶元素是整个堆中值最大的那个元素)

- 基本思想：

    - 首先将待排序序列构造成一个堆，此时变**选出了**堆中所有记录的最大者即堆顶记录。

    - 然后，将堆顶记录与堆中的最后一个元素进行交换，同时对剩下的未排序元素进行向下调整

    - 直到堆中只有一个记录

        ```java
        public void heapSort(int[] array){
            //1.先建堆
            createHeap(array);
            int heapSize = array.length;//用heapSize来记录待排序的元素个数
            for(int i = 0; i < array.length - 1; i++){//进行n - 1趟便可完成排序
            	//2.交换堆顶元素与待排序的最后一个元素
                int temp = array[heapSize - 1];
                array[heapSize - 1] = array[0];
                array[0] = temp;
                //3.更新待排序元素的个数
                heapSize--;
                //4.从下标0开始，进行一次向下调整
                siftDown(array, heapSize, 0);
            }
        }
        public void createHeap(int[] array){
            //从最后一个非叶子结点开始，从后往前依次遍历的同时进行向下调整
            for(int i = (array.length - 1 - 1) / 2; i >= 0; i--){
                siftDown(array, array.length, i);
            }
        }
        
        public void siftDown(int[] array, int size, int index){
            int parent = index;
            int child = parent * 2 + 1;
            
            while(child < size){
                //让child指向parent的左右子树的最大者
                if(child + 1 < size && array[child + 1] > array[child]){
                    child = child + 1;
                }
                //如果array[parent]小于左右子树的最大者array[child]
                if(array[parent] < array[child]){
                    int temp = array[parent];
                    array[parent] = array[child];
                    array[child] = temp;
                }else{
                    break;
                }
                
                parent = child;
                child = parent * 2 + 1;
            }
        }
        ```

        

        - 时间复杂度：O(NlogN)
        - 空间复杂度：O(1)
        - 稳定性：不稳定