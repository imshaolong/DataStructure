# ShellSort

- 当待排序元素个数较少的时候插入排序的效率较高


- 当待排元素基本有序的时候插入排序的效率较高


- 基本思路：通过指定gap来将待排序元素分成若干组，对每组元素分别进行插入排序(因此shellSort本质上是分组插排)


- 性能分析：理论上来说，如果gap的大小选择合适的话，shellSort的时间复杂度可以达到O(N^1.3)


- 为了实现方便我们在这里将sheeSort的gap依次设定为：array.length / 2, array.length / 4, array.length / 8...


```java
//以升序排序为例
public void shellSort(int[] array){
    int gap = array.length / 2;
    while(gap > 1){
        shellSortHelper(array, gap);
        gap /= 2;
    }
    shellSortHelper(array, 1);
}
public void shellSortHelper(int[] array, int gap){
    for(int bound = gap; bound < array.length; bound++){
        int temp = array[bound];//temp用来暂存待排序的元素
        int cur = bound - gap;//cur指向有序序列的最后一个元素
        for(; cur >=0; cur -= gap){//从有序序列的最后一个元素向前寻找待排序元素的合适位置
        	if(array[cur] > temp){
                array[cur + gap] = array[cur];
            }else{
                break;
            }
        }
        array[cur + gap] = temp;
    }
}
```

- shellSort的性能分析：
    - 时间复杂度：O(N^2)，理论上如果gap选择合理的话可以达到O(N^1.3)
    - 空间复杂度：O(1)
    - 稳定性：不稳定