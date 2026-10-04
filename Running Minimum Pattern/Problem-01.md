## Q

Given an array of integers:

```text
nums = [4, 2, 7, 1, 8, 3]
```

Find the **maximum difference `nums[j] - nums[i]`** such that:

```text
j > i
```

In other words, the value being subtracted must occur **before** the value being subtracted from.

For the example, don't just give the answer. Explain:

1. Your approach.
2. What information you maintain while traversing.
3. Why you don't need to compare every pair.
4. Time and space complexity.

**Don't code yet.**

---
#### My Thoughts That Time:
Q1

1. two pointer
2. we check if left pint values is less then right pointer value if not then L=R and R++ and 
3. once a lesser values comes form the num which is currebtly used as num[i] (using lest pointer), will move pointers
4. time - o(n), space- o(1)

Your **O(n) / O(1)** complexity is correct, and you're thinking in the right direction with two pointers. But there's one important issue in the pointer logic.

For this problem:

```text
[4, 2, 7, 1, 8, 3]
```

we need to keep the **smallest value seen so far on the left**, then compare the current value against it.

The key idea is:

```text
minSoFar = smallest value from indices 0...i-1

currentDifference = nums[i] - minSoFar
```

So we don't actually need to maintain a traditional `left/right` window.

For example:

```text
i=0 → 4
minSoFar = 4

i=1 → 2
minSoFar = 2

i=2 → 7
7 - 2 = 5  ← best so far

i=3 → 1
minSoFar = 1

i=4 → 8
8 - 1 = 7  ← best

i=5 → 3
3 - 1 = 2
```

Answer = **7**, from:

```text
8 - 1
```

The important part is that `1` occurs **before** `8`, so the ordering condition is satisfied.

---

## Maximum Difference

**Problem:** `nums = [4, 2, 7, 1, 8, 3]`

We want maximum `nums[j] - nums[i]` where `j > i`.

Your earlier two-pointer intuition was close, but the clean pattern is **minimum-so-far**.

```js
function maxDifference(nums) {
    let minSoFar = nums[0];
    let maxDiff = -Infinity;

    for (let i = 1; i < nums.length; i++) {
        // Best difference if nums[i] is the selling/current value
        maxDiff = Math.max(maxDiff, nums[i] - minSoFar);

        // Keep the smallest value seen so far
        minSoFar = Math.min(minSoFar, nums[i]);
    }

    return maxDiff;
}

console.log(maxDifference([4, 2, 7, 1, 8, 3])); // 7
```

### Dry run

```text
nums:       4   2   7   1   8   3
minSoFar:   4   2   2   1   1   1
maxDiff:    -   -   5   5   7   7
```

Answer = `8 - 1 = 7`.

**Complexity:** `O(n)` time, `O(1)` space.
