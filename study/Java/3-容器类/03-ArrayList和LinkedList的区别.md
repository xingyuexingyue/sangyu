1. ArrayList是实现了基于动态数组的数据结构，而LinkedList是基于链表的数据结构
2. 对于随机访问get和set，ArrayList要优于LinkedList，因为LinkedList要移动指针；
3. 对于添加和删除操作add和remove，LinkedList要比ArrayList快，因为ArrayList要移动数据；

## ArrayList中的随机访问、添加和删除部分源码如下：

```
//获取index位置的元素值
public E get(int index) {
    rangeCheck(index); //首先判断index的范围是否合法
 
    return elementData(index);
}
 
//将index位置的值设为element，并返回原来的值
public E set(int index, E element) {
    rangeCheck(index);
 
    E oldValue = elementData(index);
    elementData[index] = element;
    return oldValue;
}
 
//将element添加到ArrayList的指定位置
public void add(int index, E element) {
    rangeCheckForAdd(index);
 
    ensureCapacityInternal(size + 1);  // Increments modCount!!
    //将index以及index之后的数据复制到index+1的位置往后，即从index开始向后挪了一位
    System.arraycopy(elementData, index, elementData, index + 1,
                     size - index); 
    elementData[index] = element; //然后在index处插入element
    size++;
}
 
//删除ArrayList指定位置的元素
public E remove(int index) {
    rangeCheck(index);
 
    modCount++;
    E oldValue = elementData(index);
 
    int numMoved = size - index - 1;
    if (numMoved > 0)
        //向左挪一位，index位置原来的数据已经被覆盖了
        System.arraycopy(elementData, index+1, elementData, index,
                         numMoved);
    //多出来的最后一位删掉
    elementData[--size] = null; // clear to let GC do its work
 
    return oldValue;
}
```

##    LinkedList中的随机访问、添加和删除部分源码如下：

```
//获得第index个节点的值
public E get(int index) {
	checkElementIndex(index);
	return node(index).item;
}
 
//设置第index元素的值
public E set(int index, E element) {
	checkElementIndex(index);
	Node<E> x = node(index);
	E oldVal = x.item;
	x.item = element;
	return oldVal;
}
 
//在index个节点之前添加新的节点
public void add(int index, E element) {
	checkPositionIndex(index);
 
	if (index == size)
		linkLast(element);
	else
		linkBefore(element, node(index));
}
 
//删除第index个节点
public E remove(int index) {
	checkElementIndex(index);
	return unlink(node(index));
}
 
//定位index处的节点
Node<E> node(int index) {
	// assert isElementIndex(index);
	//index<size/2时，从头开始找
	if (index < (size >> 1)) {
		Node<E> x = first;
		for (int i = 0; i < index; i++)
			x = x.next;
		return x;
	} else { //index>=size/2时，从尾开始找
		Node<E> x = last;
		for (int i = size - 1; i > index; i--)
			x = x.prev;
		return x;
	}
}
```

从源码可以看出，ArrayList想要get(int index)元素时，直接返回index位置上的元素，而LinkedList需要通过for循环进行查找，虽然LinkedList已经在查找方法上做了优化，比如index < size / 2，则从左边开始查找，反之从右边开始查找，但是还是比ArrayList要慢。这点是毋庸置疑的。
        ArrayList想要在指定位置插入或删除元素时，主要耗时的是System.arraycopy动作，会移动index后面所有的元素；LinkedList主耗时的是要先通过for循环找到index，然后直接插入或删除。这就导致了两者并非一定谁快谁慢，下面通过一个测试程序来测试一下两者插入的速度：


## 比较两个 ArrayList 中不同的元素

```java
/**
  * 获取两个 List 的不同元素（假设 List 自身不存在重复元素）
  */
public class MyTest{
    public static void main(String[] args){
        List<String> list1 = new ArrayList<String>();
        List<String> list2 = new ArrayList<String>();
        for (int i = 0; i < 30000; i++){
            list1.add("test" + i);
        }
        
        for (int i = 0; i < 80000; i++){
            list2.add("test" + i * 2);
        }
    }
        
    // 方法1：两层遍历查找
    public static List<String> getDiff1(List<String> list1,List<String> list2){
        List<String> diffList = new ArrayList<String>();
        for (String str : list1){
            if (!list2.contains(str)){
                diffList.add(str);
            }
        }
        return diff;
    }
    
    // 方法2：两层遍历查找
    public static List<String> getDiff2(List<String> list1,List<String> list2){
        list1.retainAll(list2); // 返回值是 boolean
        return list1;
    }
    
    // 方法3，用 Map 存放 List1 和 List2 的元素作为 key，value 为其在 List1 和 List2 中出现的次数
    // 出现次数为1的即为不同元素
    public static List<String> getDiff3(List<String> list1,List<String> list2){
        List<String> diffList = new ArrayList<String>();
        Map<String,Integer> map = new HashMap<String,Integer>();
        
        for (String str : list1){
            map.put(str, 1);
        }
        
        for (String str : list2){
            Integer count = map.get(string);
            if(count != null){
                map.put(str,++count);
                continue;
            }
            map.put(str,1);
        }
        
        for (Map.Entry<String,Integer> entry : map.entrySet()){
            if(entry.getValue() == 1){
                diffList.add(entry.getKey());
            }
        }
        return diffList;
    }
    
    // 优化方法3，减少put次数
    public static List<String> getDiff4(List<String> list1,List<String> list2){
        List<String> diff = new ArrayList<String>();
        Map<String,Integer> map = new HashMap<String,Integer>();
        List<String,Integer> maxList = list1;
        List<String,Integer> minList = list2;
        if (list2.size() > list1.size()){
            maxList = list2;
            minList = list1;
        }
        
        for (String string : maxList){
            map.put(string, 1);
        }
        
        for (String string : minList){
            Integer count = map.get(string);
            if (count != null){
                map.put(string,++count);
                continue;
            }
            map.put(string, 1);
        }
        
        for (Map.Entry<String,Integer> entry : map.entrySet()){
            if(entry.getValue() == 1){
                diff.add(entry.getKey());
            }
        }
        return diff;
    }

}
```

## List.equals

List.equals指出，如果两个列表包含相同的大小，内容和元素顺序，则它们是相等的。

您可以使用这两个列表进行排序Collections.sort()，然后使用equals方法。稍好一点的解决方案是首先检查它们在订购前是否具有相同的长度，如果它们不是，则它们不相等，然后进行排序，然后使用等于。例如，如果你有两个字符串列表，它会是这样的：

```
public  boolean equalLists(List<String> one, List<String> two){     
    if (one == null && two == null){
        return true;
    }

    if((one == null && two != null) 
      || one != null && two == null
      || one.size() != two.size()){
        return false;
    }

    //to avoid messing the order of the lists we will use a copy
    //as noted in comments by A. R. S.
    one = new ArrayList<String>(one); 
    two = new ArrayList<String>(two);   

    Collections.sort(one);
    Collections.sort(two);      
    return one.equals(two);
}
```

## ArrayList - 如何判断两个列表是否相等，顺序无关紧要

例

```
ArrayList<String> listA = {"a", "b", "c"}
ArrayList<String> listB = {"b", "c", "a"}
```

listA.containsAll(listB) && listB.containsAll(listA)
