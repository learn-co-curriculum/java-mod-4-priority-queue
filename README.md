# PriorityQueue

## Learning Goals

- Understand the performance considerations for PriorityQueue.
- Create, insert, retrieve, and remove elements from the PriorityQueue.
- Use a Comparator with a PriorityQueue.

## What is a PriorityQueue

A PriorityQueue is an implementation of the Heap data structure. It keeps track
of the smallest or largest element in the structure which allows retrieval in
ascending or descending order.

A PriorityQueue is best visualized as binary tree but it uses an array to keep
track of its elements under the hood instead of the usual linked nodes used for
Tree data structures. This allows insertion and extraction in O(log n) time.

## Creating a PriorityQueue

A PriorityQueue can be initialized as empty or with a Comparator.

### Initialize an Empty PriorityQueue

When a PriorityQueue is initialized using the default constructor it creates a
min heap, i.e., the smallest element is always at the top.

```java
import java.util.PriorityQueue;

public class PriorityQueueMinExample {
    public static void main(String[] args) {
        PriorityQueue<Integer> temperatures = new PriorityQueue<>();
        temperatures.add(20);
        temperatures.add(12);
        temperatures.add(5);
        temperatures.add(23);

        System.out.println(temperatures.peek()); // -> 5
    }
}
```

The `peek` method accesses the smallest element but doesn’t remove it from the
PriorityQueue.

### Initialize a PriorityQueue with a Comparator

A Comparator can be used to change the default comparison order of element
storage. For example, in order to retrieve the maximum temperature we could use
the following code:

```java
import java.util.Comparator;
import java.util.PriorityQueue;

class MaxComparator implements Comparator<Integer> {
    @Override
    public int compare(Integer o1, Integer o2) {
        if (o1 > o2) return -1;
        if (o1 < o2) return 1;
        return 0;
    }
}

public class PriorityQueueMaxExample {
    public static void main(String[] args) {
        PriorityQueue<Integer> temperatures = new PriorityQueue<>(new MaxComparator());
        temperatures.add(20);
        temperatures.add(12);
        temperatures.add(5);
        temperatures.add(23);

        System.out.println(temperatures.peek()); // -> 23
    }
}
```

Notice that the `(o1 < o2)` comparison is returning `-1` to indicate that o1
comes before o2 in the ordering. A cleaner way to write the Comparator is to use
the `compareTo` method:

```java
import java.util.Comparator;
import java.util.PriorityQueue;

class MaxComparator implements Comparator<Integer> {
    @Override
    public int compare(Integer o1, Integer o2) {
        return o2.compareTo(o1);
    }
}

public class PriorityQueueMaxExample {
    public static void main(String[] args) {
        PriorityQueue<Integer> temperatures = new PriorityQueue<>(new MaxComparator());
        temperatures.add(20);
        temperatures.add(12);
        temperatures.add(5);
        temperatures.add(23);

        System.out.println(temperatures.peek()); // -> 23
    }
}
```

## Adding Elements

The PriorityQueue has two methods for adding elements:

- `add(E e)`
- `offer(E e)`

They perform exactly the same way for PriorityQueue. The `add` method is from
the `Collection` interface and the `offer` method is from the Queue interface.

Generally, the `add` method throws an exception when the class overriding
reaches max capacity and the `offer` method returns `false`. Since the
PriorityQueue is unbounded, it doesn’t have a defined capacity which means both
of the methods work the same way. These methods perform in O(log n) time
complexity.

## Removing Elements

There are two methods for removing elements:

- `poll()`
- `remove(Object o)`

Recall that a heap is best visualized as a binary tree where the root element is
always the smallest or largest element depending on the Comparator you’re using.
The `poll` method removes and returns the element at the top of the tree.

Although the top element can be accessed in O(1) time the removal is still O(log
n). This is because the underlying tree has to be restructured to bring the
smallest element at the top again. Restructuring costs O(log n) which is why the
`poll` method has an overall time complexity of O(log n).

```java
public class PriorityQueueMinExample {
    public static void main(String[] args) {
        PriorityQueue<Integer> temperatures = new PriorityQueue<>();
        temperatures.add(20);
        temperatures.add(12);
        temperatures.add(5);
        temperatures.add(23);

        System.out.println(temperatures.poll()); // -> 5
    }
}
```

The `remove` method takes in a value, searches the PriorityQueue for that value,
removes the value and restructures the tree. It returns `true` if the tree was
restructured and `false` otherwise.

## References

- [PriorityQueue Java Docs](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/PriorityQueue.html)
