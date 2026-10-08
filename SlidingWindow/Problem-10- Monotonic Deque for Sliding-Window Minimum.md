### Q — 🆕 New Pattern: Monotonic Deque — Minimum

You've just learned **Sliding Window Maximum using a monotonic decreasing deque**.

Now we'll learn the natural companion variation: **Sliding Window Minimum**.

Given:

```text
nums = [1, 3, -1, -3, 5, 3, 6, 7]
k = 3
```

Find the minimum value in every window of size `k`.

Expected output:

```text
[-1, -3, -3, -3, 3, 3]
```

Before coding, explain:

* What will the deque store?
* Increasing or decreasing order?
* What do you remove from the front?
* What do you remove from the back?
* Where is the minimum located?
* Complexity?

**Don't code yet—give me both approaches first.**

---
#### My Answer-

1. What will the deque store? - indexes of nums  where nums are in increasing order
2.  Increasing or decreasing order?  - increasing order
3.  What do you remove from the front?  expired indexes 
4.  What do you remove from the back?   larger values
5.  Where is the minimum located? at front
6.  Complexity? time o(n), space -0(k)
7. also share code for this problem for my notes
---
Exactly right.

You correctly identified the mirror image of the maximum problem:

* **Sliding Window Maximum:** decreasing deque → maximum at front
* **Sliding Window Minimum:** increasing deque → minimum at front
* Store **indices**, not values.
* Remove expired indices from the **front**.
* Remove larger/equal candidates from the **back**.

### Q — Sliding Window Minimum

```js
function minSlidingWindow(nums, k) {
    const deque = []; // stores indices
    let head = 0;
    const result = [];

    for (let right = 0; right < nums.length; right++) {

        // 1. Remove indices outside the current window
        while (
            head < deque.length &&
            deque[head] <= right - k
        ) {
            head++;
        }

        // 2. Remove larger/equal values from the back
        // They can never become the minimum while nums[right] exists
        while (
            head < deque.length &&
            nums[deque[deque.length - 1]] >= nums[right]
        ) {
            deque.pop();
        }

        // 3. Add current index
        deque.push(right);

        // 4. Window is ready once we have k elements
        if (right >= k - 1) {
            result.push(nums[deque[head]]);
        }
    }

    return result;
}

console.log(
    minSlidingWindow([1, 3, -1, -3, 5, 3, 6, 7], 3)
);

// [-1, -3, -3, -3, 3, 3]
```

### Notes version

```text
Sliding Window Minimum

Deque:
- Stores indices
- Maintains increasing order of values
- Front = minimum

For every new element:
1. Remove expired indices from front
2. Remove larger/equal values from back
3. Add current index
4. Once window size >= k, front gives minimum

Time:  O(n)
Space: O(k)
```

You now have the two fundamental monotonic-deque variants:

```text
Maximum → decreasing deque → front = maximum
Minimum → increasing deque → front = minimum
```

This is a good point to move to a **different pattern/variation** rather than doing another nearly identical deque problem.

