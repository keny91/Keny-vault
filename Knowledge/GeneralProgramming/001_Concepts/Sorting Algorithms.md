#sort #data

### 1. **Comparison-based Sorting**

These algorithms sort by comparing elements pairwise.

#### Examples:

- **Bubble Sort**
    
    - **How:** Repeatedly swaps adjacent elements if they are in the wrong order.
        
    - **Use case:** Teaching/learning sorting concepts or very small datasets (due to simplicity but inefficient for large data).
        
- **Insertion Sort**
    
    - **How:** Builds the sorted list one element at a time, inserting each element into its correct position.
        
    - **Use case:** Nearly sorted or small datasets; efficient in practice for small or almost sorted lists.
        
- **Selection Sort**
    
    - **How:** Repeatedly selects the minimum element and swaps it with the first unsorted element.
        
    - **Use case:** Situations where memory writes are costly (few swaps).
        
- **Merge Sort**
    
    - **How:** Divides list into halves recursively, sorts each half, then merges sorted halves.
        
    - **Use case:** Large datasets where stable sorting is required; works well with linked lists and external sorting (disk).
        
- **Quick Sort**
    
    - **How:** Picks a pivot, partitions the array around the pivot, recursively sorts partitions.
        
    - **Use case:** General-purpose sorting, often fastest in practice for arrays; good cache performance.
        
- **Heap Sort**
    
    - **How:** Uses a heap data structure to repeatedly extract the max/min element.
        
    - **Use case:** When constant worst-case time is needed (O(n log n)) and no extra memory allocation is preferred.
        

---

### 2. **Non-Comparison-based Sorting**

These algorithms sort data without comparing elements directly, usually exploiting the structure of the keys.

#### Examples:

- **Counting Sort**
    
    - **How:** Counts the occurrences of each key, then calculates positions.
        
    - **Use case:** Sorting integers or objects with integer keys in a small range, like sorting grades or ages.
        
- **Radix Sort**
    
    - **How:** Sorts numbers digit by digit, using a stable sort like counting sort on each digit.
        
    - **Use case:** Sorting large lists of fixed-length integers or strings, such as sorting phone numbers or IP addresses.
        
- **Bucket Sort**
    
    - **How:** Distributes elements into buckets and sorts each bucket individually.
        
    - **Use case:** Sorting uniformly distributed data, e.g., floating-point numbers between 0 and 1.
        

---

### 3. **Special-purpose Sorting**

- **Timsort**
    
    - **How:** Hybrid of merge sort and insertion sort, optimized for real-world data.
        
    - **Use case:** Python and Java's standard sorting algorithms, excellent for real-world partially sorted data.
        
- **Sleep Sort** (novelty)
    
    - **How:** Uses timing delays (not practical).
        
    - **Use case:** Just a fun algorithm, not for practical use.
        

---

### Summary Table

| Algorithm      | Type                 | Time Complexity (Avg) | Space        | Use Case Highlights                       |
| -------------- | -------------------- | --------------------- | ------------ | ----------------------------------------- |
| Bubble Sort    | Comparison-based     | O(n²)                 | O(1)         | Simple, tiny data, educational purposes   |
| Insertion Sort | Comparison-based     | O(n²), O(n) best      | O(1)         | Nearly sorted data, small datasets        |
| Selection Sort | Comparison-based     | O(n²)                 | O(1)         | When writes are expensive                 |
| Merge Sort     | Comparison-based     | O(n log n)            | O(n)         | Large data, stable sort, external sorting |
| Quick Sort     | Comparison-based     | O(n log n)            | O(log n) avg | Fast general purpose array sorting        |
| Heap Sort      | Comparison-based     | O(n log n)            | O(1)         | Worst-case guarantees, limited memory     |
| Counting Sort  | Non-comparison-based | O(n + k)              | O(k)         | Integers in small range                   |
| Radix Sort     | Non-comparison-based | O(nk)                 | O(n + k)     | Fixed-length integers or strings          |
| Bucket Sort    | Non-comparison-based | O(n + k)              | O(n)         | Uniform distribution of floating points   |
| Timsort        | Hybrid (Comp-based)  | O(n log n)            | O(n)         | Real-world data, standard in Python/Java  |
