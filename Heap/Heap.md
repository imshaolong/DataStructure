# 堆(heap)

- 堆(heap)是具有如下性质的完全二叉树：

    - 如果每个结点的值都小于等于其左右孩子结点的值，此时把这棵完全二叉树称为小根堆。
    - 如果每个结点的值都大于等于其左右孩子结点的值，此时把这个完全二叉树称为大根堆。

- 从堆的定义可知，一个完全二叉树如果是堆，则根节点（称为堆顶）一定是当前堆中所有结点的最大者（大根堆）或最小者（小根堆）。

- 堆的基本操作：

    - 堆的调整操作：给定一个数组，这个数组不满足堆的特性，经过一定的调整操作之后，把它变成一个堆

        - 向下调整（下沉式调整）：要求在这个完全二叉树中，除了根节点之外其余结点都满足大堆的要求。此时才能进行向下调整。

        ```java
        //堆是一个完全二叉树，通常使用数组来表示
        //数组中位于[0, size)之间的元素是属于堆中的元素
        //index表示从哪个下标出发进行调整
        public void siftDown(int[] array,int size, int index){
            int parent = index;
        	//根据父节点的下边找到左子树的根节点的下标
            int child = 2 * parent + 1;
            //循环的条件：如果child对应的结点存在，就继续调整如果超过size就说明当前的parent已经是叶子节点，就表示调整已经完成了，再没有子节点需要调整了
            while(child < size){
                //再去找右子树的对应结点
                if(child + 1 < size && array[child + 1] > array[parent]){
                    child = child + 1;
                }
                //child经过上面if语句块的处理之后，已经不知道child是指向当前parent的左子树还是右子树
                //child现在肯定是左右子树中值比较大的那个
                
                //接下来就可以拿刚才child位置的元素和parent位置的元素进行对比，看看是否符合大堆的定义
                //如果不符合大堆的定义，我们就交换child和parent位置的元素
                if(array[child] > array[parent]){
                	int temp = array[parent];
                    array[parent] = array[child];
                    array[child] = temp;
                }else{
                    //当前的child和parent的关系已经符合大堆的要求，说明已经调整完毕了
                    break;
                }
                //下次循环之前，需要更新parent和child的值
                parent = child;
                child = 2 * parent + 1;
                
            }
                
        }
        ```

        

        - 向上调整（上浮式调整）：

    - 建堆：随便给一个数组都能够创建出一个堆

        - 从后往前遍历数组，从最后一个结点的父节点出发(最后一个非叶子结点)依次从当前位置向下调整。

            ```java
            public void createHeap(int[] array, int size){
                //从后往前遍历，从最后一个非叶子结点出发，依次向下进行调整
                //size -1 得到的是最后一个元素的下标
                //(size -1 -1) / 2得到的是最后一个元素的父节点的下标
                for(int i = (size - 1 - 1) / 2; i >= 0; i--){
                    shitDown(array, size, i);
                }
            }
            ```

        - 如果是基于向下调整的方式建堆，必须从后往前遍历。

        - 如果是基于向上调整的方式建堆，必须从前往后遍历。

        - 下面在实现优先级队列的过程中实现堆的其他操作。

# 优先级队列(Priority Queue)

- 优先级队列(Priority Queue)：是按照某种优先级进行排列的队列，优先级越高的元素出队越早，优先级相同者按照先进先出的原则进行处理。实现优先级队列的核心数据结构就是堆。

    ```java
    public class MyPriorityQueue{
        private int[] array = new int[100];//暂时不考虑扩容
        private int size = 0;//[0, size)b表示有效元素的区间
        //入队
        public void offer(int x){
            //1.先把x放到数组元素的末尾。
            array[size] = x;
            size++;
            
            //2.从x所在位置开始进行向上调整
            //array表示用来承载元素的数组
            //size表示数组中有效元素的个数
            //size - 1表示从那个下标开始进行向上调整 
            siftUp(array, size, size - 1);
        }
        public void siftUp(int[] array, int size, int index){
            int child = index;
            int parent = (child - 1) / 2;
            //如果child为0，说明child已经是根节点了，根节点就没有父节点
            //调整到这里就已经到顶了
            while(child > 0){
            	//比较当前child和parent之间的大小关系，看看是否符合大堆
                if(array[parent] < array[child]){
                    //交换父子元素的内容
                    int temp = array[parent];
                    array[parent] = array[child];
                    array[child] = temp;
                }else{
                    break;
                }
                child = parent;
                parent = (child - 1) / 2;
            }
        }
        
        //出队
        public Integer poll(){
            if(size <= 0){
                return null;
            }
            int ret = array[0];
            //1.把最后一个元素赋值到array[0]
            array[0] = array[size - 1];
            //2.尾删最后一个元素
            size--;
            //3.从index = 0开始进行一次向下调整
            siftDown(array,size,0);
            return ret;
        }
        
        public void shiftDown(int[] array, int size, int index){
            int parent = index;
            int child = 2 * parent + 1;
            while(child < size){
                if(child + 1 < size && array[child + 1] > array[child]){
                    child = child + 1;
                }
                if(array[child] > array[parent]){
                    int temp = array[parent];
                    array[parent] = array[child];
                    array[child] = temp;
                }else{
                    break;
                }
                parent = child;
                child = 2 * parent + 1;
            }
        }
        
        //取队首元素
        public Integer peek(){
            if(size == 0){
                return null;
            }
            return array[0];
        }
        //判空
        public boolean isEmpty(){
            return size == 0;
        }
        
        
        public static void main(String[] args){
            MyPriorityQueue queue = new MyPriorityQueue();
            queue.offer(1);
            queue.offer(2);
            queue.offer(3);
            queue.offer(4);
            queue.offer(5);
            queue.offer(6);
            queue.offer(7);
            queue.offer(8);
            queue.offer(9);
            while(!queue.isEmpty()){
                System.out.println(queue.poll());
            }
        }
    }
    ```

    

