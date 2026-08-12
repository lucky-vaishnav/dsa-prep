**Find First and Last Position of Element in Sorted Array**

```text
nums = [5,7,7,8,8,10]
target = 8

Output = [3,4]
```

Think about:

* Pattern
* Why?
* Brute-force approach
* Optimal approach
* Time complexity
* Space complexity

**Hint:** We already know normal Binary Search. The interesting part is finding **both boundaries** of the target.

### My Thought-
So we will use binary search and for brute force approach Time complexity will be O of n. Binary search time complexity will be O of log n. Space complexity will be O of 1. And as this array is sorted, so we can use binary search. And as we know that this array is already sorted, so we will do the, use the binary search template, left pointer, right pointer, and mid will be the first element to check. And whenever the mid is equal to the target, then we just need to check that where the same element exists. It is the one index after or one index before. So that will be the extra part, but the rest will be the same because the array is already sorted.

---
Yes, your overall understanding is correct. One important correction:

> When `mid === target`, don't just check `mid - 1` / `mid + 1`. There may be **many duplicates**, so we use binary search to find each boundary.

### Brute Force — O(n)

```javascript
function searchRange(nums, target) {
    let first = -1;
    let last = -1;

    for (let i = 0; i < nums.length; i++) {
        if (nums[i] === target) {
            if (first === -1) {
                first = i;
            }

            last = i;
        }
    }

    return [first, last];
}
```

---

## Optimal — Two Binary Searches — O(log n)

We perform **binary search twice**:

1. Find the **first occurrence**
2. Find the **last occurrence**

```javascript
function searchRange(nums, target) {

    function findFirst() {

        let left = 0;
        let right = nums.length - 1;
        let result = -1;

        while (left <= right) {

            const mid = Math.floor((left + right) / 2);

            if (nums[mid] === target) {
                result = mid;

                // Target found,
                // but there may be another one on the left.
                right = mid - 1;

            } else if (nums[mid] < target) {
                left = mid + 1;

            } else {
                right = mid - 1;
            }
        }

        return result;
    }

    function findLast() {

        let left = 0;
        let right = nums.length - 1;
        let result = -1;

        while (left <= right) {

            const mid = Math.floor((left + right) / 2);

            if (nums[mid] === target) {
                result = mid;

                // Target found,
                // but there may be another one on the right.
                left = mid + 1;

            } else if (nums[mid] < target) {
                left = mid + 1;

            } else {
                right = mid - 1;
            }
        }

        return result;
    }

    return [findFirst(), findLast()];
}
```

### ⭐ Key idea for your notes

```text
Find First:
target found → move LEFT
right = mid - 1

Find Last:
target found → move RIGHT
left = mid + 1
```

Example:

```text
nums   = [5,7,7,8,8,8,10]
target = 8

First binary search → 3
Last binary search  → 5

Answer → [3,5]
```

So this is a very useful **modified Binary Search pattern**:
**when you find the target, don't stop — continue searching toward the required boundary.**

## Question -
So is it the only best solution for it with respect to the time complexity? Because we are using two binary search here, so it is not a problem, right? So it is the best solution from all the patterns for this problem, right, that I can consider, or no?

Yes. For this problem, **two binary searches are the optimal approach**.

* Brute force → `O(n)`
* Binary search for first + binary search for last → `O(log n) + O(log n)` = **O(log n)**
* Space → **O(1)**

So you should consider **two modified binary searches** the best solution for your DSA notes.

And yes, doing binary search twice is **not a problem**—constant factors are ignored in Big-O.

The key pattern to remember is:

> **Sorted array + need first/last occurrence → boundary binary search.**
