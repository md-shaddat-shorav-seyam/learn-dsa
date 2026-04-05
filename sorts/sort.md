Here’s a full but easy-to-follow guide to:

* Bubble Sort
* Selection Sort
* Insertion Sort
* Merge Sort
* Quick Sort

I’ll explain for each one:

* idea
* step-by-step example
* pseudocode
* C++ code
* time complexity
* when to use

---

# 1) Bubble Sort

## Main idea

Bubble sort compares **adjacent elements** and swaps them if they are in the wrong order.

After every pass, the **largest element “bubbles up”** to the end.

---

## Example

Array:

```text
[5, 1, 4, 2, 8]
```

### Pass 1

Compare 5 and 1 → swap

```text
[1, 5, 4, 2, 8]
```

Compare 5 and 4 → swap

```text
[1, 4, 5, 2, 8]
```

Compare 5 and 2 → swap

```text
[1, 4, 2, 5, 8]
```

Compare 5 and 8 → no swap

```text
[1, 4, 2, 5, 8]
```

Now 8 is in correct position.

---

### Pass 2

Compare 1 and 4 → no swap
Compare 4 and 2 → swap

```text
[1, 2, 4, 5, 8]
```

Compare 4 and 5 → no swap

Now 5 is fixed.

---

### Pass 3

Compare 1 and 2 → no swap
Compare 2 and 4 → no swap

Sorted.

---

## Pseudocode

```text
BubbleSort(A, n):
    for i = 0 to n-2:
        swapped = false
        for j = 0 to n-2-i:
            if A[j] > A[j+1]:
                swap(A[j], A[j+1])
                swapped = true
        if swapped == false:
            break
```

---

## C++ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

void bubbleSort(vector<int>& arr) {
    int n = arr.size();

    for (int i = 0; i < n - 1; i++) {
        bool swapped = false;

        for (int j = 0; j < n - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }

        if (!swapped) break;
    }
}

void printArray(const vector<int>& arr) {
    for (int x : arr) cout << x << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {5, 1, 4, 2, 8};

    bubbleSort(arr);
    printArray(arr);

    return 0;
}
```

---

## Complexity

* Best: **O(n)** if already sorted and optimized with `swapped`
* Average: **O(n²)**
* Worst: **O(n²)**
* Space: **O(1)**

---

## 특징 / Notes

* Very simple
* Not efficient for large arrays
* Stable sort

---

# 2) Selection Sort

## Main idea

Selection sort repeatedly finds the **smallest element** from the unsorted part and puts it at the beginning.

---

## Example

Array:

```text
[64, 25, 12, 22, 11]
```

### Pass 1

Smallest element is 11
Swap with first element

```text
[11, 25, 12, 22, 64]
```

### Pass 2

From remaining part `[25, 12, 22, 64]`, smallest is 12
Swap with second element

```text
[11, 12, 25, 22, 64]
```

### Pass 3

From `[25, 22, 64]`, smallest is 22
Swap

```text
[11, 12, 22, 25, 64]
```

Sorted.

---

## Pseudocode

```text
SelectionSort(A, n):
    for i = 0 to n-2:
        minIndex = i
        for j = i+1 to n-1:
            if A[j] < A[minIndex]:
                minIndex = j
        swap(A[i], A[minIndex])
```

---

## C++ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

void selectionSort(vector<int>& arr) {
    int n = arr.size();

    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;

        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }

        swap(arr[i], arr[minIndex]);
    }
}

void printArray(const vector<int>& arr) {
    for (int x : arr) cout << x << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {64, 25, 12, 22, 11};

    selectionSort(arr);
    printArray(arr);

    return 0;
}
```

---

## Complexity

* Best: **O(n²)**
* Average: **O(n²)**
* Worst: **O(n²)**
* Space: **O(1)**

---

## Notes

* Fewer swaps than bubble sort
* Not stable in normal form
* Good for understanding sorting basics

---

# 3) Insertion Sort

## Main idea

Insertion sort works like arranging playing cards in your hand.

It takes one element at a time and inserts it into the correct position in the already sorted part.

---

## Example

Array:

```text
[5, 2, 4, 6, 1, 3]
```

Start with first element as sorted:

```text
[5]
```

Insert 2 into sorted part:

```text
[2, 5, 4, 6, 1, 3]
```

Insert 4 into sorted part:

```text
[2, 4, 5, 6, 1, 3]
```

Insert 6:

```text
[2, 4, 5, 6, 1, 3]
```

Insert 1:

```text
[1, 2, 4, 5, 6, 3]
```

Insert 3:

```text
[1, 2, 3, 4, 5, 6]
```

---

## Pseudocode

```text
InsertionSort(A, n):
    for i = 1 to n-1:
        key = A[i]
        j = i - 1

        while j >= 0 and A[j] > key:
            A[j+1] = A[j]
            j = j - 1

        A[j+1] = key
```

---

## C++ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

void insertionSort(vector<int>& arr) {
    int n = arr.size();

    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;

        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }

        arr[j + 1] = key;
    }
}

void printArray(const vector<int>& arr) {
    for (int x : arr) cout << x << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {5, 2, 4, 6, 1, 3};

    insertionSort(arr);
    printArray(arr);

    return 0;
}
```

---

## Complexity

* Best: **O(n)** when already sorted
* Average: **O(n²)**
* Worst: **O(n²)**
* Space: **O(1)**

---

## Notes

* Stable
* Very good for **small arrays**
* Very good when data is **almost sorted**

---

# 4) Merge Sort

## Main idea

Merge sort uses **divide and conquer**.

It:

1. divides the array into two halves
2. sorts each half recursively
3. merges the sorted halves

---

## Example

Array:

```text
[38, 27, 43, 3, 9, 82, 10]
```

### Step 1: Divide

```text
[38, 27, 43, 3]   [9, 82, 10]
```

Then again:

```text
[38, 27] [43, 3] [9, 82] [10]
```

Then:

```text
[38] [27] [43] [3] [9] [82] [10]
```

---

### Step 2: Merge sorted parts

Merge [38] and [27]:

```text
[27, 38]
```

Merge [43] and [3]:

```text
[3, 43]
```

Merge [9] and [82]:

```text
[9, 82]
```

Merge [27, 38] and [3, 43]:

```text
[3, 27, 38, 43]
```

Merge [9, 82] and [10]:

```text
[9, 10, 82]
```

Final merge:

```text
[3, 9, 10, 27, 38, 43, 82]
```

---

## Pseudocode

```text
MergeSort(A, left, right):
    if left >= right:
        return

    mid = (left + right) / 2

    MergeSort(A, left, mid)
    MergeSort(A, mid+1, right)
    Merge(A, left, mid, right)

Merge(A, left, mid, right):
    create temporary arrays L and R

    copy left half into L
    copy right half into R

    i = 0, j = 0, k = left

    while i < size(L) and j < size(R):
        if L[i] <= R[j]:
            A[k] = L[i]
            i++
        else:
            A[k] = R[j]
            j++
        k++

    copy remaining elements of L
    copy remaining elements of R
```

---

## C++ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    vector<int> L(n1), R(n2);

    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];

    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];

    int i = 0, j = 0, k = left;

    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left >= right) return;

    int mid = left + (right - left) / 2;

    mergeSort(arr, left, mid);
    mergeSort(arr, mid + 1, right);
    merge(arr, left, mid, right);
}

void printArray(const vector<int>& arr) {
    for (int x : arr) cout << x << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {38, 27, 43, 3, 9, 82, 10};

    mergeSort(arr, 0, arr.size() - 1);
    printArray(arr);

    return 0;
}
```

---

## Complexity

* Best: **O(n log n)**
* Average: **O(n log n)**
* Worst: **O(n log n)**
* Space: **O(n)**

---

## Notes

* Stable
* Very efficient for large data
* Needs extra memory
* Good for linked lists and external sorting

---

# 5) Quick Sort

## Main idea

Quick sort also uses **divide and conquer**.

It chooses a **pivot** and rearranges the array so that:

* smaller elements go to the left
* bigger elements go to the right

Then it sorts left and right parts recursively.

---

## Example

Array:

```text
[10, 7, 8, 9, 1, 5]
```

Take last element as pivot = **5**

Rearrange around pivot:

```text
[1, 5, 8, 9, 10, 7]
```

Pivot 5 is now in correct place.

Now sort left part:

```text
[1]
```

Sort right part:

```text
[8, 9, 10, 7]
```

Take pivot = 7

After partition:

```text
[7, 9, 10, 8]
```

Continue until fully sorted:

```text
[1, 5, 7, 8, 9, 10]
```

---

## Partition concept

This is the heart of quick sort.

Example:

```text
[10, 7, 8, 9, 1, 5]
pivot = 5
```

We move all smaller elements before pivot.

Final result after partition:

```text
[1, 5, 8, 9, 10, 7]
```

Pivot index becomes fixed.

---

## Pseudocode

```text
QuickSort(A, low, high):
    if low < high:
        p = Partition(A, low, high)
        QuickSort(A, low, p-1)
        QuickSort(A, p+1, high)

Partition(A, low, high):
    pivot = A[high]
    i = low - 1

    for j = low to high-1:
        if A[j] < pivot:
            i = i + 1
            swap(A[i], A[j])

    swap(A[i+1], A[high])
    return i+1
```

---

## C++ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int partitionArray(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }

    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int pivotIndex = partitionArray(arr, low, high);

        quickSort(arr, low, pivotIndex - 1);
        quickSort(arr, pivotIndex + 1, high);
    }
}

void printArray(const vector<int>& arr) {
    for (int x : arr) cout << x << " ";
    cout << endl;
}

int main() {
    vector<int> arr = {10, 7, 8, 9, 1, 5};

    quickSort(arr, 0, arr.size() - 1);
    printArray(arr);

    return 0;
}
```

---

## Complexity

* Best: **O(n log n)**

* Average: **O(n log n)**

* Worst: **O(n²)**
  happens when pivot choice is bad, like already sorted array in poor implementation

* Space:

  * Average recursion stack: **O(log n)**
  * Worst recursion stack: **O(n)**

---

## Notes

* Usually very fast in practice
* Not stable in normal form
* In-place sort
* Widely used

---

# Comparison Table

| Sort           | Best       | Average    | Worst      | Space        | Stable |
| -------------- | ---------- | ---------- | ---------- | ------------ | ------ |
| Bubble Sort    | O(n)       | O(n²)      | O(n²)      | O(1)         | Yes    |
| Selection Sort | O(n²)      | O(n²)      | O(n²)      | O(1)         | No     |
| Insertion Sort | O(n)       | O(n²)      | O(n²)      | O(1)         | Yes    |
| Merge Sort     | O(n log n) | O(n log n) | O(n log n) | O(n)         | Yes    |
| Quick Sort     | O(n log n) | O(n log n) | O(n²)      | O(log n) avg | No     |

---

# Which one should you remember for exams/interviews?

## Bubble Sort

Remember for basic concept only.

## Selection Sort

Remember because it is easy and common in exams.

## Insertion Sort

Important for small or nearly sorted arrays.

## Merge Sort

Very important. Good for theory and interviews.

## Quick Sort

Very important. Frequently asked in interviews and coding problems.

---

# Easy intuition in one line

* **Bubble Sort** → push biggest to the end again and again
* **Selection Sort** → pick smallest and place it in front
* **Insertion Sort** → insert each element in its correct place
* **Merge Sort** → divide, sort, merge
* **Quick Sort** → choose pivot, split around pivot, repeat

---

# Full combined C++ code for all sorts

```cpp
#include <iostream>
#include <vector>
using namespace std;

// ---------- Bubble Sort ----------
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        bool swapped = false;
        for (int j = 0; j < n - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        if (!swapped) break;
    }
}

// ---------- Selection Sort ----------
void selectionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        swap(arr[i], arr[minIndex]);
    }
}

// ---------- Insertion Sort ----------
void insertionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;

        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }

        arr[j + 1] = key;
    }
}

// ---------- Merge Sort ----------
void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;

    vector<int> L(n1), R(n2);

    for (int i = 0; i < n1; i++) L[i] = arr[left + i];
    for (int j = 0; j < n2; j++) R[j] = arr[mid + 1 + j];

    int i = 0, j = 0, k = left;

    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) arr[k++] = L[i++];
        else arr[k++] = R[j++];
    }

    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left >= right) return;

    int mid = left + (right - left) / 2;
    mergeSort(arr, left, mid);
    mergeSort(arr, mid + 1, right);
    merge(arr, left, mid, right);
}

// ---------- Quick Sort ----------
int partitionArray(vector<int>& arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }

    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int p = partitionArray(arr, low, high);
        quickSort(arr, low, p - 1);
        quickSort(arr, p + 1, high);
    }
}

void printArray(const vector<int>& arr) {
    for (int x : arr) cout << x << " ";
    cout << endl;
}

int main() {
    vector<int> a1 = {5, 1, 4, 2, 8};
    vector<int> a2 = {64, 25, 12, 22, 11};
    vector<int> a3 = {5, 2, 4, 6, 1, 3};
    vector<int> a4 = {38, 27, 43, 3, 9, 82, 10};
    vector<int> a5 = {10, 7, 8, 9, 1, 5};

    bubbleSort(a1);
    selectionSort(a2);
    insertionSort(a3);
    mergeSort(a4, 0, a4.size() - 1);
    quickSort(a5, 0, a5.size() - 1);

    cout << "Bubble Sort: ";
    printArray(a1);

    cout << "Selection Sort: ";
    printArray(a2);

    cout << "Insertion Sort: ";
    printArray(a3);

    cout << "Merge Sort: ";
    printArray(a4);

    cout << "Quick Sort: ";
    printArray(a5);

    return 0;
}
```

---

# Exam tip

For exam writing, always mention:

1. **definition**
2. **working process**
3. **example**
4. **pseudocode**
5. **time complexity**
6. **space complexity**
7. **stability**
8. **advantages/disadvantages**

---

I can also make you a **very clean handwritten-style exam note version** of these 5 sorting algorithms.
