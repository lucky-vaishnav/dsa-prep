**Q**

This one is a **new variation/pattern**, so I'm announcing it before you start.

### 🆕 Pattern: Monotonic Deque for Sliding-Window Maximum

Given:

```text
nums = [1, 3, -1, -3, 5, 3, 6, 7]
k = 3
```

Find the **maximum value in every contiguous window of size `k`**.

Expected output:

```text
[3, 3, 5, 5, 6, 7]
```

For Q2, explain:

* Your approach
* What the deque stores
* Why we remove elements from the **back**
* Why we remove elements from the **front**
* Time and space complexity

**Important:** Don't code yet. First give me your approach for Q1 and Q2, then I'll review it.

---
The key points are exactly :

* Store **indices**, not values.
* Deque maintains **decreasing values** from front → back.
* Front always represents the **maximum** for the current window.
* **Time:** `O(n)`
* **Space:** `O(k)` because the deque contains at most `k` indices.

### Q2 — Sliding Window Maximum

```js
function maxSlidingWindow(nums, k) {
    const deque = []; // stores indices
    const result = [];

    for (let right = 0; right < nums.length; right++) {

        // 1. Remove indices that are outside the current window
        while (deque.length > 0 && deque[0] <= right - k) {
            deque.shift();
        }

        // 2. Remove smaller elements from the back
        // They can never become maximum while nums[right] is in the window
        while (
            deque.length > 0 &&
            nums[deque[deque.length - 1]] <= nums[right]
        ) {
            deque.pop();
        }

        // 3. Add current index
        deque.push(right);

        // 4. Window is ready once we have k elements
        if (right >= k - 1) {
            result.push(nums[deque[0]]);
        }
    }

    return result;
}

console.log(
    maxSlidingWindow([1, 3, -1, -3, 5, 3, 6, 7], 3)
);

// [3, 3, 5, 5, 6, 7]
```

### One important implementation detail in JavaScript

The conceptual operation is:

```text
remove from front → O(1)
```

But **`Array.shift()` is generally O(n)** because the remaining elements may need to be reindexed.

For interview-quality JavaScript, I'd implement the deque with a `head` pointer:

```js
function maxSlidingWindow(nums, k) {
    const deque = []; // indices
    let head = 0;
    const result = [];

    for (let right = 0; right < nums.length; right++) {

        // Remove indices outside the window
        while (
            head < deque.length &&
            deque[head] <= right - k
        ) {
            head++;
        }

        // Remove smaller values from the back
        while (
            head < deque.length &&
            nums[deque[deque.length - 1]] <= nums[right]
        ) {
            deque.pop();
        }

        deque.push(right);

        // Window size >= k
        if (right >= k - 1) {
            result.push(nums[deque[head]]);
        }
    }

    return result;
}

console.log(
    maxSlidingWindow([1, 3, -1, -3, 5, 3, 6, 7], 3)
);

// [3, 3, 5, 5, 6, 7]
```

### The mental model to remember

```text
Deque = candidates for maximum

Front → largest / current maximum
        ↓
       ...
        ↓
Back  → smallest candidate
```

When a new value arrives:

1. **Expired indices → remove from front**
2. **Smaller values → remove from back**
3. **Add current index to back**
4. **Front gives the maximum**

This is an important monotonic-deque pattern because it generalizes beyond just sliding-window maximum.

