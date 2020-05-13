# BubbleSort

- 基本思路：

    - 通过引入bound变量，来将待排序区间分为[0, bound)和[bound, array.length)

    - 其中，[0, bound)为待排序区间，[bound, array.length)为已排序区间

    - 从前向后一次遍历待排序区间，如果当前元素比后面的元素大就交换两个元素的位置

        ```java
        public void bubbleSort(int[] array){
            //从前往后遍历的同时，用当前元素与后面的元素做比较，如果当前元素比后面的元素大就交换
            //[0, bound)待排序区间     [bound,array.length)已排序区间
            for(int bound = array.length - 1; bound >= 0; bound++){
                for(int cur = 0; cur < bound; cur++){
                    if(array[cur] > array[cur + 1]){
                        int temp = array[cur];
                        array[cur] = array[cur + 1];
                        array[cur + 1] = temp;
                    }
                }
            }
        }
        ```

        - 时间复杂度：O(N^2)
        - 空间复杂度：O(1)
        - 稳定性：稳定

