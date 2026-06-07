### 1️⃣ What is Monotonic Queue / Deque?

A **Monotonic Deque** is a **double-ended queue** where elements are kept in **increasing or decreasing order**.

### Two types:

1. **Monotonic Increasing** → front has **smallest**
2. **Monotonic Decreasing** → front has **largest**

📌 The deque always stays **sorted in one direction**.

---

### 2️⃣ Is it a Unique Pattern or Subset?

### ✅ Short answer:

> It is a unique pattern, but it combines concepts from other patterns.
> 

### Relation to other patterns:

| Pattern | Relation |
| --- | --- |
| Sliding Window | ⭐ Monotonic deque is **mostly used inside sliding window** |
| Stack | Logic similar to **monotonic stack**, but with window removal |
| Two Pointers | Window boundaries often move using pointers |
| Greedy | We discard useless elements greedily |

📌 **Interview framing**

> “Monotonic Queue is a specialized data structure pattern, commonly used with Sliding Window problems.”
> 

---

### 3️⃣ When Should You Think of Monotonic Deque? 🧠

Look for:

- “**maximum/minimum in every window of size k**”
- “**sliding window max / min**”
- “next greater / smaller **with window constraint**”
- brute force = `O(n*k)` → needs `O(n)`

👉 **This is the biggest signal**

---

### 4️⃣ Core Idea (Very Important)

### We store **indices**, not values

Why?

- To check if element is **out of window**
- To compare values using array

---

### 5️⃣ Monotonic Deque Template (Sliding Window Maximum)

### Problem:

**LeetCode 239 – Sliding Window Maximum**

---

### ✅ Template (KEEP THIS FOR NOTES)

```jsx
functionslidingWindowMax(nums, k) {
const deque = [];// stores indices
const result = [];

for (let i =0; i < nums.length; i++) {

// 1️⃣ Remove indices out of window
if (deque.length && deque[0] <= i - k) {
      deque.shift();
    }

// 2️⃣ Maintain decreasing order
while (deque.length && nums[deque[deque.length -1]] <= nums[i]) {
      deque.pop();
    }

// 3️⃣ Add current index
    deque.push(i);

// 4️⃣ Window formed
if (i >= k -1) {
      result.push(nums[deque[0]]);
    }
  }

return result;
}

```

---

### 6️⃣ Why This Works (Interview Explanation)

- Deque front always stores **max element index**
- Smaller elements behind a bigger element are **useless**
- Each element is **added once and removed once**

⏱️ **Time Complexity:** `O(n)`

📦 **Space Complexity:** `O(k)`

---

### 7️⃣ Visual Intuition 🧠

For `nums = [1,3,-1,-3,5,3,6,7], k = 3`

Deque stores indices of **useful candidates only**

```
Window: [1,3,-1] → max = 3
Deque: [3, -1]  (indices)

```

When `5` arrives:

- remove all smaller values
- deque becomes `[5]`

---

### 8️⃣ Common Variations

### 🔹 Sliding Window Minimum

Just flip comparison:

```jsx
nums[deque[deque.length -1]] >= nums[i]

```

---

### 🔹 Max/Min in Fixed Range

Same template, just tweak window logic.

---

### 9️⃣ Must-Do LeetCode Questions 🔥

### 🟢 Easy

- **1438** – Longest Continuous Subarray With Abs Diff ≤ Limit

### 🟡 Medium (CORE)

- **239** – Sliding Window Maximum ⭐
- **862** – Shortest Subarray with Sum at Least K
- **1696** – Jump Game VI

### 🔴 Hard

- **1425** – Constrained Subsequence Sum
- **1499** – Max Value of Equation

📌 If you master **239 + 862**, you’re solid.

---

### 🔟 Monotonic Queue vs Monotonic Stack

| Feature | Stack | Queue |
| --- | --- | --- |
| Direction | One side | Both ends |
| Window removal | ❌ | ✅ |
| Use case | Next greater/smaller | Sliding window max/min |

---

### 1️⃣1️⃣ One-Page Revision Notes (Save This)

### When to use:

- Sliding window + max/min
- Optimize `O(n*k)` → `O(n)`

### Key rules:

- Store **indices**
- Remove out-of-window elements
- Maintain monotonic order
- Front = answer

### Complexity:

- Time: `O(n)`
- Space: `O(k)`

---

### 1️⃣2️⃣ Interview One-Liner 💬

> “Monotonic deque maintains candidates for max/min in a sliding window by removing useless elements greedily, achieving O(n) time.”
> 

---
