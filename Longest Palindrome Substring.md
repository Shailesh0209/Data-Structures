# Longest Palindrome Substring - Leetcode Q5
Let's delve into the provided Python code to understand how it **finds the longest palindromic substring** within a given string. We'll use the input `s = "babad"` to illustrate each step of the algorithm.

---

### **Problem Statement**

Given a string `s`, find the **longest substring** that is a palindrome. A palindrome is a string that reads the same backward as forward.

**Example:**
- **Input:** `s = "babad"`
- **Possible Outputs:** `"bab"` or `"aba"`
  
(Note: Both `"bab"` and `"aba"` are valid answers since they are palindromic and have the same length.)

---

### **Code Overview**

Here's the provided Python code:

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        res = ""
        resLen = 0
        for i in range(len(s)):
            # Odd length palindrome
            l, r = i, i
            while l >= 0 and r < len(s) and s[l] == s[r]:
                if (r - l + 1) > resLen:
                    res = s[l:r+1]
                    resLen = r - l + 1
                l -= 1
                r += 1
            
            # Even length palindrome
            l, r = i, i+1
            while l >= 0 and r < len(s) and s[l] == s[r]:
                if (r - l + 1) > resLen:
                    res = s[l:r+1]
                    resLen = r - l + 1
                l -= 1
                r += 1
            
        return res
```

### **Key Components**

1. **Variables:**
   - `res`: Stores the current longest palindromic substring found.
   - `resLen`: Stores the length of `res`.
   
2. **Iterating Through the String:**
   - The loop `for i in range(len(s)):` iterates through each character in the string, treating each character as the center of a potential palindrome.
   
3. **Expanding Around Centers:**
   - **Odd-Length Palindromes:** Centered at a single character (e.g., `"aba"`).
   - **Even-Length Palindromes:** Centered between two characters (e.g., `"abba"`).

4. **Updating the Result:**
   - If a longer palindrome is found, update `res` and `resLen` accordingly.

---

### **Step-by-Step Execution with `s = "babad"`**

Let's walk through the algorithm using `s = "babad"`.

#### **Initialization:**
- `res = ""`
- `resLen = 0`

#### **Iteration Details:**

We'll iterate through each character in the string, considering both odd and even-length palindromes centered at each position.

| **Step** | **i** | **Current Character (`s[i]`)** | **Odd-Length Expansion** | **Even-Length Expansion** | **Current `res`** | **`resLen`** |
|----------|-------|-------------------------------|--------------------------|---------------------------|--------------------|---------------|
| 1        | 0     | 'b'                           | Check `'b'` (indices 0-0): Palindrome `"b"` | Check between `'b'` and `'a'` (indices 0-1): Not a palindrome | `"b"`             | 1             |
| 2        | 1     | 'a'                           | Expand around `'a'`:
  - Compare `s[0]` and `s[2]` (`'b'` vs `'b'`): Match → Palindrome `"bab"`
  - Compare `s[-1]` and `s[3]` (out of bounds and `'a'`): Stop | Expand between `'a'` and `'b'` (indices 1-2): Not a palindrome | `"bab"`            | 3             |
| 3        | 2     | 'b'                           | Expand around `'b'`:
  - Compare `s[1]` and `s[3]` (`'a'` vs `'a'`): Match → Palindrome `"aba"`
  - Compare `s[0]` and `s[4]` (`'b'` vs `'d'`): Not a match | Expand between `'b'` and `'a'` (indices 2-3): Not a palindrome | `"bab"` (unchanged) | 3             |
| 4        | 3     | 'a'                           | Expand around `'a'`:
  - Compare `s[2]` and `s[4]` (`'b'` vs `'d'`): Not a match | Expand between `'a'` and `'d'` (indices 3-4): Not a palindrome | `"bab"` (unchanged) | 3             |
| 5        | 4     | 'd'                           | Expand around `'d'`:
  - Compare `s[3]` and `s[5]` (`'a'` vs out of bounds): Stop | Expand between `'d'` and out of bounds: Stop | `"bab"` (unchanged) | 3             |

#### **Detailed Breakdown:**

1. **i = 0 ('b'):**
   - **Odd-Length:**
     - **Initial:** `l = 0`, `r = 0` → Substring `"b"`
     - **Check:** `s[0] == s[0]` → `'b' == 'b'` → **Match**
     - **Update:** `res = "b"`, `resLen = 1`
     - **Expand:** `l = -1`, `r = 1` → Out of bounds → Stop
     
   - **Even-Length:**
     - **Initial:** `l = 0`, `r = 1` → Substring `"ba"`
     - **Check:** `s[0] == s[1]` → `'b' == 'a'` → **No Match**
     - **No Update**

2. **i = 1 ('a'):**
   - **Odd-Length:**
     - **Initial:** `l = 1`, `r = 1` → Substring `"a"`
     - **Check:** `s[1] == s[1]` → `'a' == 'a'` → **Match**
     - **Update:** `res = "a"`, `resLen = 1` (No change since `resLen` is already 1)
     - **Expand:** `l = 0`, `r = 2` → Substring `"bab"`
     - **Check:** `s[0] == s[2]` → `'b' == 'b'` → **Match**
     - **Update:** `res = "bab"`, `resLen = 3`
     - **Expand:** `l = -1`, `r = 3` → Out of bounds → Stop
     
   - **Even-Length:**
     - **Initial:** `l = 1`, `r = 2` → Substring `"ab"`
     - **Check:** `s[1] == s[2]` → `'a' == 'b'` → **No Match**
     - **No Update**

3. **i = 2 ('b'):**
   - **Odd-Length:**
     - **Initial:** `l = 2`, `r = 2` → Substring `"b"`
     - **Check:** `s[2] == s[2]` → `'b' == 'b'` → **Match**
     - **Update:** `res = "b"`, `resLen = 1` (No change)
     - **Expand:** `l = 1`, `r = 3` → Substring `"aba"`
     - **Check:** `s[1] == s[3]` → `'a' == 'a'` → **Match**
     - **Update:** `res = "aba"`, `resLen = 3` (No change since `resLen` is already 3)
     - **Expand:** `l = 0`, `r = 4` → Substring `"babad"`
     - **Check:** `s[0] == s[4]` → `'b' == 'd'` → **No Match** → Stop
     
   - **Even-Length:**
     - **Initial:** `l = 2`, `r = 3` → Substring `"ba"`
     - **Check:** `s[2] == s[3]` → `'b' == 'a'` → **No Match**
     - **No Update**

4. **i = 3 ('a'):**
   - **Odd-Length:**
     - **Initial:** `l = 3`, `r = 3` → Substring `"a"`
     - **Check:** `s[3] == s[3]` → `'a' == 'a'` → **Match**
     - **Update:** `res = "a"`, `resLen = 1` (No change)
     - **Expand:** `l = 2`, `r = 4` → Substring `"bad"`
     - **Check:** `s[2] == s[4]` → `'b' == 'd'` → **No Match** → Stop
     
   - **Even-Length:**
     - **Initial:** `l = 3`, `r = 4` → Substring `"ad"`
     - **Check:** `s[3] == s[4]` → `'a' == 'd'` → **No Match**
     - **No Update**

5. **i = 4 ('d'):**
   - **Odd-Length:**
     - **Initial:** `l = 4`, `r = 4` → Substring `"d"`
     - **Check:** `s[4] == s[4]` → `'d' == 'd'` → **Match**
     - **Update:** `res = "d"`, `resLen = 1` (No change)
     - **Expand:** `l = 3`, `r = 5` → Out of bounds → Stop
     
   - **Even-Length:**
     - **Initial:** `l = 4`, `r = 5` → Substring `"d"` + out of bounds → Stop
     - **No Update**

#### **Final Result:**
- The longest palindromic substring found is `"bab"` with a length of `3`.
  
**Note:** `"aba"` is also a valid answer with the same length. The algorithm returns the first one it encounters, which is `"bab"` in this case.

---

### **Understanding the Algorithm**

1. **Center Expansion Technique:**
   - The idea is to consider each character (and the gap between characters) as the center of a palindrome and expand outward to check for palindromic properties.
   - This approach efficiently checks all possible palindromic substrings by leveraging the symmetric nature of palindromes.

2. **Handling Odd and Even Lengths:**
   - **Odd-Length Palindromes:** Have a single center character (e.g., `"aba"`).
   - **Even-Length Palindromes:** Have a center between two characters (e.g., `"abba"`).

3. **Updating the Longest Palindrome:**
   - Whenever a longer palindrome is found during expansion, update `res` and `resLen` to reflect the new longest palindrome.

---

### **Detailed Code Explanation**

Let's break down the code step by step.

#### **1. Initialization**

```python
res = ""
resLen = 0
```

- **`res`**: Stores the current longest palindromic substring.
- **`resLen`**: Stores the length of `res` for quick comparison.

#### **2. Iterating Through Each Character**

```python
for i in range(len(s)):
```

- Iterate through each character in the string `s` using its index `i`.
- Treat each character as a potential center for a palindrome.

#### **3. Expanding for Odd-Length Palindromes**

```python
# Odd length palindrome
l, r = i, i
while l >= 0 and r < len(s) and s[l] == s[r]:
    if (r - l + 1) > resLen:
        res = s[l:r+1]
        resLen = r - l + 1
    l -= 1
    r += 1
```

- **Initial Center:** Both `l` and `r` start at `i`, considering the single character at position `i` as the center.
  
- **While Loop Conditions:**
  - **`l >= 0`**: Ensure the left pointer doesn't go out of bounds.
  - **`r < len(s)`**: Ensure the right pointer doesn't go out of bounds.
  - **`s[l] == s[r]`**: Check if the characters at `l` and `r` are the same (palindromic condition).

- **Inside the Loop:**
  - If the current palindrome (`s[l:r+1]`) is longer than `res`, update `res` and `resLen`.
  - Move the pointers outward (`l -= 1`, `r += 1`) to check for a larger palindrome.

#### **4. Expanding for Even-Length Palindromes**

```python
# Even length palindrome
l, r = i, i+1
while l >= 0 and r < len(s) and s[l] == s[r]:
    if (r - l + 1) > resLen:
        res = s[l:r+1]
        resLen = r - l + 1
    l -= 1
    r += 1
```

- **Initial Center:** `l` starts at `i` and `r` starts at `i + 1`, considering the gap between `s[i]` and `s[i+1]` as the center for even-length palindromes.

- **While Loop Conditions:**
  - Similar to the odd-length case, ensuring pointers stay within bounds and characters match.

- **Inside the Loop:**
  - Update `res` and `resLen` if a longer palindrome is found.
  - Move the pointers outward to explore larger palindromic substrings.

#### **5. Returning the Result**

```python
return res
```

- After iterating through all characters and checking all possible centers, return the longest palindromic substring found.

---

### **Time and Space Complexity Analysis**

#### **Time Complexity: O(n²)**

- **Outer Loop:** Iterates through each character in the string → **O(n)**
- **Inner While Loops:** In the worst case, for each character, the algorithm may expand to the entire string → **O(n)**
- **Total:** **O(n) * O(n) = O(n²)**

**Note:** While the average case may perform better, the worst-case scenario (e.g., all characters are the same) results in quadratic time complexity.

#### **Space Complexity: O(1)**

- **Space Used:** Only a few variables (`res`, `resLen`, `l`, `r`) are used.
- **Output Storage:** The longest palindromic substring is stored, which requires **O(n)** space in the worst case (when the entire string is a palindrome). However, since the output is required, it's typically not counted against the algorithm's space complexity.
  
**Overall Space Complexity:** **O(1)** (excluding output)

---

### **Visual Walkthrough with `s = "babad"`**

Let's visualize how the algorithm processes `s = "babad"`.

#### **Initial State:**
- `res = ""`
- `resLen = 0`

#### **Step-by-Step Expansion:**

1. **i = 0 ('b'):**
   - **Odd-Length:**
     - **Center:** `'b'` (indices 0-0)
     - **Match:** `'b' == 'b'` → `"b"`
     - **Update:** `res = "b"`, `resLen = 1`
     - **Expand:** `l = -1`, `r = 1` → Out of bounds → Stop
     
   - **Even-Length:**
     - **Center:** Between `'b'` and `'a'` (indices 0-1)
     - **Match:** `'b' != 'a'` → No palindrome
     
   - **Current `res`:** `"b"` (length 1)

2. **i = 1 ('a'):**
   - **Odd-Length:**
     - **Center:** `'a'` (indices 1-1)
     - **Match:** `'a' == 'a'` → `"a"`
     - **Update:** No change (`resLen` remains 1)
     - **Expand:** `l = 0`, `r = 2` → Compare `'b'` and `'b'` → **Match**
     - **New Palindrome:** `"bab"` (indices 0-2)
     - **Update:** `res = "bab"`, `resLen = 3`
     - **Expand:** `l = -1`, `r = 3` → Out of bounds → Stop
     
   - **Even-Length:**
     - **Center:** Between `'a'` and `'b'` (indices 1-2)
     - **Match:** `'a' != 'b'` → No palindrome
     
   - **Current `res`:** `"bab"` (length 3)

3. **i = 2 ('b'):**
   - **Odd-Length:**
     - **Center:** `'b'` (indices 2-2)
     - **Match:** `'b' == 'b'` → `"b"`
     - **Update:** No change (`resLen` remains 3)
     - **Expand:** `l = 1`, `r = 3` → Compare `'a'` and `'a'` → **Match**
     - **New Palindrome:** `"aba"` (indices 1-3)
     - **Update:** No change (`resLen` remains 3)
     - **Expand:** `l = 0`, `r = 4` → Compare `'b'` and `'d'` → **No Match** → Stop
     
   - **Even-Length:**
     - **Center:** Between `'b'` and `'a'` (indices 2-3)
     - **Match:** `'b' != 'a'` → No palindrome
     
   - **Current `res`:** `"bab"` (length 3)

4. **i = 3 ('a'):**
   - **Odd-Length:**
     - **Center:** `'a'` (indices 3-3)
     - **Match:** `'a' == 'a'` → `"a"`
     - **Update:** No change (`resLen` remains 3)
     - **Expand:** `l = 2`, `r = 4` → Compare `'b'` and `'d'` → **No Match** → Stop
     
   - **Even-Length:**
     - **Center:** Between `'a'` and `'d'` (indices 3-4)
     - **Match:** `'a' != 'd'` → No palindrome
     
   - **Current `res`:** `"bab"` (length 3)

5. **i = 4 ('d'):**
   - **Odd-Length:**
     - **Center:** `'d'` (indices 4-4)
     - **Match:** `'d' == 'd'` → `"d"`
     - **Update:** No change (`resLen` remains 3)
     - **Expand:** `l = 3`, `r = 5` → Out of bounds → Stop
     
   - **Even-Length:**
     - **Center:** Between `'d'` and out of bounds (indices 4-5)
     - **Match:** Out of bounds → Stop
     
   - **Current `res`:** `"bab"` (length 3)

#### **Final Output:**
- The longest palindromic substring found is `"bab"` with a length of `3`.

**Alternative Valid Output:** `"aba"` is also a valid answer with the same length. The algorithm returns the first one it encounters, which is `"bab"` in this case.

---

### **Additional Insights**

1. **Why Check Both Odd and Even Lengths?**
   - Palindromes can be either odd or even in length. By checking both scenarios, the algorithm ensures that all possible palindromic substrings are considered.

2. **Why Is the Time Complexity O(n²)?**
   - For each character, the algorithm potentially expands to the entire length of the string in both directions. Thus, in the worst case (e.g., all characters are identical), the number of comparisons becomes quadratic relative to the string's length.

3. **Space Efficiency:**
   - The algorithm uses constant extra space (excluding the space for the output), making it space-efficient.

4. **Alternative Approaches:**
   - **Dynamic Programming:** Another method to solve this problem with O(n²) time and space complexity.
   - **Manacher’s Algorithm:** A more advanced algorithm that can find the longest palindromic substring in linear time O(n).

---

### **Conclusion**

The provided `longestPalindrome` method efficiently finds the longest palindromic substring within a given string by employing the **center expansion technique**. It meticulously checks for both odd and even-length palindromes centered at each character, ensuring that all potential palindromic substrings are evaluated. While its time complexity is quadratic, its simplicity and effectiveness make it a practical solution for this problem.

---

### **Complete Walkthrough Summary with `s = "babad"`**

| **i** | **Character** | **Odd-Length Palindrome** | **Even-Length Palindrome** | **Current Longest (`res`)** | **`resLen`** |
|-------|---------------|---------------------------|----------------------------|------------------------------|---------------|
| 0     | 'b'           | `"b"`                     | Not a palindrome           | `"b"`                        | 1             |
| 1     | 'a'           | `"bab"`                   | Not a palindrome           | `"bab"`                      | 3             |
| 2     | 'b'           | `"aba"`                   | Not a palindrome           | `"bab"`                      | 3             |
| 3     | 'a'           | `"a"`                     | Not a palindrome           | `"bab"`                      | 3             |
| 4     | 'd'           | `"d"`                     | Not a palindrome           | `"bab"`                      | 3             |

**Final Output:** `"bab"`
