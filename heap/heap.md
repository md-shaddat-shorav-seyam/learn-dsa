Here’s a full guide to **heap**, **max heap**, **min heap**, **heapify**, and **heap sort** with **concept**, **example**, **pseudocode**, and **C++ code**.

---

# 1) What is a Heap?

A **heap** is a special type of **complete binary tree**.

## Complete binary tree

A binary tree where:

* all levels are completely filled except possibly the last level
* the last level is filled from **left to right**

Because of this structure, a heap is usually stored in an **array**, not with tree nodes.

---

# 2) Array representation of Heap

If a heap is stored in array `arr`:

For index `i`:

* **Left child** = `2*i + 1`
* **Right child** = `2*i + 2`
* **Parent** = `(i - 1) / 2`

Example array:

```text
Index:  0  1  2  3  4  5  6
Value: 50 30 40 10 20 35 38
```

Tree:

```text
          50
        /    \
      30      40
     /  \    /  \
   10   20  35  38
```

---

# 3) Types of Heap

There are mainly two types:

## A) Max Heap

In a **max heap**, every parent is **greater than or equal to** its children.

### Rule

```text
parent >= left child
parent >= right child
```

### Example

```text
          90
        /    \
      70      60
     /  \    /  \
   40   50  20  30
```

Array form:

```cpp
[90, 70, 60, 40, 50, 20, 30]
```

Here:

* 90 > 70, 60
* 70 > 40, 50
* 60 > 20, 30

So this is a **max heap**.

---

## B) Min Heap

In a **min heap**, every parent is **smaller than or equal to** its children.

### Rule

```text
parent <= left child
parent <= right child
```

### Example

```text
          10
        /    \
      20      30
     /  \    /  \
   40   50  60  70
```

Array form:

```cpp
[10, 20, 30, 40, 50, 60, 70]
```

Here:

* 10 < 20, 30
* 20 < 40, 50
* 30 < 60, 70

So this is a **min heap**.

---

# 4) Important point about Heap

Heap does **not** mean fully sorted.

Example max heap:

```cpp
[100, 50, 80, 20, 40, 70, 60]
```

This is valid because each parent is bigger than its children.

But array is not sorted like:

```cpp
[20, 40, 50, 60, 70, 80, 100]
```

So heap only guarantees:

* root is max in max heap
* root is min in min heap

---

# 5) Heap operations

Common operations:

* insert
* delete root
* heapify
* build heap
* heap sort

You asked mainly for:

* max heap
* min heap
* heapify
* heap sort

So let’s focus there.

---

# 6) What is Heapify?

**Heapify** means:
adjusting a tree/subtree so that it satisfies heap property.

There are two common meanings people use:

## A) Heapify down / sift down

Used when a node may violate heap property with its children.

Example:

* after deletion
* while building heap
* in heap sort

## B) Heapify up / sift up

Used when a newly inserted node may violate heap property with its parent.

---

# 7) Max Heapify

## Idea

Suppose root of a subtree may be smaller than one of its children.
Then:

1. compare root with left and right child
2. find largest
3. if root is not largest, swap
4. continue heapifying downward

---

## Example of Max Heapify

Array:

```cpp
[10, 50, 40, 20, 30]
```

Tree:

```text
          10
        /    \
      50      40
     /  \
   20   30
```

This is **not** a max heap because `10 < 50`.

### Step 1

Compare 10, 50, 40
Largest = 50

Swap 10 and 50:

```cpp
[50, 10, 40, 20, 30]
```

Tree:

```text
          50
        /    \
      10      40
     /  \
   20   30
```

### Step 2

Now heapify node `10`

Compare 10, 20, 30
Largest = 30

Swap 10 and 30:

```cpp
[50, 30, 40, 20, 10]
```

Tree:

```text
          50
        /    \
      30      40
     /  \
   20   10
```

Now it is a max heap.

---

# 8) Min Heapify

Same idea, but now choose the **smallest** child.

## Example

Array:

```cpp
[50, 20, 30, 40, 10]
```

Tree:

```text
          50
        /    \
      20      30
     /  \
   40   10
```

This is not a min heap because 50 is too big.

### Step 1

Compare 50, 20, 30
Smallest = 20

Swap:

```cpp
[20, 50, 30, 40, 10]
```

### Step 2

Now heapify 50

Compare 50, 40, 10
Smallest = 10

Swap:

```cpp
[20, 10, 30, 40, 50]
```

### Step 3

But now root 20 > 10, so to make full min heap from root properly you would apply min-heap building bottom-up. Final valid min heap becomes:

```cpp
[10, 20, 30, 40, 50]
```

---

# 9) Pseudocode of Max Heapify

```text
MAX-HEAPIFY(arr, n, i)
    largest = i
    left = 2*i + 1
    right = 2*i + 2

    if left < n and arr[left] > arr[largest]
        largest = left

    if right < n and arr[right] > arr[largest]
        largest = right

    if largest != i
        swap arr[i] and arr[largest]
        MAX-HEAPIFY(arr, n, largest)
```

---

# 10) Pseudocode of Min Heapify

```text
MIN-HEAPIFY(arr, n, i)
    smallest = i
    left = 2*i + 1
    right = 2*i + 2

    if left < n and arr[left] < arr[smallest]
        smallest = left

    if right < n and arr[right] < arr[smallest]
        smallest = right

    if smallest != i
        swap arr[i] and arr[smallest]
        MIN-HEAPIFY(arr, n, smallest)
```

---

# 11) Build Max Heap

If an unsorted array is given, we can convert it into a max heap.

## Important idea

Leaf nodes are already heaps.
So start from the last non-leaf node and heapify backward to root.

Last non-leaf index:

```cpp
n/2 - 1
```

## Pseudocode

```text
BUILD-MAX-HEAP(arr, n)
    for i = n/2 - 1 down to 0
        MAX-HEAPIFY(arr, n, i)
```

---

## Example of Build Max Heap

Array:

```cpp
[4, 10, 3, 5, 1]
```

Start from index:

```cpp
n = 5
n/2 - 1 = 1
```

### i = 1

Node = 10
Children = 5, 1
Already okay

### i = 0

Node = 4
Children = 10, 3
Largest = 10
Swap:

```cpp
[10, 4, 3, 5, 1]
```

Now heapify index 1:

* 4 with children 5 and 1
* largest = 5
  Swap:

```cpp
[10, 5, 3, 4, 1]
```

Final max heap:

```cpp
[10, 5, 3, 4, 1]
```

---

# 12) Build Min Heap

## Pseudocode

```text
BUILD-MIN-HEAP(arr, n)
    for i = n/2 - 1 down to 0
        MIN-HEAPIFY(arr, n, i)
```

---

# 13) Heap Sort

Heap sort uses heap to sort array.

## Main idea

For **ascending order**:

1. build a **max heap**
2. root contains maximum
3. swap root with last element
4. reduce heap size
5. heapify root again
6. repeat

---

## Why it works

In max heap:

* biggest element is always at root
* move it to the end
* then fix the remaining heap
* repeat until array becomes sorted

---

# 14) Heap Sort Example

Array:

```cpp
[4, 10, 3, 5, 1]
```

## Step 1: Build max heap

After building:

```cpp
[10, 5, 3, 4, 1]
```

Tree:

```text
         10
       /    \
      5      3
     / \
    4   1
```

---

## Step 2: Swap root with last

Swap 10 and 1:

```cpp
[1, 5, 3, 4, 10]
```

Now heap size = 4
Heapify index 0:

Compare 1, 5, 3 → largest = 5
Swap:

```cpp
[5, 1, 3, 4, 10]
```

Heapify index 1:

Compare 1, 4 → largest = 4
Swap:

```cpp
[5, 4, 3, 1, 10]
```

---

## Step 3: Swap root with last of heap

Swap 5 and 1:

```cpp
[1, 4, 3, 5, 10]
```

Heap size = 3
Heapify index 0:

Compare 1, 4, 3 → largest = 4
Swap:

```cpp
[4, 1, 3, 5, 10]
```

---

## Step 4

Swap 4 and 3:

```cpp
[3, 1, 4, 5, 10]
```

Heap size = 2
Heapify root:
already okay

---

## Step 5

Swap 3 and 1:

```cpp
[1, 3, 4, 5, 10]
```

Sorted.

---

# 15) Pseudocode of Heap Sort

```text
HEAP-SORT(arr, n)
    BUILD-MAX-HEAP(arr, n)

    for i = n-1 down to 1
        swap arr[0] and arr[i]
        MAX-HEAPIFY(arr, i, 0)
```

Note:

* `i` becomes new heap size
* sorted part stays at the end

---

# 16) C++ Code for Max Heapify, Min Heapify, Build Heap, Heap Sort

```cpp
#include <bits/stdc++.h>
using namespace std;

// Print array
void printArray(const vector<int>& arr) {
    for (int x : arr) {
        cout << x << " ";
    }
    cout << endl;
}

// ---------------- MAX HEAPIFY ----------------
void maxHeapify(vector<int>& arr, int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < n && arr[left] > arr[largest]) {
        largest = left;
    }

    if (right < n && arr[right] > arr[largest]) {
        largest = right;
    }

    if (largest != i) {
        swap(arr[i], arr[largest]);
        maxHeapify(arr, n, largest);
    }
}

// ---------------- MIN HEAPIFY ----------------
void minHeapify(vector<int>& arr, int n, int i) {
    int smallest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < n && arr[left] < arr[smallest]) {
        smallest = left;
    }

    if (right < n && arr[right] < arr[smallest]) {
        smallest = right;
    }

    if (smallest != i) {
        swap(arr[i], arr[smallest]);
        minHeapify(arr, n, smallest);
    }
}

// ---------------- BUILD MAX HEAP ----------------
void buildMaxHeap(vector<int>& arr) {
    int n = arr.size();
    for (int i = n / 2 - 1; i >= 0; i--) {
        maxHeapify(arr, n, i);
    }
}

// ---------------- BUILD MIN HEAP ----------------
void buildMinHeap(vector<int>& arr) {
    int n = arr.size();
    for (int i = n / 2 - 1; i >= 0; i--) {
        minHeapify(arr, n, i);
    }
}

// ---------------- HEAP SORT ----------------
void heapSort(vector<int>& arr) {
    int n = arr.size();

    // Step 1: Build max heap
    buildMaxHeap(arr);

    // Step 2: One by one move current root to end
    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]);      // move current max to end
        maxHeapify(arr, i, 0);     // heapify reduced heap
    }
}

int main() {
    vector<int> arr = {4, 10, 3, 5, 1};

    cout << "Original array: ";
    printArray(arr);

    vector<int> maxHeapArr = arr;
    buildMaxHeap(maxHeapArr);
    cout << "Max Heap: ";
    printArray(maxHeapArr);

    vector<int> minHeapArr = arr;
    buildMinHeap(minHeapArr);
    cout << "Min Heap: ";
    printArray(minHeapArr);

    vector<int> sortedArr = arr;
    heapSort(sortedArr);
    cout << "Heap Sorted array: ";
    printArray(sortedArr);

    return 0;
}
```

---

# 17) Sample Output

For:

```cpp
{4, 10, 3, 5, 1}
```

Possible output:

```text
Original array: 4 10 3 5 1
Max Heap: 10 5 3 4 1
Min Heap: 1 4 3 5 10
Heap Sorted array: 1 3 4 5 10
```

---

# 18) Insert in Max Heap

When inserting:

1. put new element at the end
2. compare with parent
3. if greater than parent, swap upward
4. repeat until heap property is satisfied

This is called **heapify up** or **sift up**

## Pseudocode

```text
INSERT-MAX-HEAP(arr, value)
    append value to arr
    i = last index

    while i > 0 and arr[parent(i)] < arr[i]
        swap arr[i] and arr[parent(i)]
        i = parent(i)
```

---

## C++ code

```cpp
void insertMaxHeap(vector<int>& arr, int value) {
    arr.push_back(value);
    int i = arr.size() - 1;

    while (i > 0) {
        int parent = (i - 1) / 2;
        if (arr[parent] < arr[i]) {
            swap(arr[parent], arr[i]);
            i = parent;
        } else {
            break;
        }
    }
}
```

---

# 19) Delete root from Max Heap

When deleting max:

1. replace root with last element
2. remove last element
3. heapify down from root

## Pseudocode

```text
DELETE-MAX(arr)
    if heap empty
        return

    arr[0] = arr[last]
    remove last
    MAX-HEAPIFY(arr, size, 0)
```

---

## C++ code

```cpp
void deleteMax(vector<int>& arr) {
    int n = arr.size();
    if (n == 0) return;

    arr[0] = arr[n - 1];
    arr.pop_back();

    maxHeapify(arr, arr.size(), 0);
}
```

---

# 20) Time Complexity

## Max Heapify / Min Heapify

Height of heap is `log n`

So:

```text
Heapify = O(log n)
```

## Build Heap

```text
O(n)
```

Not `O(n log n)` in optimized bottom-up build.

## Heap Sort

* build max heap = `O(n)`
* each extraction = `O(log n)`
* done `n-1` times

So:

```text
Heap Sort = O(n log n)
```

---

# 21) Space Complexity

Heap sort is:

```text
O(1) extra space
```

because sorting happens in the same array.

That is one big advantage.

---

# 22) Advantages of Heap

* efficient access to largest/smallest element
* priority queue implementation
* in-place heap sort
* useful in graph algorithms like Dijkstra, Prim
* useful in scheduling systems

---

# 23) Disadvantages of Heap

* not fully sorted
* searching arbitrary element is not efficient
* heap sort is usually slower in practice than quicksort for many real cases
* not stable sorting

---

# 24) Heap vs BST

## Heap

* good for getting min/max fast
* root is special
* not sorted structure

## BST

* supports ordered searching better
* left < root < right
* in-order traversal gives sorted order

---

# 25) STL in C++ for Heap

C++ gives built-in heap through `priority_queue`.

## Max heap by default

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    priority_queue<int> pq;

    pq.push(10);
    pq.push(30);
    pq.push(20);

    cout << pq.top() << endl; // 30
}
```

## Min heap

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    priority_queue<int, vector<int>, greater<int>> pq;

    pq.push(10);
    pq.push(30);
    pq.push(20);

    cout << pq.top() << endl; // 10
}
```

---

# 26) Real-world use cases

## Max heap

* get highest priority task
* get largest number quickly
* top scorer / highest bid system

## Min heap

* get smallest value quickly
* shortest path algorithms
* merging sorted arrays/lists
* job scheduling by earliest time

## Heap sort

* when in-place sorting is needed
* when guaranteed `O(n log n)` worst-case is important

---

# 27) Short revision

## Max Heap

Parent is bigger than children.

## Min Heap

Parent is smaller than children.

## Heapify

Fix heap property at a node/subtree.

## Build Heap

Convert normal array into heap.

## Heap Sort

Build max heap, then repeatedly move max to end.

---

# 28) Very short pseudocode summary

## Max Heapify

```text
find largest among root, left, right
if root not largest:
    swap
    heapify again
```

## Min Heapify

```text
find smallest among root, left, right
if root not smallest:
    swap
    heapify again
```

## Heap Sort

```text
build max heap
repeat:
    swap first and last
    reduce heap size
    maxHeapify(root)
```

---

# 29) Interview-style question

Why do we use **max heap** for ascending heap sort?

Because:

* max heap gives largest element at root
* we place that largest element at the end
* repeat
* final order becomes ascending

For descending order, use **min heap**.

---

# 30) Descending heap sort idea

If you want **descending order**:

* build **min heap**
* repeatedly move minimum to end

---

If you want, I can give you next:
**“heap full topic with insert, delete, priority_queue, k-th largest, heap questions for interview/DSA exam”**.
