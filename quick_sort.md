# Quick Sort: A Deep Dive

## 1. Introduction
Quick Sort is one of the most efficient sorting algorithms, widely used due to its average-case time complexity of **O(n log n)**. It follows the **Divide and Conquer** paradigm, recursively breaking down the problem into smaller subproblems.

---

## 2. History
Quick Sort was developed by **Tony Hoare** in 1959 while working on machine translation at Moscow State University. He designed it as an efficient sorting method that minimizes swaps compared to Bubble Sort.

---

## 3. Algorithm Explanation
Quick Sort works by **choosing a pivot**, partitioning the array around the pivot, and recursively sorting the subarrays.

### Algorithm Steps
1. **Choose a pivot** (can be the first, last, middle, or a randomly chosen element).
2. **Partition** the array so that:
   - Elements **less than** the pivot move to the left.
   - Elements **greater than** the pivot move to the right.
3. **Recursively apply Quick Sort** to the left and right subarrays.
4. The base case is when the subarray has one or zero elements.

---

## 4. Step-by-Step Sorting Example
Let's sort the array:  
`[8, 4, 7, 3, 1, 5, 9, 2]`

### Step 1: Choose a Pivot
Let's take the **last element** as the pivot: **2**.

### Step 2: Partition
Rearrange elements such that:
- Elements **less than** 2 on the left
- Elements **greater than** 2 on the right  
New order after partition:  
`[1, 2, 7, 3, 8, 5, 9, 4]`  
**Pivot (2) is now at index 1.**  

### Step 3: Recursively Apply Quick Sort
- Left subarray: `[1]` (Already sorted)
- Right subarray: `[7, 3, 8, 5, 9, 4]`

### Step 4: Choose a Pivot (Right Subarray)
Pivot = **4**  
Partitioning results in:  
`[3, 4, 7, 8, 5, 9]`  
Pivot is at index **2**.

### Step 5: Continue Recursion
- Left subarray: `[3]` (Sorted)
- Right subarray: `[7, 8, 5, 9]`
  
Pivot = **9**, partitioning results in:  
`[7, 8, 5, 9]`  
Pivot (9) at index **5**.

Pivot = **5**, partitioning results in:  
`[5, 7, 8, 9]`  

Final sorted array:  
`[1, 2, 3, 4, 5, 7, 8, 9]`

---

## 5. Time Complexity Analysis
- **Best/Average Case**: `O(n log n)`  
  - Happens when partitioning splits the array into nearly equal halves.
- **Worst Case**: `O(n^2)`  
  - Occurs when pivot selection is poor (e.g., always picking the smallest or largest element in a sorted array).

---

## 6. Pros & Cons
✅ **Pros:**
- Faster than Merge Sort for most real-world data.
- In-place sorting (requires `O(1)` extra space).
- Good **cache performance** due to locality of reference.

❌ **Cons:**
- Worst case `O(n^2)` for bad pivot choices.
- Not stable (relative order of equal elements can change).
- Recursive calls use extra stack memory `O(log n)`.

---

## 8. Real-World Use Cases
- **Databases**: Indexing and query optimization.
- **Machine Learning**: Sorting features in preprocessing.
- **Networking**: Packet scheduling.
- **Gaming**: Leaderboard ranking.

---

## 9. Summary
| Feature          | Quick Sort |
|-----------------|-----------|
| **Time Complexity (Best/Average)** | `O(n log n)` |
| **Time Complexity (Worst)** | `O(n^2)` |
| **Space Complexity** | `O(1)` (in-place) |
| **Stable?** | ❌ No |
| **Sorting Method** | Partitioning |
| **Use Cases** | Databases, ML, Networking, Gaming |

---
def quicksort(arr):
    """
    Sorts an array using the Quick Sort algorithm.

 Args:
        arr: The array to be sorted.

 Returns:
        The sorted array.
    """
    if len(arr) <= 1:
        return arr

 pivot = arr[len(arr) - 1]  # Choose the last element as the pivot
    left = []
    right = []
 for i in range(len(arr) - 1):  # Exclude the pivot
        if arr[i] < pivot:
            left.append(arr[i])
        else:
            right.append(arr[i])
 return quicksort(left) + [pivot] + quicksort(right)
# Example usage:
my_array = [8, 4, 7, 3, 1, 5, 9, 2]
sorted_array = quicksort(my_array)
print("Sorted array:", sorted_array)

#Lomuto partition scheme implementation.

def quicksort_lomuto(arr, low, high):
    if low < high:
        pi = partition_lomuto(arr, low, high)
        quicksort_lomuto(arr, low, pi - 1)
        quicksort_lomuto(arr, pi + 1, high)

def partition_lomuto(arr, low, high):
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] < pivot:
            i = i + 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

my_array2 = [8, 4, 7, 3, 1, 5, 9, 2]
quicksort_lomuto(my_array2, 0, len(my_array2) - 1)
print("Sorted array using Lomuto:", my_array2)

#Hoare partition scheme implementation.

def quicksort_hoare(arr, low, high):
    if low < high:
        pi = partition_hoare(arr, low, high)
        quicksort_hoare(arr, low, pi)  # Note the change: pi instead of pi - 1
        quicksort_hoare(arr, pi + 1, high)

def partition_hoare(arr, low, high):
    pivot = arr[low]
    i = low - 1
    j = high + 1

 while True:
        i += 1
        while arr[i] < pivot:
            i += 1

 j -= 1
        while arr[j] > pivot:
            j -= 1

  if i >= j:
            return j

  arr[i], arr[j] = arr[j], arr[i]

my_array3 = [8, 4, 7, 3, 1, 5, 9, 2]
quicksort_hoare(my_array3, 0, len(my_array3) - 1)
print("Sorted array using Hoare:", my_array3)

