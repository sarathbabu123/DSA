# Sorting Algorithms

## Stable Sorting Algorithms
- **Insertion Sort**
- **Merge Sort**
- **Bubble Sort**

## Unstable Sorting Algorithms
- **Quick Sort**
- **Heap Sort**
- **Selection Sort**

---

## Selection Sort

### Code
```python
arr = [13, 46, 24, 52, 20, 9]

for i in range(len(arr)):
    minidx = i
    for j in range(i + 1, len(arr)):
        if arr[minidx] > arr[j]:
            minidx = j
    arr[i], arr[minidx] = arr[minidx], arr[i]  # Swap the elements

print(arr)
```

### How it works
- Divides the list into two sections: sorted and unsorted.
- Finds the minimum element from the unsorted section and swaps it with the first element of the unsorted section.
- Repeats this process until the entire list is sorted.

### Properties
- **In-place:** Yes (does not require extra space).
- **Stable:** No (relative order of equal elements may change).

### Time Complexity
- **Best Case:** `O(n²)`
- **Average Case:** `O(n²)`
- **Worst Case:** `O(n²)`

### Space Complexity
- **`O(1)`** (In-place sorting)

---

## Bubble Sort

### Code
```python
arr = [13, 46, 24, 52, 20, 9]

n = len(arr)
for i in range(n):
    swapped = False
    for j in range(0, n - i - 1):
        if arr[j] > arr[j + 1]:
            arr[j], arr[j + 1] = arr[j + 1], arr[j]  # Swap adjacent elements
            swapped = True
    if not swapped:
        break

print(arr)
```

### How it works
- Repeatedly compares adjacent elements and swaps them if they are in the wrong order.
- After each pass, the largest unsorted element "bubbles up" to its correct position.
- Stops early if no swaps are made in a pass, indicating the list is already sorted.

### Properties
- **In-place:** Yes (does not require extra space).
- **Stable:** Yes (maintains the relative order of equal elements).

### Time Complexity
- **Best Case:** `O(n)` (when the list is already sorted)
- **Average Case:** `O(n²)`
- **Worst Case:** `O(n²)`

### Space Complexity
- **`O(1)`** (In-place sorting)

---

## Insertion Sort

### Code
```python
def insertion_sort(arr):
    n = len(arr)
    for i in range(1, n):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key

# Example usage:
arr = [5, 3, 8, 4, 2]
insertion_sort(arr)
print("Sorted array:", arr)
```

### How it works
- Builds the sorted list one element at a time.
- Picks the next element and inserts it into its correct position in the sorted portion.
- Repeats until the entire list is sorted.

### Properties
- **In-place:** Yes (does not require extra space).
- **Stable:** Yes (maintains the relative order of equal elements).

### Time Complexity
- **Best Case:** `O(n)` (when the list is already sorted)
- **Average Case:** `O(n²)`
- **Worst Case:** `O(n²)`

### Space Complexity
- **`O(1)`** (In-place sorting)

---

## Merge Sort

### Code
```python
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2
        left = arr[:mid]
        right = arr[mid:]

        merge_sort(left)
        merge_sort(right)

        i = j = k = 0

        while i < len(left) and j < len(right):
            if left[i] <= right[j]:
                arr[k] = left[i]
                i += 1
            else:
                arr[k] = right[j]
                j += 1
            k += 1

        while i < len(left):
            arr[k] = left[i]
            i += 1
            k += 1

        while j < len(right):
            arr[k] = right[j]
            j += 1
            k += 1

# Example usage:
arr = [38, 27, 43, 3, 9, 82, 10]
merge_sort(arr)
print("Sorted array:", arr)
```

### How it works
- Divides the array into halves recursively until each subarray contains a single element.
- Merges the subarrays back together in sorted order.

### Properties
- **In-place:** No (requires additional space for merging).
- **Stable:** Yes (maintains the relative order of equal elements).

### Time Complexity
- **Best Case:** `O(n log n)`
- **Average Case:** `O(n log n)`
- **Worst Case:** `O(n log n)`

### Space Complexity
- **`O(n)`** (requires additional space for merging)

---

## Recursive Bubble Sort

### Code
```python
def bubble_sort_recursive(arr, n=None):
    if n is None:
        n = len(arr)

    if n == 1:
        return

    for i in range(n - 1):
        if arr[i] > arr[i + 1]:
            arr[i], arr[i + 1] = arr[i + 1], arr[i]

    bubble_sort_recursive(arr, n - 1)

# Example usage:
arr = [64, 34, 25, 12, 22, 11, 90]
bubble_sort_recursive(arr)
print("Sorted array:", arr)
```

### How it works
- Recursively sorts the array by bubbling the largest element to the end in each recursive call.

### Properties
- **In-place:** Yes (does not require extra space).
- **Stable:** Yes (maintains the relative order of equal elements).

### Time Complexity
- **Best Case:** `O(n)` (when the list is already sorted)
- **Average Case:** `O(n²)`
- **Worst Case:** `O(n²)`

### Space Complexity
- **`O(n)`** (due to recursion stack)

---

## Recursive Insertion Sort

### Code
```python
def insertion_sort_recursive(arr, n=None):
    if n is None:
        n = len(arr)

    if n <= 1:
        return

    insertion_sort_recursive(arr, n - 1)

    last = arr[n - 1]
    j = n - 2

    while j >= 0 and arr[j] > last:
        arr[j + 1] = arr[j]
        j -= 1

    arr[j + 1] = last

# Example usage:
arr = [12, 11, 13, 5, 6]
insertion_sort_recursive(arr)
print("Sorted array:", arr)
```

### How it works
- Recursively sorts the first `n-1` elements and then inserts the last element into its correct position.

### Properties
- **In-place:** Yes (does not require extra space).
- **Stable:** Yes (maintains the relative order of equal elements).

### Time Complexity
- **Best Case:** `O(n)` (when the list is already sorted)
- **Average Case:** `O(n²)`
- **Worst Case:** `O(n²)`

### Space Complexity
- **`O(n)`** (due to recursion stack)

---

## Quick Sort

### Code
```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr

    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]

    return quick_sort(left) + middle + quick_sort(right)

# Example usage:
arr = [10, 7, 8, 9, 1, 5]
sorted_arr = quick_sort(arr)
print("Sorted array:", sorted_arr)
```

### How it works
- Selects a pivot element and partitions the array into three parts: elements less than the pivot, equal to the pivot, and greater than the pivot.
- Recursively sorts the left and right partitions.

### Properties
- **In-place:** No (the implementation shown is not in-place).
- **Stable:** No (relative order of equal elements may change).

### Time Complexity
- **Best Case:** `O(n log n)`
- **Average Case:** `O(n log n)`
- **Worst Case:** `O(n²)` (when the pivot is poorly chosen)

### Space Complexity
- **`O(n)`** (due to recursion and additional lists)

---

## Summary of Sorting Algorithms

| Algorithm              | Time Complexity (Best) | Time Complexity (Worst) | Time Complexity (Average) | Space Complexity | Stability | In-place |
|-------------------------|-------------------------|--------------------------|----------------------------|------------------|-----------|----------|
| Selection Sort          | `O(n²)`                | `O(n²)`                 | `O(n²)`                   | `O(1)`           | No        | Yes      |
| Bubble Sort             | `O(n)`                 | `O(n²)`                 | `O(n²)`                   | `O(1)`           | Yes       | Yes      |
| Insertion Sort          | `O(n)`                 | `O(n²)`                 | `O(n²)`                   | `O(1)`           | Yes       | Yes      |
| Merge Sort              | `O(n log n)`           | `O(n log n)`            | `O(n log n)`              | `O(n)`           | Yes       | No       |
| Recursive Bubble Sort   | `O(n)`                 | `O(n²)`                 | `O(n²)`                   | `O(n)`           | Yes       | Yes      |
| Recursive Insertion Sort| `O(n)`                 | `O(n²)`                 | `O(n²)`                   | `O(n)`           | Yes       | Yes      |
| Quick Sort              | `O(n log n)`           | `O(n²)`                 | `O(n log n)`              | `O(n)`           | No        | No       |

---
