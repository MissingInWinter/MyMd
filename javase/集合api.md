

# 集合api

![Collection](images\Collection.png)



![Snipaste_2022-12-12_16-30-39](images\Snipaste_2022-12-12_16-30-39.png)











## 1.collection

| 方法名称                             | 说明                             |
| ------------------------------------ | -------------------------------- |
| public  boolean add(E e)             | 把给定的对象添加到当前集合中     |
| public  void clear()                 | 清空集合中所有的元素             |
| public  boolean remove(E e)          | 把给定的对象在当前集合中删除     |
| public  boolean contains(Object obj) | 判断当前集合中是否包含给定的对象 |
| public  boolean isEmpty()            | 判断当前集合是否为空             |
| public  int size()                   | 返回集合中元素的个数。           |
| public  Object[] toArray()           | 把集合中的元素，存储到数组中     |

| 方法名称                        | 说明                                                        |
| ------------------------------- | ----------------------------------------------------------- |
| **Iterator<E>**  **iterator()** | 返回集合中的迭代器对象，该迭代器对象默认指向当前集合的0索引 |

| 方法名称          | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| boolean hasNext() | 询问当前位置是否有元素存在，存在返回true ,不存在返回false    |
| E  next()         | 获取当前位置的元素，并同时将迭代器对象移向下一个位置，注意防止取出越界。 |

## 2.List

| 方法名称                       | 说明                                   |
| ------------------------------ | -------------------------------------- |
| void add(int  index,E element) | 在此集合中的指定位置插入指定的元素     |
| E remove(int  index)           | 删除指定索引处的元素，返回被删除的元素 |
| E set(int index,E  element)    | 修改指定索引处的元素，返回被修改的元素 |
| E get(int  index)              | 返回指定索引处的元素                   |

List的sort方法也很实用



### 2.1LinkedList

LinkedList也是有索引的、以上方法也是适用的

| 方法名称                   | 说明                             |
| -------------------------- | -------------------------------- |
| public  void addFirst(E e) | 在该列表开头插入指定的元素       |
| public  void addLast(E e)  | 将指定的元素追加到此列表的末尾   |
| public  E getFirst()       | 返回此列表中的第一个元素         |
| public  E getLast()        | 返回此列表中的最后一个元素       |
| public  E removeFirst()    | 从此列表中删除并返回第一个元素   |
| public  E removeLast()     | 从此列表中删除并返回最后一个元素 |

另有Colllections工具类

## 3.map

Map祖宗接口、其实现类均可继承使用其api

| 方法名称                            | 说明                                 |
| ----------------------------------- | ------------------------------------ |
| V  put(K key,V value)               | 添加元素                             |
| V  remove(Object key)               | 根据键删除键值对元素                 |
| void  clear()                       | 移除所有的键值对元素                 |
| boolean containsKey(Object key)     | 判断集合是否包含指定的键             |
| boolean containsValue(Object value) | 判断集合是否包含指定的值             |
| boolean isEmpty()                   | 判断集合是否为空                     |
| int  size()                         | 集合的长度，也就是集合中键值对的个数 |

| Set<K>  keySet() | 获取所有键的集合 |
| ---------------- | ---------------- |

| V  get(Object key) | 根据键获取值 |
| ------------------ | ------------ |



| 方法名称                       | 说明                     |
| ------------------------------ | ------------------------ |
| Set<Map.Entry<K,V>> entrySet() | 获取所有键值对对象的集合 |

| K getKey()   | 获得键 |
| ------------ | ------ |
| V getValue() | 获取值 |



maps.forEach((k , v) -> {
    System.out.println(k +"----->" + v);
});
