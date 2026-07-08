![[Pasted image 20250224142405.png]]
![[Pasted image 20250224142426.png]]
![[Pasted image 20250224142449.png]]
![[Pasted image 20250224142658.png]]
![[Pasted image 20250224143958.png]]
![[Pasted image 20250224144023.png]]
![[Pasted image 20250224144249.png]]
![[Pasted image 20250224144337.png]]
![[Pasted image 20250224144357.png]]э![[Pasted image 20250224144415.png]]![[Pasted image 20250224144441.png]]![[Pasted image 20250224144459.png]]![[Pasted image 20250224145201.png]]
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
![[Pasted image 20250224145402.png]]
![[Pasted image 20250224153415.png]]
![[Pasted image 20250224153511.png]]


