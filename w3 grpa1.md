Let's break down and explain the question and the provided solution.

### Question Explanation:
You are given a list of dish orders (represented by unique dish IDs), and the restaurant needs to prepare dishes in a specific order:
1. **Dishes with the most orders should be prepared first.**
2. **If two or more dishes have the same number of orders, the dish with the smaller ID (numerically smaller) should be prepared first.**

You need to implement a function `DishPrepareOrder(order_list)` that:
- Takes a list of dish IDs as input.
- Counts the number of times each dish ID appears in the list.
- Sorts the dish IDs in descending order of their count (i.e., most frequent first).
- If two dishes have the same count, the dish with the smaller numerical ID should come first.

### Sample Input:
```python
[1004, 1003, 1004, 1003, 1004, 1005, 1003, 1004, 1003, 1002, 1005, 1002, 1002, 1001, 1002, 1002]
```

### Sample Output:
```python
[1002, 1003, 1004, 1005, 1001]
```

### Explanation of Output:
- Dish `1002` appears 5 times (most frequent).
- Dish `1003` appears 4 times.
- Dish `1004` appears 4 times (but its ID is higher than `1003`, so it comes after `1003`).
- Dish `1005` appears 2 times.
- Dish `1001` appears 1 time.

### Code Explanation:

1. **`insertionsort(L)` Function:**
   - This function is a simple **stable sorting algorithm** (insertion sort). It's stable because if two items have the same frequency, they will maintain their original order, which in our case is sorted by the dish ID.
   - It sorts the list of tuples `L` in place based on the second value (the frequency), in descending order (most frequent dishes first).

2. **`DishPrepareOrder(order_list)` Function:**
   - The function starts by counting how many times each dish ID appears in the `order_list`. This is done using a dictionary `order_count` where the key is the dish ID, and the value is its count.
   
   - After building the `order_count` dictionary, it creates a list `R` where each element is a tuple of `(dish_id, count)`. This list is sorted in two stages:
     - First, by dish ID using the `sorted()` function (which guarantees that dishes with smaller IDs come first).
     - Second, by using `insertionsort()` to sort by frequency, ensuring that dishes with higher counts come first.

   - Finally, after sorting, the function extracts just the dish IDs in the correct order (ignoring their counts) and returns them as the result.

### Code Walkthrough:
```python
def DishPrepareOrder(order_list):
    order_count = {}
    R = []
    
    # Step 1: Count how many times each dish ID appears
    for order in order_list:
        if order in order_count:
            order_count[order] += 1
        else:
            order_count[order] = 1
    
    # Step 2: Create a list of (ID, count) tuples sorted by ID (default sorting)
    for ID in sorted(order_count.keys()):
        R.append((ID, order_count[ID]))
    
    # Step 3: Use insertion sort to sort by count in descending order
    R = insertionsort(R)
    
    # Step 4: Extract only the dish IDs from the sorted list
    Res = []
    for tup in R:
        Res.append(tup[0])
    
    return Res
```

### Output Explanation:
- When you pass the input `[1004, 1003, 1004, 1003, 1004, 1005, 1003, 1004, 1003, 1002, 1005, 1002, 1002, 1001, 1002, 1002]`, the function calculates the frequency of each dish and sorts them based on the frequency (and dish ID as a tie-breaker), returning the list `[1002, 1003, 1004, 1005, 1001]`.

### Summary:
- The task is to prioritize dishes based on how often they are ordered.
- We first count the frequency of each dish, then sort them by frequency (with ties broken by dish ID), and finally return the sorted list of dish IDs.

If you need further explanation or modifications, feel free to ask!
