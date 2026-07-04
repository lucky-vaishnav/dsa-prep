Given an array:

```
nums = [1,3,-1,-3,5,3,6,7]
k = 3
```

Return the **maximum** element in every sliding window of size `k`.

Example:

```
Input:
nums = [1,3,-1,-3,5,3,6,7]
k = 3

Output:
[3,3,5,5,6,7]
```

Explanation:

```
Window [1,3,-1]   -> 3
Window [3,-1,-3]  -> 3
Window [-1,-3,5]  -> 5
Window [-3,5,3]   -> 5
Window [5,3,6]    -> 6
Window [3,6,7]    -> 7
```

---

Tell me:

```
Pattern:
Why:
Brute Force Complexity:
Optimal Data Structure:
Optimal Approach:
Time Complexity:
Space Complexity:
```

### Pattern

If you think:I

```
Sliding Window
```

🟡 **Partially correct.**

There are actually **three approaches** to this problem.

| Approach | Time | Space |
| --- | --- | --- |
| Brute Force | O(n × k) | O(1) |
| Sliding Window (recalculate max every window) | O(n × k) | O(1) |
| ⭐ Monotonic Deque | O(n) | O(k) |

So yes, there **is** a sliding window, but **sliding window alone isn't enough** to achieve `O(n)`.

---

# Why Sliding Window Alone Doesn't Work

Suppose

```
nums = [1,3,-1,-3,5]
k = 3
```

Window

```
[1,3,-1]
```

Maximum

```
3
```

Move window

```
[3,-1,-3]
```

Maximum

```
3
```

Move again

```
[-1,-3,5]
```

How do you know the maximum is `5`?

With only a normal sliding window, you have to scan the entire window again.

That costs

```
O(k)
```

for every window.

Total:

```
O(n × k)
```

---

# Why We Need a New Data Structure

We need a structure that can answer:

> **"What's the maximum element in the current window?"**
> 

without scanning all `k` elements every time.

That's exactly what a **Monotonic Deque** does.

---

# Pattern Recognition

Add this to your notebook:

```
Sliding Window Maximum

Recognition Clues:
- Window of fixed size k
- Need maximum/minimum in every window

Brute Force:
Check every window completely

Time:
O(n × k)

Optimal Pattern:
Monotonic Queue (Deque)

Time:
O(n)

Space:
O(k)
```

---

# Problem

```
nums= [1,3,-1,-3,5,3,6,7]
k=3
```

Output

```
[3,3,5,5,6,7]
```

---

# Why Monotonic Deque?

The deque always stores **indices**, not values.

The values at those indices are maintained in **decreasing order**.

Example:

```
Deque:

[3,2,1]
```

means

```
Front -----> Back

Largest     Smallest
```

So the front always contains the maximum element of the current window.

---

# Approach

### Step 1

Create

```
constdeque= [];
constresult= [];
```

Deque stores indices.

---

### Step 2

For every index

```
right=0→ n-1
```

---

### Step 3

Remove elements outside the window

If

```
deque[0]<=right-k
```

then

```
deque.shift();
```

because that index is no longer inside the current window.

---

### Step 4

Maintain decreasing order

While

```
nums[right]>=nums[deque[last]]
```

remove from back.

```
deque.pop();
```

Reason:

If a bigger number arrives, the smaller number behind it can **never** become the maximum in any future window.

---

### Step 5

Push current index

```
deque.push(right);
```

---

### Step 6

If first window is complete

```
right>=k-1
```

answer is

```
nums[deque[0]]
```

because front is always maximum.

---

# Code

```jsx
function maxSlidingWindow(nums, k) {
  const deque = [];
  const result = [];

  for (let right = 0; right < nums.length; right++) {
    // Remove indices outside current window
    while (deque.length && deque[0] <= right - k) {
      deque.shift();
    }

    // Maintain decreasing order
    while (deque.length && nums[right] >= nums[deque[deque.length - 1]]) {
      deque.pop();
    }

    // Add current index
    deque.push(right);

    // Store answer once first window is complete
    if (right >= k - 1) {
      result.push(nums[deque[0]]);
    }
  }

  return result;
}

console.log(maxSlidingWindow([1, 3, -1, -3, 5, 3, 6, 7], 3));
```

Output
```
[3,3,5,5,6,7]
```

---

# The Most Important Interview Insight

Many people ask:

> **Why do we remove smaller elements from the back?**
> 

Imagine:

```
Deque

8 5 2
```

Now

```
9
```

arrives.

Can

```
8
```

ever be the maximum of a future window?

**No.**

Because:

- `9` is larger.
- `9` entered later, so it will stay in the window **longer** than `8`.

The same logic applies to `5` and `2`.

So we safely remove them.

This is the key idea behind a **Monotonic Deque**.
