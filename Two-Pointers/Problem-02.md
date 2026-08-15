### 🔵 —: 3Sum

```text
nums = [-1, 0, 1, 2, -1, -4]

Output = [
    [-1, -1, 2],
    [-1, 0, 1]
]
```

Find all **unique triplets** whose sum is `0`.

Think about:

* Brute force approach
* What pattern can reduce the complexity?
* How can we avoid duplicate triplets?
* Time & space complexity

**Don't worry if Q2 isn't immediately clear.** This is a good step up because it combines ideas you've already learned rather than introducing an entirely unrelated technique.

### My Thought-
So for this question, there is some problem. So for that, actually the brute force complexity will be O of n square, and we will be traversing the array. And within that traverse, we will traverse with the first element and the rest of the element, and we'll calculate total for the three elements. If it is equal to zero, then we will reset those sub till now values. So it will be O of n square. But I am still not sure what will be used to identify the unique subset. And for optimal approach, I am not sure what should be the approach, but according to me, in our last discussion, we have talked about this problem and while we were learning about the array reversal pattern with two pointers. So I think this is related to that. But yeah, you can share me the thought process and the code for it, for both brute force and whatever the best approach for it.

---
Yes — your instinct about **Two Pointers** is correct. This is a very good problem for connecting the pattern you've already learned.

One correction first: the straightforward brute-force approach is actually **O(n³)**, because we need to choose **three elements**.

## 1. Brute Force — O(n³)

We try every possible triplet:

```javascript
function threeSum(nums) {

    const resultSet = new Set();

    for (let i = 0; i < nums.length - 2; i++) {

        for (let j = i + 1; j < nums.length - 1; j++) {

            for (let k = j + 1; k < nums.length; k++) {

                if (nums[i] + nums[j] + nums[k] === 0) {

                    // Sort the triplet so that
                    // [-1, 0, 1] and [1, -1, 0]
                    // become the same key.
                    const triplet = [
                        nums[i],
                        nums[j],
                        nums[k]
                    ].sort((a, b) => a - b);

                    resultSet.add(triplet.join(','));
                }
            }
        }
    }

    // Convert Set keys back into arrays
    return [...resultSet].map(key =>
        key.split(',').map(Number)
    );
}
```

But this produces duplicates, so we'd need additional logic to remove duplicate triplets.

For example:

```text
[-1, 0, 1, 2, -1, -4]
```

could produce:

```text
[-1, 0, 1]
[-1, 0, 1]
...
```

We can use a `Set` with a sorted triplet as a key, but that doesn't improve the main complexity.

---

# 2. Optimal — Sorting + Two Pointers

This is the important part.

First sort:

```text
[-4, -1, -1, 0, 1, 2]
```

Now fix one element:

```text
i
↓
[-4, -1, -1, 0, 1, 2]
```

Then use two pointers:

```text
        left       right
          ↓          ↓
[-4, -1, -1, 0, 1, 2]
```

Calculate:

```text
sum = nums[i] + nums[left] + nums[right]
```

Then:

### If sum < 0

We need a **larger** sum:

```text
left++
```

### If sum > 0

We need a **smaller** sum:

```text
right--
```

### If sum === 0

We found a triplet:

```text
result.push(...)
```

Then move both pointers.

---

## Code

```javascript
function threeSum(nums) {

    nums.sort((a, b) => a - b);

    const result = [];

    for (let i = 0; i < nums.length - 2; i++) {

        // Skip duplicate first elements
        if (i > 0 && nums[i] === nums[i - 1]) {
            continue;
        }

        let left = i + 1;
        let right = nums.length - 1;

        while (left < right) {

            const sum = nums[i] + nums[left] + nums[right];

            if (sum === 0) {

                result.push([
                    nums[i],
                    nums[left],
                    nums[right]
                ]);

                // Skip duplicate left values
                while (
                    left < right &&
                    nums[left] === nums[left + 1]
                ) {
                    left++;
                }

                // Skip duplicate right values
                while (
                    left < right &&
                    nums[right] === nums[right - 1]
                ) {
                    right--;
                }

                left++;
                right--;

            } else if (sum < 0) {

                left++;

            } else {

                right--;
            }
        }
    }

    return result;
}
```

### Complexity

Sorting:

```text
O(n log n)
```

Then:

```text
n × two-pointer traversal
= O(n²)
```

Therefore:

```text
Time  = O(n²)
Space = O(1) auxiliary
```

Ignoring the output array.

---

## ⭐ The important connection for you

You were right to connect this with **Two Pointer + Array Sorting**.

The progression is:

```text
3 elements
   ↓
Fix 1 element
   ↓
Remaining 2 elements
   ↓
Two Pointer
```

And the sorting gives us the direction:

```text
sum < 0  → left++
sum > 0  → right--
```

### Duplicate handling is the extra part

There are **three places** where we prevent duplicates:

```text
1. Skip duplicate nums[i]

2. After finding a triplet,
   skip duplicate nums[left]

3. After finding a triplet,
   skip duplicate nums[right]
```

For example:

```text
[-1, -1, 0, 1, 1]
```

We don't want to return the same `[-1, 0, 1]` multiple times.

So your initial pattern recognition was **correct**, but the key upgrade is:

> **Sort → fix one element → solve the remaining 2Sum using Two Pointers.**

This is a very important pattern combination to remember.
