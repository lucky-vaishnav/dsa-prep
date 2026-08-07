## Problem: Search a 2D Matrix (LeetCode 74)

```text
Input:

matrix =
[
  [1,3,5,7],
  [10,11,16,20],
  [23,30,34,60]
]

target = 3

Output:
true
```

### Hint

Notice these two properties:

```text
Each row is sorted.

The first element of every row is greater than the last element of the previous row.
```

Think about:

* Pattern
* Why
* Brute Force Complexity
* Optimal Data Structure
* Optimal Approach
* Time Complexity
* Space Complexity

💡 **Small Hint:** This problem is actually a **Binary Search** problem, but not in the usual one-dimensional array. Think about how you can still eliminate half of the search space each step.

Let's see your thought process first, then we'll discuss the solutions together.

---
# My Thought -
So for the second problem, search in 2D matrix, so like you said, it is a sorted array, and the element within the sub-array are also sorted. So we can use this property to search the element, and whenever we think about sorted, binary search is the better option. So we will do the binary search twice. First, we'll do within the main array, and then we will check if that mid element's first element is greater than or equal to, or less than or equal to, the previous sub-array last element. Accordingly, we can think that which array to move to. And then once we got that array to check, for that particular array, we will do binary search again. So brute force will be O of n into k time complexity, and for binary search, it will be approximately, I think, we will do twice binary search, so it will be around O of log n into log k, something like that. So I'll also share the brute force code and the binary search code.

---
Excellent! I'd give this **9/10**.

---

# Verification

## Pattern

✅ Correct

```text
Binary Search
```

---

## Why?

✅ Because:

* Each row is sorted.
* The first element of every row is greater than the last element of the previous row.

This means the entire matrix behaves like one sorted sequence.

---

## Your Approach

You said:

> Binary Search twice.

✅ This is a perfectly valid and common solution.

1. Binary search to find the correct row.
2. Binary search inside that row.

---

## Brute Force

Time:

```text
O(m × n)
```

✔️ Correct.

Space:

```text
O(1)
```

---

## Optimal (Two Binary Searches)

Suppose

```text
m = rows
n = columns
```

Time

```text
O(log m + log n)
```

Not

```text
O(log m × log n)
```

because the searches happen **one after another**, so we **add** their complexities.

---

## Even Better Solution ⭐

There is an even more elegant approach.

Treat the matrix as one long sorted array.

Example

```text
1  3  5  7
10 11 16 20
23 30 34 60
```

Imagine it as

```text
[1,3,5,7,10,11,16,20,23,30,34,60]
```

Then perform **one Binary Search**.

To convert an index back into row/column:

```javascript
row = Math.floor(mid / cols)
col = mid % cols
```

Complexity

```text
O(log(m × n))
```

Since

```text
log(m × n) = log(m) + log(n)
```

both approaches have the same asymptotic complexity, but the single binary search is cleaner and is the solution interviewers often prefer.

---

# Code

## Brute Force

```javascript
function searchMatrix(matrix, target) {

    for (const row of matrix) {

        for (const num of row) {

            if (num === target) {
                return true;
            }
        }
    }

    return false;
}
```

---

## Approach 1 — Binary Search Twice

```javascript
function searchMatrix(matrix, target) {

    const rows = matrix.length;
    const cols = matrix[0].length;

    let top = 0;
    let bottom = rows - 1;

    while (top <= bottom) {

        const mid = Math.floor((top + bottom) / 2);

        if (target < matrix[mid][0]) {

            bottom = mid - 1;

        } else if (target > matrix[mid][cols - 1]) {

            top = mid + 1;

        } else {

            let left = 0;
            let right = cols - 1;

            while (left <= right) {

                const m = Math.floor((left + right) / 2);

                if (matrix[mid][m] === target) {
                    return true;
                }

                if (matrix[mid][m] < target) {
                    left = m + 1;
                } else {
                    right = m - 1;
                }
            }

            return false;
        }
    }

    return false;
}
```

---

## Approach 2 — Single Binary Search (Recommended)

```javascript
function searchMatrix(matrix, target) {

    const rows = matrix.length;
    const cols = matrix[0].length;

    let left = 0;
    let right = rows * cols - 1;

    while (left <= right) {

        const mid = Math.floor((left + right) / 2);

        const row = Math.floor(mid / cols);
        const col = mid % cols;

        if (matrix[row][col] === target) {
            return true;
        }

        if (matrix[row][col] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return false;
}
```

---

## ⭐ New note for your notebook

```text
Binary Search in 2D Matrix

Approach 1:
- Binary Search to find the row.
- Binary Search inside that row.
- Time: O(log m + log n)

Approach 2 (Preferred):
- Treat the matrix as one sorted array.
- Convert index:
    row = Math.floor(mid / cols)
    col = mid % cols
- Time: O(log(m × n))
```

**One correction to your answer:** Whenever you have two algorithms running one after another, remember to **add** their complexities, not multiply them. So:

* ❌ `O(log m × log n)`
* ✅ `O(log m + log n)`

That's a small but important complexity rule to remember.

