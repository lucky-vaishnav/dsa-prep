### Question

Given:

```text
nums = [1, 2, 1, 2, 3]    
k = 3
```

Find the **length of the longest contiguous subarray containing at most `k` distinct elements**.

Explain:

1. Your approach.
2. What information you need to maintain.
3. When you expand the range.
4. When and why you shrink it.
5. Time and space complexity.

### My Thoughts-
So for this question, containing most k distinct elements. So from this problem, I can understand that we need to find subarray length which have most k distinct element. Distinct means, I think unique element. So we will be using a hash map, which will be storing the indexes of that element. The key will be that element and hash map, and plus variable, size sliding window. When hash map already have this element, then we can check for distinctness, duplicacy. And this will we will use. So hash map and sliding window will be the key, and we will keep calculating the max length by using this approach. O of n time complexity, O of n space complexity. And please share the code as well for this problem.

Exactly. Your pattern identification is **correct**: **variable-size sliding window + HashMap frequency**.

I'd give your explanation **9/10**.

One small correction: for this problem, we don't need to store the **index** of each element. We need its **frequency inside the current window**.

For example:

```text
nums = [1, 2, 1, 2, 3]
k = 3
```

At some point the window could be:

```text
[1, 2, 1, 2]
```

The frequency map is:

```text
1 → 2
2 → 2
```

There are only **2 distinct elements**, so the window is valid.

When we add `3`:

```text
[1, 2, 1, 2, 3]
```

Now:

```text
1 → 2
2 → 2
3 → 1
```

There are **3 distinct elements**, still valid.

If there were 4 distinct elements, we'd shrink from the left until the number of distinct elements becomes `<= k`.

### Code

```js
function longestSubarrayAtMostKDistinct(nums, k) {
    const freq = new Map();

    let left = 0;
    let maxLength = 0;

    for (let right = 0; right < nums.length; right++) {
        // Add current element
        freq.set(nums[right], (freq.get(nums[right]) || 0) + 1);

        // Too many distinct elements → shrink window
        while (freq.size > k) {
            const leftElement = nums[left];

            freq.set(leftElement, freq.get(leftElement) - 1);

            // Remove completely if its frequency becomes 0
            if (freq.get(leftElement) === 0) {
                freq.delete(leftElement);
            }

            left++;
        }

        // Current window is valid
        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
```

For:

```text
[1, 2, 1, 2, 3]
k = 3
```

the answer is:

```text
5
```

because the entire array contains exactly 3 distinct elements.

### The important distinction

You said:

> "When hashmap already have this element, then we can check for distinctness."

Almost—but **whether the element already exists doesn't determine whether the window is valid**.

The key condition is:

```js
freq.size > k
```

Because `freq.size` = **number of distinct elements currently inside the window**.

And when shrinking, don't immediately delete the element when you encounter it. Decrease its frequency first:

```js
freq.set(leftElement, freq.get(leftElement) - 1);
```

Only delete it when:

```js
freq.get(leftElement) === 0
```

That distinction is very important for sliding-window problems involving duplicates.

**Complexity:**

* Time: **O(n)** — each element enters and leaves the window at most once.
* Space: **O(k)** in the usual bounded-distinct interpretation, since the map holds at most `k + 1` entries during processing; more generally **O(min(n, number of distinct values))**. Saying O(n) is also a valid loose upper bound, but O(k) is more precise here.
