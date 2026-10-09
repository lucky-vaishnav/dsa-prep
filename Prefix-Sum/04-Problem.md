### Prefix Sum + Earliest Index

We've used prefix sums with a **frequency map** for counting subarrays. Now we're going to use the same prefix-sum idea for a different purpose: finding the **longest** valid subarray.

Given:

```text
nums = [1, -1, 5, -2, 3]
k = 3
```

Find the **length of the longest contiguous subarray whose sum is exactly `k`**.

Expected answer:

```text
4
```

Before coding, explain:

1. What will you store in the HashMap?
2. Why should we store the **earliest index**?
3. What condition will you check?
4. What will `map.set(0, -1)` represent?
5. Time and space complexity.

This is a useful variation of the prefix-sum pattern rather than another sliding-window problem.

---
#### My Thoughts-
1. What will you store in the HashMap? - earliest index of prefixSum
2.  Why should we store the **earliest index**? - to achive contiguous subarray   
3.  What condition will you check? currentPrefixSum-k exists in hashMap
4.  What will `map.set(0, -1)` represent?  prefix sum exists before the start
5.  Time and space complexity. - O(n), O(n)

---

You've identified the key pieces of the solution.

One refinement: we store the earliest index for each prefix sum because it gives us the longest possible subarray when that prefix sum is encountered again.

## Longest Subarray With Sum Exactly K

JavaScript solution

JavaScript

```
function longestSubarraySumK(nums, k) {
    let prefixSum = 0;
    let maxLength = 0;

    const prefixMap = new Map();

    // Prefix sum 0 exists before the array starts
    prefixMap.set(0, -1);

    for (let i = 0; i < nums.length; i++) {
        prefixSum += nums[i];

        const required = prefixSum - k;

        // Check whether a previous prefix sum gives sum k
        if (prefixMap.has(required)) {
            const length = i - prefixMap.get(required);
            maxLength = Math.max(maxLength, length);
        }

        // Store only the earliest index for each prefix sum
        if (!prefixMap.has(prefixSum)) {
            prefixMap.set(prefixSum, i);
        }
    }

    return maxLength;
}

console.log(longestSubarraySumK([1, -1, 5, -2, 3], 3));
// Output: 4
```

### Dry run

For `nums = [1, -1, 5, -2, 3]`, `k = 3`:

| Index | Value | Prefix sum | Required prefix (`sum - k`) | Best length |
| ----- | ----- | ---------- | --------------------------- | ----------- |
| 0     | 1     | 1          | -2                          | 0           |
| 1     | -1    | 0          | -3                          | 0           |
| 2     | 5     | 5          | 2                           | 0           |
| 3     | -2    | 3          | 0                           | 4           |
| 4     | 3     | 6          | 3                           | 4           |

At index `3`, the prefix sum is `3`. We previously stored prefix sum `0` at index `-1`.

Therefore:

length=3−(−1)=4\text{length}=3-(-1)=4length=3−(−1)=4

The longest subarray is `[1, -1, 5, -2]`, whose sum is `3`.

### Notes for your interview

* Pattern: Prefix Sum + HashMap (earliest index)

* Map: `prefixSum → earliest index`

* Condition: `prefixSum - k` exists in the map

* Initialization: `map.set(0, -1)` handles subarrays starting at index `0`.

* Important: Never overwrite an existing prefix sum's earliest index.

* Time: O(n)O(n)O(n)

* Auxiliary space: O(n)O(n)O(n)

This approach works with negative numbers, where a standard sliding window generally cannot guarantee correctness.
