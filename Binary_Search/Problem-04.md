## Problem: Find Minimum in Rotated Sorted Array (LeetCode 153)

```text
Input:
nums = [3,4,5,1,2]

Output:
1
```

Tell me:

* Pattern
* Why
* Brute Force Complexity
* Optimal Data Structure
* Optimal Approach
* Time Complexity
* Space Complexity

After your answer, I'll share:

* Brute force code
* Optimal code
* Any alternative approaches

---
# Verification

## Pattern

✅ Correct

```text
Modified Binary Search
```

---

## Why?

✅ Because the array is **sorted but rotated**.

---

## Brute Force

```text
Time : O(n)
Space: O(1)
```
---

## Optimal Data Structure

No extra data structure.
---

## Optimal Idea

Instead of checking where the **target** lies, we check **which side contains the minimum**.

Rule:

```javascript
if (nums[mid] > nums[right])
```

Minimum is in the **right half**.

```javascript
left = mid + 1;
```

Otherwise,

Minimum is in the **left half (including mid)**.

```javascript
right = mid;
```

Notice it's:

```javascript
right = mid;
```

not

```javascript
right = mid - 1;
```

because **mid itself could be the minimum**.

---

## Complexity

Time

```text
O(log n)
```

Space

```text
O(1)
```
---

# Code

## Brute Force

```javascript
function findMin(nums) {

    let min = nums[0];

    for (const num of nums) {
        min = Math.min(min, num);
    }

    return min;
}
```

---

## Optimal (Modified Binary Search)

```javascript
function findMin(nums) {

    let left = 0;
    let right = nums.length - 1;

    while (left < right) {

        const mid = Math.floor((left + right) / 2);

        if (nums[mid] > nums[right]) {

            left = mid + 1;

        } else {

            right = mid;
        }
    }

    return nums[left];
}
```

---

# ⭐ New Note for your notebook

Compare these two rotated-array problems:

| Problem                                  | Compare With  | Goal                 |
| ---------------------------------------- | ------------- | -------------------- |
| **Search in Rotated Sorted Array**       | `target`      | Find target index    |
| **Find Minimum in Rotated Sorted Array** | `nums[right]` | Find minimum element |

Same pattern (**Modified Binary Search**), but **different decision logic**.

---
