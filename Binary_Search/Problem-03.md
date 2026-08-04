Perfect! We'll continue with our format.

* ✅ **Q1 = Revision**
* ✅ **Q2 = New (Heap)**

---

# 🟢 Q1 (Revision)

## Problem: Search in Rotated Sorted Array (LeetCode 33)

Example:

```text
nums = [4,5,6,7,0,1,2]
target = 0

Output:
4
```

Tell me:

* Pattern
* Why
* Brute Force Complexity
* Optimal Data Structure
* Optimal Approach
* Time Complexity
* Space Complexity

As usual, after your answer I'll verify it and share:

* Brute Force code
* Optimal code
* (If any other approaches exist)

---
# My Answer -
```text
So for question number one, search in rotated sorted array. So it seems like that maybe we want to use this feature, like this rotated sorted array, to search the element in minimum time. Because for this problem, I think brute force complexity will be O of n. And, but by using this feature of rotated sorted array, I think we should use some pattern or some good idea to reduce this time. But I am not sure what will be that approach. So yeah. And one more question from my side, why can't we just use that indexOf parameter for this problem? And yeah, share that brute force code as well, optimal code as well, or any other approach, as you said earlier.
```


You correctly recognized that the problem is asking us to use the **sorted property** to do better than `O(n)`, but you missed identifying the exact pattern.

---

# Verification

### Pattern

❌ Not identified.

✅ Correct pattern:

```text
Modified Binary Search
```

---

### Why?

✅ Because the array is **sorted but rotated**.

A normal binary search doesn't work directly, but **one half of the array is always sorted**, and we use that fact to eliminate half of the search space each time.

---

### Brute Force

Time:

```text
O(n)
```

Space:

```text
O(1)
```

✔️ Correct.

---

### Optimal Data Structure

No extra data structure.

✔️ Correct.

---

### Optimal Approach

Instead of:

> Binary Search

The important idea is:

> **Modified Binary Search**

At every iteration:

1. Find `mid`.
2. Check **which half is sorted**.
3. Decide whether the target lies in that sorted half.
4. Search only that half.

This is the key idea of the problem.

---

### Complexity

Time:

```text
O(log n)
```

Space:

```text
O(1)
```

✔️ Correct.

---

# Your Question

> Why can't we just use `indexOf()`?

We can.

```javascript
nums.indexOf(target)
```

But internally `indexOf()` performs a **linear search**, so its time complexity is:

```text
O(n)
```

The interviewer wants you to exploit the **sorted + rotated** property and solve it in:

```text
O(log n)
```

That's why `indexOf()` isn't considered an acceptable optimal solution.

---

# Code

## Brute Force

```javascript
function search(nums, target) {
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] === target) {
            return i;
        }
    }

    return -1;
}
```

---

## Using `indexOf()`

```javascript
function search(nums, target) {
    return nums.indexOf(target);
}
```

---

## Optimal (Modified Binary Search)

```javascript
function search(nums, target) {

    let left = 0;
    let right = nums.length - 1;

    while (left <= right) {

        const mid = Math.floor((left + right) / 2);

        if (nums[mid] === target) {
            return mid;
        }

        // Left half is sorted
        if (nums[left] <= nums[mid]) {

            if (target >= nums[left] && target < nums[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }

        }
        // Right half is sorted
        else {

            if (target > nums[mid] && target <= nums[right]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }

    return -1;
}
```

---

This problem introduces a **new Binary Search pattern**:

> **Modified Binary Search on Rotated Sorted Arrays**

gether and then move on to the code.
