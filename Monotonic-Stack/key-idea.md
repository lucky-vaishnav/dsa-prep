## **Monotonic Stack(maintain a stack that is always increasing or always decreasing.)**

**When to use:**

Next greater/smaller element, stock span, histogram area.

**Common problems:**

- Next greater element
- Daily temperatures
- Largest rectangle in histogram

**Key idea:**

Maintain stack in monotonic order.

## 🧠 1. How to Identify a Monotonic Stack Problem Instantly

If the problem asks any of these:

✔ "Next greater element"

✔ "Next smaller element"

✔ "Previous greater/smaller element"

✔ "Next element to the left/right that satisfies a condition"

✔ "Span/distance until the next larger/smaller value"

✔ "Optimize O(n²) comparisons to O(n) using a stack"

✔ "Histogram/rectangle area/stock span"

## Monotonic Stack Template (JavaScript)

### Template for **next greater element**

```jsx
function nextGreaterElement(nums) {
    let stack = [];  // stores indexes
    let res = new Array(nums.length).fill(-1);

    for (let i = 0; i < nums.length; i++) {
        while (stack.length && nums[i] > nums[stack[stack.length - 1]]) {
            let idx = stack.pop();
            res[idx] = nums[i];
        }
        stack.push(i);
    }
    return res;
}
```

### Template for **next smaller element**

```jsx
while (stack.length && nums[i] < nums[stack[top]]) {
    // same logic but checking <
}
```

### Template for **previous greater/smaller**

→ iterate from **right-to-left** instead of left-to-right.

---

## 📚  LeetCode Problems to Practice (in perfect learning order)

### ✅ **Level 1 — Basics (Learn the Pattern)**

1. **496. Next Greater Element I**
2. **503. Next Greater Element II (Circular array)**
3. **739. Daily Temperatures**
4. **901. Online Stock Span**

### ✅ **Level 2 — Apply the Pattern**

1. **84. Largest Rectangle in Histogram** (MOST IMPORTANT)
2. **85. Maximal Rectangle** (Uses histogram logic)
3. **42. Trapping Rain Water** (Monotonic decreasing stack approach)

### ✅ **Level 3 — Advanced Applications**

1. **321. Create Maximum Number**
2. **1673. Find the Most Competitive Subsequence**
3. **1687. Delivering Boxes from Storage to Ports** (complex stack + greedy)

---

## ✔️ Quick Real-World Examples to Make It Easy

### Example 1 — “Daily Temperatures”

> Find how many days until a warmer temperature.
> 

This is exactly "next greater element" → **use monotonic decreasing stack**.

---

### Example 2 — “Largest Rectangle in Histogram”

> Find biggest rectangle using heights.
> 

This needs **previous smaller** and **next smaller** for every bar → classic monotonic stack.

---

### Example 3 — “Trapping Rain Water”

> Find how much water is trapped.
> 

You look for **previous higher** and **next higher** → monotonic decreasing stack.
