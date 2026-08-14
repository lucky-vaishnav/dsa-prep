## Problem: Longest Consecutive Sequence

Given an unsorted array of integers, return the length of the **longest consecutive elements sequence**.

Your algorithm must run in **O(n)** time.

### Example

```
Input:
[100,4,200,1,3,2]

Output:
4
```

Explanation:

```
1,2,3,4
```

is the longest consecutive sequence.

---

### Tell me:

```
Pattern:
Why:
Brute Force Complexity:
Optimal Data Structure:
Optimal Approach:
Time Complexity:
Space Complexity:
```

💡 **Hint:** We've revised this a couple of times. Remember the trick that avoids starting from every number.

> **Only start counting when the current number is the beginning of a sequence (`num - 1` doesn't exist).**
> 

That is exactly the interview insight.

> **Brute Force**
> 

Sorting is **not** brute force.

- **True Brute Force:** For every number, keep checking `num+1`, `num+2`, ... using a linear search.
    - **Time:** `O(n²)` (or worse depending on implementation)
- **Better Approach (Sorting):**
    - Sort the array, then count consecutive elements.
    - **Time:** `O(n log n)`

So sorting is an **improved approach**, but not the optimal one.

---

# Brute Force (O(n²))

```jsx
function longestConsecutive(nums) {

    let maxLength = 0;

    for (let i = 0; i < nums.length; i++) {

        let current = nums[i];
        let length = 1;

        while (nums.includes(current + 1)) {
            current++;
            length++;
        }

        maxLength = Math.max(maxLength, length);
    }

    return maxLength;
}
```

---

# Sorting Approach (O(n log n))

```jsx
function longestConsecutive(nums) {

    if (nums.length === 0) return 0;

    nums.sort((a, b) => a - b);

    let maxLength = 1;
    let currentLength = 1;

    for (let i = 1; i < nums.length; i++) {

        if (nums[i] === nums[i - 1]) {
            continue;
        }

        if (nums[i] === nums[i - 1] + 1) {
            currentLength++;
        } else {
            maxLength = Math.max(maxLength, currentLength);
            currentLength = 1;
        }
    }

    return Math.max(maxLength, currentLength);
}
```

---

# HashSet Approach (O(n))

```jsx
function longestConsecutive(nums) {

    // Key Idea:
    // Only start counting when the current number is
    // the START of a sequence.
    // A number is the start only if (num - 1) does NOT exist.
    // This prevents counting the same sequence multiple times.

    const set = new Set(nums);

    let maxLength = 0;

    for (const num of set) {

        if (!set.has(num - 1)) {

            let current = num;
            let length = 1;

            while (set.has(current + 1)) {
                current++;
                length++;
            }

            maxLength = Math.max(maxLength, length);
        }
    }

    return maxLength;
}
```

---

## ⭐ The one-line interview memory trick

```
Only start counting when the current number is the beginning of a sequence.

Beginning means:

(num - 1) does NOT exist.

This guarantees every consecutive sequence is counted exactly once.
```

This is the single most important idea of the problem. If you remember just this one line, you'll always be able to derive the solution instead of memorizing it.

---
### Question- For HashSet approach time complexitiy - Why isn't it O(n²)?

Your concern is very common here. The key is that **the `while` loop does not run `O(n)` times for every element**.

Suppose:

```text
nums = [100, 4, 200, 1, 3, 2]
```

We put everything into a `Set`:

```text
{100, 4, 200, 1, 3, 2}
```

Then:

```javascript
for (const num of nums) {
    if (!set.has(num - 1)) {

        let current = num;

        while (set.has(current + 1)) {
            current++;
        }
    }
}
```

### Why isn't it O(n²)?

Because the `while` loop only starts for the **beginning of a sequence**.

For:

```text
1, 2, 3, 4
```

When we reach `1`:

```text
1 → 2 → 3 → 4
```

The `while` loop does 3 iterations.

But when we later reach:

```text
2
```

we check:

```text
set.has(1) → true
```

So `2` is **not a sequence starting point**.

Same for `3` and `4`.

Therefore, that sequence is traversed only **once**.

### The important amortized-analysis idea

Across the entire algorithm, each element participates in the consecutive-chain traversal at most once.

So:

```text
Outer for loop       → O(n)
All while iterations → O(n) total
Set operations       → O(1) average
--------------------------------
Total                → O(n)
```

Therefore:

**HashSet approach = `O(n)` average time, `O(n)` space.**

Your `O(n × d)` reasoning would be correct **if the `while` loop could traverse the same sequence repeatedly for every element**. The `num - 1` check is precisely what prevents that.

And yes, this is why the HashSet solution is better than sorting:

```text
Sorting approach → O(n log n)
HashSet approach → O(n) average
```

⭐ **This is a very important DSA concept: amortized analysis.** A nested loop does **not automatically mean `O(n²)`**; you need to look at the **total number of iterations across the whole algorithm**.

----
### Question -  what is time complexity of creating new set from an array?

const myArray = [1, 2, 2, 3];
const mySet = new Set(myArray); // O(N) time



