# 1. What is a Data Structure?

- A **data structure** (DS) is a way of organizing data so that it can be used effectively

# 2. Why Data Structures?

- They are essential ingredients in creating fast and powerful algorithms.
- They help to manage and organize data.
- They make code cleaner and easier to understand.

# 3. Abstract Data Type

- An abstract data type (ADT) is an abstraction of a data structure which provides only the interface to which a data structure must adhere to.
- The interface does not give any specific details about how something should be implemented or in what programming language.

## + Example

| Abstraction (ADT) | Implementation (DS)     |
| ----------------- | ----------------------- |
| List              | Dynamic Array           |
|                   | Linked List             |
| Queue             | Linked List based Queue |
|                   | Array based Queue       |
|                   | Stack based Queue       |
| Map               | Tree Map                |
|                   | Hash Map / Hash Table   |
| Vehicle           | Golf Cart               |
|                   | Bicycle                 |
|                   | Smart Car               |

# 4. Big O - Computational Complexity Analysis

- As programmers, we often find ourselves asking the same two questions over and over again:

  - How much **time** does this algorithm need to finish?

  - How much **space** does this algorithm need for its computation?

- Big-O Notation: Big-O Notation gives an upper bound of the complexity in the **worst case**, helping to quantify performance as the input size becomes **arbitrarily large**.

## + Clarification

- n - The size of the input

Complexities ordered in from smallest to largest

|                   | Big-O          |
| ----------------- | -------------- |
| Constant Time     | O(1)           |
| Logarithmic Time  | O(log(n))      |
| Linear Time       | O(n)           |
| Linearithmic Time | O(nlog(n))     |
| Quadric Time      | O(n^2)         |
| Cubic Time        | O(n^3)         |
| Exponential Time  | O(b^n),(b > 1) |
| Factorial Time    | O(n!)          |

## + Properties

- O(n + c) = O(n)
- O(cn) = O(n), c > 0

let f be a function that describes the running time of a particular algorithm for an input of size n:

- f(n) = 7log(n)^3 + 15n^2 + 2n^3 + 8
- O(f(n)) = O(n^3)

## + Example

### O(1)

```go
a := 1
b := 2
c := a + 5*b

i := 0
while i < 11 Do
    i = i + 1
```

### O(n)

```go
i := 0
while i < n Do
    i = i + 1

f(n) = n
O(f(n)) = O(n)

i := 0
while i < n Do
    i = i + 3

f(n) = n / 3
O(f(n)) = O(n)
```

### O(n^2)

- Both of the following run in quadratic time. The first may be obvious since n work done n times is n\*n = O(n^2), but what about the second one?

```go
For (i := 0; i < n; i = i + 1)
    For (j := 0; j < n; j = j + 1)

f(n) = n*n = n^2, O(f(n)) = O(n^2)

For (i := 0; i < n; i = i + 1)
    For (j := i; j < n; j = j + 1)

f(n) = (n) + (n-1) + (n-2) +...+ 3 + 2 + 1 = n*(n+1)/2 = O(n^2)
```

```go
i := 0
While i < n Do
    j := 0
    While j < 3*n Do
        j = j + 1
    j = 0
    While j < 2*n Do
        j = j + 1
    i = i + 1

f(n) = n * (3n + 2n) = 5n^2
O(f(n)) = O(n^2)
```

```go
i := 0
While i < 3 * n Do
    j := 10
    While j < 50 Do
        j = j + 1
    j = 0
    While j < n*n*n Do
        j = j + 2
    i = i + 1

f(n) = 3n * (40 + n^3/2) = 3n/40 + 3n^4/2
O(f(n)) = O(n^4)
```

### O(log(n))

- Suppose we have a sorted array and we want to find the index of a particular value in the array, if it exists. What is the time complexity of the following algorithm?

```go
low := 0
high := n-1
While low <= high Do
    mid := (low + high) / 2

    If array[mid] == value: return mid
    Else If array[mid] < value: low = mid + 1
    Else if array[mid] > value: high = mid - 1

return -1 // Value not found

Ans: O(log2(n)) = O(log(n))
```

### Others

- O(2^n) - Finding all subsets of a set
- O(n!) - Finding all permutations of a string
- O(nlog(n)) - Sorting using mergesort
- O(nm) - Iterating over all the cells in a matrix of size n by m

# 5. Static and Dynamic Arrays

- Static Array:

  - fixed-length, contain n elements
  - indexable from the range [0, n-1]

- Dynamic Array: The dynamic array can **grow** and **shrink** in size.

- When and Where is a static Array used?

  - Storing and accessing sequential data
  - Temporarily storing objects
  - Used by IO routines as buffers
  - Lookup tables and inverse lookup tables from a function
  - Used in dynamic programming tocache answers to subproblems

- Complexity

|           | Static Array | Dynamic Array |
| --------- | ------------ | ------------- |
| Access    | O(1)         | O(1)          |
| Search    | O(n)         | O(n)          |
| Insertion | N/A          | O(n)          |
| Appending | N/A          | O(1)          |
| Deletion  | N/A          | O(n)          |


- Implement Dynamic Array

```java
/**
 * Most of the time when you use an array it's to place integers inside of it, so why not have a
 * super fast integer only array? This file contains an implementation of an integer only array
 * which can outperform Java's ArrayList by about a factor of 10-15x! Enjoy!
 *
 * @author William Fiset, william.alexandre.fiset@gmail.com
 */
public class IntArray implements Iterable<Integer> {

  private static final int DEFAULT_CAP = 1 << 3;

  public int[] arr;
  public int len = 0;
  private int capacity = 0;

  // Initialize the array with a default capacity
  public IntArray() {
    this(DEFAULT_CAP);
  }

  // Initialize the array with a certain capacity
  public IntArray(int capacity) {
    if (capacity < 0) throw new IllegalArgumentException("Illegal Capacity: " + capacity);
    this.capacity = capacity;
    arr = new int[capacity];
  }

  // Given an array make it a dynamic array!
  public IntArray(int[] array) {
    if (array == null) throw new IllegalArgumentException("Array cannot be null");
    arr = java.util.Arrays.copyOf(array, array.length);
    capacity = len = array.length;
  }

  // Returns the size of the array
  public int size() {
    return len;
  }

  // Returns true/false on whether the array is empty
  public boolean isEmpty() {
    return len == 0;
  }

  // To get/set values without method call overhead you can do
  // array_obj.arr[index] instead, you can gain about 10x the speed!
  public int get(int index) {
    return arr[index];
  }

  public void set(int index, int elem) {
    arr[index] = elem;
  }

  // Add an element to this dynamic array
  public void add(int elem) {
    if (len + 1 >= capacity) {
      if (capacity == 0) capacity = 1;
      else capacity *= 2; // double the size
      arr = java.util.Arrays.copyOf(arr, capacity); // pads with extra 0/null elements
    }
    arr[len++] = elem;
  }

  // Removes the element at the specified index in this list.
  // If possible, avoid calling this method as it take O(n) time
  // to remove an element (since you have to reconstruct the array!)
  public void removeAt(int rm_index) {
    System.arraycopy(arr, rm_index + 1, arr, rm_index, len - rm_index - 1);
    --len;
    --capacity;
  }

  // Search and remove an element if it is found in the array
  // If possible, avoid calling this method as it take O(n) time
  public boolean remove(int elem) {
    for (int i = 0; i < len; i++) {
      if (arr[i] == elem) {
        removeAt(i);
        return true;
      }
    }
    return false;
  }

  // Reverse the contents of this array
  public void reverse() {
    for (int i = 0; i < len / 2; i++) {
      int tmp = arr[i];
      arr[i] = arr[len - i - 1];
      arr[len - i - 1] = tmp;
    }
  }

  // Perform a binary search on this array to find an element in O(log(n)) time
  // Make sure this array is sorted! Returns a value < 0 if item is not found
  public int binarySearch(int key) {
    int index = java.util.Arrays.binarySearch(arr, 0, len, key);
    // if (index < 0) index = -index - 1; // If not found this will tell you where to insert
    return index;
  }

  // Sort this array
  public void sort() {
    java.util.Arrays.sort(arr, 0, len);
  }

  // Iterator is still fast but not as fast as iterative for loop
  @Override
  public java.util.Iterator<Integer> iterator() {
    return new java.util.Iterator<Integer>() {
      int index = 0;

      public boolean hasNext() {
        return index < len;
      }

      public Integer next() {
        return arr[index++];
      }

      public void remove() {
        throw new UnsupportedOperationException();
      }
    };
  }

  @Override
  public String toString() {
    if (len == 0) return "[]";
    else {
      StringBuilder sb = new StringBuilder(len).append("[");
      for (int i = 0; i < len - 1; i++) sb.append(arr[i] + ", ");
      return sb.append(arr[len - 1] + "]").toString();
    }
  }

  // Example usage
  public static void main(String[] args) {

    IntArray ar = new IntArray(50);
    ar.add(3);
    ar.add(7);
    ar.add(6);
    ar.add(-2);

    ar.sort(); // [-2, 3, 6, 7]

    // Prints [-2, 3, 6, 7]
    for (int i = 0; i < ar.size(); i++) System.out.println(ar.get(i));

    // Prints [-2, 3, 6, 7]
    System.out.println(ar);
  }
}
```