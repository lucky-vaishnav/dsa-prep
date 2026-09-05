### Q

Given:

```text
nums = [2, 1, 5, 1, 3, 2]   // negative values can also be there
k = 3
```

Find the **maximum sum of any contiguous subarray of exactly `k` elements**.

Explain:

1. Your approach.
2. Why it works.
3. How you'd maintain the window.
4. Time and space complexity.

Don't code yet—walk me through your thinking first.

---

Yes — **the core approach is correct**, and you correctly identified why negative values don't matter for a fixed-size window.


### Small correction

You said:

> `i - K >= K`

That's not the condition we want.

If `i` is the current index and `K = 3`, the window becomes size 3 when:

```text
i >= K - 1
```

So for `K = 3`:

```text
i >= 2
```

At `i = 2`, the first window is:

```text
[2, 1, 5]
```

Then when moving to `i = 3`, we remove the element at:

```text
i - K = 3 - 3 = 0
```

So the standard implementation is:

```js
function maxSumSubarray(nums, k) {
    let windowSum = 0;
    let maxSum = -Infinity;

    for (let i = 0; i < nums.length; i++) {
        windowSum += nums[i];

        // Window has reached size k
        if (i >= k - 1) {
            maxSum = Math.max(maxSum, windowSum);

            // Remove the element leaving the window
            windowSum -= nums[i - k + 1];
        }
    }

    return maxSum;
}
```

For:

```text
[2, 1, 5, 1, 3, 2]
k = 3
```

the windows are:

```text
[2, 1, 5] → 8
[1, 5, 1] → 7
[5, 1, 3] → 9
[1, 3, 2] → 6
```

So the answer is **9**.

### Your notes version

```text
Fixed-size Sliding Window

Use when:
- Window size is exactly K.
- We need to evaluate every contiguous group of K elements.

Approach:
1. Add the current element to windowSum.
2. Once window size reaches K:
   - Update the answer.
   - Remove the element that is leaving the window.
3. Continue until the array ends.

Time: O(n)
Space: O(1)

Negative numbers are fine because the window size is fixed.
We never make decisions based on whether the sum became too large/small.
```

Your understanding of the **fixed vs variable sliding-window distinction** is the important part here.
