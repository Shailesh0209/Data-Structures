Let’s walk through the corrected solution step-by-step using **Example 1**:

### **Example 1:**

- **Input:** `nums = [2, 3, 1, 1, 4]`
- **Output:** `2`

**Goal:** Find the minimum number of jumps to reach the last index (`nums[4]`) starting from the first index (`nums[0]`).

### **Understanding the Corrected Code:**

```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        res = 0          # Number of jumps
        l = r = 0        # Current window [l, r] that can be reached with `res` jumps

        while r < len(nums) - 1:
            farthest = 0
            for i in range(l, r + 1):
                farthest = max(farthest, i + nums[i])
            l = r + 1      # Move to the next window
            r = farthest   # Update the farthest reachable index
            res += 1       # Increment the number of jumps
        return res
```

### **Step-by-Step Breakdown:**

We'll track the variables `res` (number of jumps), `l` and `r` (current window), and `farthest` (farthest index reachable in the next jump).

1. **Initialization:**
   - `res = 0`
   - `l = 0`
   - `r = 0`
   - `nums = [2, 3, 1, 1, 4]`

2. **First Iteration (First Jump):**
   - **Condition Check:** `r (0) < len(nums) - 1 (4)` → **True**, enter the loop.
   - **Find Farthest in Current Window [0, 0]:**
     - **i = 0:**
       - `farthest = max(0, 0 + nums[0]) = max(0, 0 + 2) = 2`
   - **Update for Next Jump:**
     - `l = r + 1 = 0 + 1 = 1`
     - `r = farthest = 2`
     - `res = res + 1 = 0 + 1 = 1`
   
   **State After First Jump:**
   - `res = 1`
   - `l = 1`
   - `r = 2`
   
   **Explanation:**
   - From index `0`, you can jump up to index `2`. So, the next window is `[1, 2]`.

3. **Second Iteration (Second Jump):**
   - **Condition Check:** `r (2) < len(nums) - 1 (4)` → **True**, enter the loop.
   - **Find Farthest in Current Window [1, 2]:**
     - **i = 1:**
       - `farthest = max(0, 1 + nums[1]) = max(0, 1 + 3) = 4`
     - **i = 2:**
       - `farthest = max(4, 2 + nums[2]) = max(4, 2 + 1) = 4`
   - **Update for Next Jump:**
     - `l = r + 1 = 2 + 1 = 3`
     - `r = farthest = 4`
     - `res = res + 1 = 1 + 1 = 2`
   
   **State After Second Jump:**
   - `res = 2`
   - `l = 3`
   - `r = 4`
   
   **Explanation:**
   - From index `1`, you can jump up to index `4`. Index `4` is the last index, so the algorithm stops after this jump.

4. **Termination:**
   - **Condition Check:** `r (4) < len(nums) - 1 (4)` → **False**, exit the loop.
   - **Return `res`:** `2`

### **Visual Representation:**

Let’s visualize the jumps and the state of variables:

1. **Initial Position:**
   - **Index:** `0`
   - **Jump Range:** `[0]` (since `nums[0] = 2`, you can reach up to index `2`)

2. **First Jump:**
   - **Jump from Index `0` to Index `1`:**
     - Now at index `1`
     - **Jump Range:** `[1, 2]` (since `nums[1] = 3`, you can reach up to index `4`)

3. **Second Jump:**
   - **Jump from Index `1` to Index `4`:**
     - Now at index `4` (last index)
     - **Total Jumps:** `2`

### **Summary of Steps:**

| Jump Number | Current Window [l, r] | Indices Explored | Farthest Reached | Next Window [l, r] | Total Jumps (`res`) |
|-------------|-----------------------|-------------------|-------------------|---------------------|---------------------|
| 1           | [0, 0]                | 0                 | 2                 | [1, 2]              | 1                   |
| 2           | [1, 2]                | 1, 2              | 4                 | [3, 4]              | 2                   |
| **End**     | [3, 4]                | -                 | -                 | -                   | **2**               |

### **Key Takeaways:**

- **Window Concept:** The algorithm maintains a window `[l, r]` representing the range of indices reachable with the current number of jumps (`res`).
  
- **Farthest Reachable:** Within each window, it calculates the farthest index reachable in the next jump.

- **Increment Jumps:** After processing the current window, it moves to the next window `[r + 1, farthest]` and increments the jump count.

- **Termination Condition:** The loop continues until the farthest reachable index covers or surpasses the last index.

This approach ensures that with each jump, you maximize the reach, leading to the minimum number of jumps needed to reach the end.

### **Additional Example for Clarity:**

Let’s briefly consider **Example 2** to reinforce understanding.

#### **Example 2:**

- **Input:** `nums = [2, 3, 0, 1, 4]`
- **Output:** `2`

**Step-by-Step:**

1. **Initial State:**
   - `res = 0`
   - `l = 0`
   - `r = 0`

2. **First Jump:**
   - **Window:** `[0, 0]`
   - **i = 0:** `farthest = max(0, 0 + 2) = 2`
   - **Update:**
     - `l = 1`
     - `r = 2`
     - `res = 1`
   
3. **Second Jump:**
   - **Window:** `[1, 2]`
   - **i = 1:** `farthest = max(0, 1 + 3) = 4`
   - **i = 2:** `farthest = max(4, 2 + 0) = 4`
   - **Update:**
     - `l = 3`
     - `r = 4`
     - `res = 2`
   
4. **Termination:**
   - `r = 4` covers the last index.
   - **Total Jumps:** `2`

**Conclusion:**
- Jump from index `0` to `1`, then from index `1` to `4`.
- **Total Jumps:** `2`

This confirms that the algorithm correctly computes the minimum number of jumps needed.
