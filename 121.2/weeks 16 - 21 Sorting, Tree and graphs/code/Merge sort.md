![[Pasted image 20250224144510.png]]
![[Pasted image 20250224145201.png]]
✅ **What this part does:**

- This is the main function that starts the merge sort process.
- It **creates a copy** (`tmp`) of the input array.
- It **calls** `recursiveMergeSort` to sort the array.
![[Pasted image 20250224145234.png]]
✅ **What this part does:**

- **Base Case:** If there's only one element (`iStart == iEnd`), stop recursion.
- **Find the middle point (`iMid`).**
- **Recursive calls:**
    - **Left Half:** Calls `recursiveMergeSort` on the first half (`iStart` to `iMid-1`).
    - **Right Half:** Calls `recursiveMergeSort` on the second half (`iMid` to `iEnd`).
- **Merge Step:** Calls `merge()` to merge the sorted halves.
-1️⃣ **At the start:**

- `mergeSort()` clones the original `array` into `B`.
- It calls `recursiveMergeSort(B, 0, array.length - 1, array)`.
- This means `B` is the working array, and `array` will store the final sorted values.

2️⃣ **During recursion:**

- We process smaller subarrays, sorting them into **the opposite array** (`B → A` or `A → B`).
- This ensures that after every merge step, the merged result is written into **the other array**, so we don't overwrite data.

3️⃣ **Final merge writes back into `A`**

- Since we keep swapping roles of `A` and `B`, the last merge call ensures `A` contains the fully sorted array.
![[Pasted image 20250224145402.png]]
✅ **What this part does:**

- **Two pointers:**
    - `i` starts at `iStart` (left half).
    - `j` starts at `iMid` (right half).
- **Loop through the range `[iStart, iEnd]` and merge:**
    - If the left element is smaller (`A[i] <= A[j]`), copy it to `B[k]`, move `i++`.
    - Otherwise, copy the right element to `B[k]`, move `j++`.
- **When merging is done, `B` contains the sorted values.**
- ![[Pasted image 20250224144249.png]]
![[Pasted image 20250224144415.png]]
![[Pasted image 20250224144441.png]]


