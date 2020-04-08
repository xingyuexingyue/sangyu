```java
public class MyArrayList<E> {

    private Object[] elementData;
    private int size;
    private static final int DEFAULT_CAPCAITY = 10; // 定义一个默认长度

    public MyArrrayList() {
        elementData = new Object[DEFAULT_CAPCAITY];
    }

    public MyArrrayList(int capacity) {
        if (capacity < 0) {
            throw new RuntimeException("容器的容量不能为负数");
        } else if (capacity == 0) {
            elementData = new Object[DEFAULT_CAPCAITY];
        } else {
            elementData = new Object[capacity];
        }
    }

    public void add(E element) {
        // 扩容的时机
        if (size == elementData.length) {
            // 扩容操作
            Object[] newArray = new Object[elementData.length + (elementData.length >> 1)]; // Object[] newArray = new Object[elementData.length<<1]，<< 左移，相当于*2,这里使用增加一半的方式，避免一次增加过大的长度,使用位运算符一定要奥注意它的优先级问题，要使用括号，因为位运算符的优先级很低
            System.arraycopy(elementData, 0, newArray, 0, elementData.length);
            elementData = newArray; // 拷贝后旧的数组会被垃圾回收掉
        }
        elementData[size++] = element;
    }

    public E get(int index) {
        checkRange(index);
        return (E) elementData[index];
    }

    public void set(E element, int index) {
        checkRange(index);
        elementData[index] = element;
    }

    public void checkRange(int index) {
        if (index < 0 || index > size - 1) {
            throw new RuntimeException("索引不合法：" + index);
        }
    }

    public void remove(E element) {
        for (int i = 0; i < size; i++) {
            if (element.equals(get(i))) { 
                remove(i);
            }
        }
    }

    public void remove(int index) {
        int numMoved = elementData.length - index - 1;
        if (numMoved > 0) {
            System.arraycopy(elementData, index + 1, elementData, index, numMoved);
        }
        // 不管大于0还是小于等于0都需要将最后一个值置为null，并将size-1
        elementData[--size] = null;
    }

    public int size() {
        return size;
    }

    public boolean isEmpty() {
        return size == 0 ? true : false;
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append("[");
        for (int i = 0; i < size; i++) {
            sb.append(elementData[i] + ",");
        }
        sb.setCharAt(sb.length() - 1, ']');
        return sb.toString();
    }
}
```