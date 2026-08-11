### **Search in Rotated Sorted Array II**

```text
nums = [2,5,6,0,0,1,2]
target = 0

Output:
true
```

This is similar to the rotated sorted array problem we already learned, **but now duplicates are allowed**.

Think about:

* Pattern
* Why?
* What changes because of duplicates?
* Brute-force complexity
* Optimal approach
* Time complexity
* Space complexity

### Small hint

Previously we could confidently determine which half was sorted.

With duplicates, consider this situation:

```text
[2,2,2,3,2,2]
```

Sometimes `nums[left]`, `nums[mid]`, and `nums[right]` can all be equal.

Think about **what information you lose in that situation** and what you can safely do.

---
### My Thought-
So for question number two, search in rotated sorted array 2, so actually it will be, the approach will be similar like we've done modified binary search, but for this problem, the array can have duplicate value as well. So what we will do is that while moving to left, while updating left and right pointer, so we will check that if the nearby value also the same, so we can update the mid according to that. That one will be the major change for this problem, I think. So pattern will be modified binary search, and optimal approach, binary search. And complexity will be O of n log n, space complexity will be O of 1, and brute force complexity will be O of n. And I, sorry, I wanted to update it. The time complexity for modified binary search will be O of log n.

---
Yes — **mostly correct. 8/10.**

The main correction is the complexity:

* **Pattern:** ✅ Modified Binary Search
* **Brute force:** `O(n)`
* **Optimal average:** `O(log n)`
* **Worst case with duplicates:** ⚠️ **`O(n)`**
* **Space:** `O(1)`

The important change is not exactly “check nearby values.” The issue is when:

```text
nums[left] === nums[mid] === nums[right]
```

We **cannot determine which half is sorted** from those values.

So we safely shrink both sides:

```javascript
left++;
right--;
```

That can make the algorithm degrade to `O(n)` in the worst case.

### ⭐ Key note

```text
No duplicates:
Modified Binary Search → O(log n)

With duplicates:
Modified Binary Search → O(log n) average
                         O(n) worst case
```

This is an important example of how **duplicates can break the normal Binary Search guarantee**.


```javascript
function search(nums, target) {

    let left = 0;
    let right = nums.length - 1;

    while (left <= right) {

        const mid = Math.floor((left + right) / 2);

        if (nums[mid] === target) {
            return true;
        }

        // Duplicates make it impossible to determine
        // which side is sorted.
        if (
            nums[left] === nums[mid] &&
            nums[mid] === nums[right]
        ) {
            left++;
            right--;
            continue;
        }

        // Left half is sorted
        if (nums[left] <= nums[mid]) {

            if (
                nums[left] <= target &&
                target < nums[mid]
            ) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }

        } 
        // Right half is sorted
        else {

            if (
                nums[mid] < target &&
                target <= nums[right]
            ) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }

    return false;
}
```

**Key addition compared with Search in Rotated Sorted Array I:**

```javascript
if (nums[left] === nums[mid] && nums[mid] === nums[right]) {
    left++;
    right--;
}
```

That's the main part to remember for the **duplicate-element version**.

### Question
So when you say worst case, which means that all the elements of the array is same, just one is not. According to me, the worst case will be like the element just after the calculated first mid value, I think, right? Because that is how the for each loop, we will just do left plus plus, right minus minus. And at the end, we will reach to that unique element or that searchable element we want to search it. So, yeah, and doing left plus plus and right minus minus, so the mid value will be always the same.

You're **very close**, but one correction: the worst case doesn't require the unique element to be immediately after the first `mid`.

The real worst case is when we repeatedly get:

```text
nums[left] === nums[mid] === nums[right]
```

so we are forced to do:

```javascript
left++;
right--;
```

For example:

```text
[2, 2, 2, 2, 2, 2, 2, 2, 3, 2, 2]
```

If we're searching for `3`, the algorithm may keep shrinking from both ends until it finally reaches `3`.

### About your `mid` observation

Yes, **conceptually you're right that we're not getting the usual `mid`-based elimination**.

But `mid` is recalculated every iteration:

```javascript
mid = Math.floor((left + right) / 2);
```

So it doesn't necessarily remain the same index. The **search range shrinks by only one from each side**, rather than eliminating half the search space.

That's why:

```text
Normal Binary Search:
n → n/2 → n/4 → n/8 ...
O(log n)

Duplicate worst case:
n → n-2 → n-4 → n-6 ...
O(n)
```

⭐ **Key idea:** duplicates can make us lose the information needed to discard half the array. That's the reason the worst case becomes `O(n)`.

Yes — **So yes, as long as the shrinking happens symmetrically and the new left + right still produces the same midpoint, mid can remain the same for multiple iterations.** 👍

```text
[2, 2, 2, 2, 2, 3, 2, 2]
```

First:

```text
left = 0
right = 7
mid = 3
```

Since:

```text
nums[left] = nums[mid] = nums[right] = 2
```

we do:

```text
left++
right--
```

Now:

```text
left = 1
right = 6
mid = 3
```

Again `mid` is **3**.

Next:

```text
left = 2
right = 5
mid = 3
```

Again `mid` is **3**.

So yes, **as long as the shrinking happens symmetrically and the new `left + right` still produces the same midpoint, `mid` can remain the same for multiple iterations.**

Eventually, when the range changes enough, `mid` will change.

The more important point is:

> We're not eliminating half the search space; we're only removing one element from each side, which is why this can degrade to `O(n)`.**

