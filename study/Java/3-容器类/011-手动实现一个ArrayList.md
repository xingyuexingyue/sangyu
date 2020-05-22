```java
public class MyArrayList06<E> {
    private Object[] elementData;
    private int size;
    private static final int DEFAULT_CAPCAITY = 10;

    public MyArrayList06() {
        elementData = new Object[DEFAULT_CAPCAITY];
    }

    public MyArrayList06(int capacity) {
        if (capacity < 0) {
            throw new RuntimeException("容器容量不能为负数");
        } else if (capacity == 0) {
            elementData = new Object[DEFAULT_CAPCAITY];
        } else {
            elementData = new Object[capacity];
        }
    }

    public int size() {
        return size;
    }

    public void checkIndex(int index) {
        if (index < 0 || index > size - 1) {
            throw new RuntimeException("索引不合法" + index);
        }
    }

    public void add(E element) {
        if (size == elementData.length) {
            Object[] arr = new Object[elementData.length + (elementData.length >> 1)];
            System.arraycopy(elementData, 0, arr, 0, elementData.length);
            elementData = arr;
        }
        elementData[size++] = element;
    }

    public void add(int index, E element) {
        checkIndex(index);
        if (size == elementData.length) {
            Object[] arr = new Object[elementData.length + 1];
            System.arraycopy(elementData, 0, arr, 0, elementData.length);
            elementData = arr;
        }
        System.arraycopy(elementData, index, elementData, index + 1, elementData.length - index - 1);
        elementData[index] = element;
    }

    public E get(int index) {
        checkIndex(index);
        return (E) elementData[index];
    }

    public void set(int index, E element) {
        checkIndex(index);
        elementData[index] = element;
    }

    public int indexOf(Object o) {
        if (o == null) {
            for (int i = 0; i < size; i++) {
                if (elementData[i] == null) {
                    return i;
                }
            }
        } else {
            for (int i = 0; i < size; i++) {
                if (o.equals(elementData[i])) {
                    return i;
                }
            }
        }
        return -1;
    }

    public boolean contains(Object o) {
        return !(indexOf(o) == -1);
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public void remove(E element) {
        for (int i = 0; i < size; i++) {
            if (element.equals(get(i))) {
                remove(i);
            }
        }
    }
    

    public void remove(int index) {
        checkIndex(index);
        int numMoved = elementData.length - index - 1;
        if (numMoved > 0){
            System.arraycopy(elementData, index + 1, elementData, index, numMoved);  
        }
        elementData[size--] = null;

    }

    @Override
    public String toString() {
        return "MyArrayList06{" +
                "elementData=" + Arrays.toString(elementData) +
                ", size=" + size +
                '}';
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