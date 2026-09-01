### 🔵 Q — : Largest Rectangle in Histogram
https://leetcode.com/problems/largest-rectangle-in-histogram/
```text
heights = [2, 1, 5, 6, 2, 3]

Output = 10
```

The largest rectangle is:

```text
[5, 6]
```

with:

```text
height = 5
width = 2
area = 10
```

Think about:

* Brute-force approach
* Which previously learned pattern might apply?
* What does the **nearest smaller element** have to do with the problem?
* Could a Monotonic Stack help?
* What should the stack store: values or indices?
* Time and space complexity?

This is intentionally a **stronger Monotonic Stack problem** than Daily Temperatures/Next Greater Element.

### Review

* **Brute force:** `O(n²)` ✅
* **Optimal:** Monotonic **increasing** stack ✅
* **Stack stores indices:** ✅
* When a **smaller height** arrives, pop from the stack and calculate the rectangle that can extend up to that boundary. ✅
* Indices let us calculate the rectangle's **width**. ✅
* **Time:** `O(n)` ✅
* **Space:** `O(n)` ✅

The important correction is this:

> The maximum area is **not necessarily the area at the moment we pop** using only the current element. The popped height can extend from its previous smaller boundary all the way to the current smaller boundary.

For example:

```text
heights = [2, 1, 5, 6, 2, 3]
```

When we reach `2`, we start popping:

```text
height 6 → width 1 → area 6
height 5 → width 2 → area 10
```

The `5` can cover:

```text
[5, 6]
```

so:

```text
5 × 2 = 10
```

---

## Brute Force

A straightforward brute-force version is: for every starting index, keep extending the rectangle and maintain the minimum height.

```javascript
function largestRectangleArea(heights) {
    let maxArea = 0;

    for (let i = 0; i < heights.length; i++) {

        let minHeight = Infinity;

        for (let j = i; j < heights.length; j++) {

            minHeight = Math.min(
                minHeight,
                heights[j]
            );

            const width = j - i + 1;
            const area = minHeight * width;

            maxArea = Math.max(maxArea, area);
        }
    }

    return maxArea;
}
```

### Complexity

```text
Time  → O(n²)
Space → O(1)
```

---

## Optimal — Monotonic Increasing Stack

```javascript 
function largestRectangleArea(heights) {
    const stack = [];
    let maxArea = 0;

    for (let i = 0; i <= heights.length; i++) {

        const currentHeight =
            i === heights.length ? 0 : heights[i];

        while (
            stack.length > 0 &&
            currentHeight < heights[stack[stack.length - 1]]
        ) {
            const heightIndex = stack.pop();
            const height = heights[heightIndex];

            const width =
                stack.length === 0
                    ? i
                    : i - stack[stack.length - 1] - 1;

            const area = height * width;

            maxArea = Math.max(maxArea, area);
        }

        stack.push(i);
    }

    return maxArea;
}
```

### Why the increasing stack?

We maintain:

```text
heights[stack[0]]
    ≤
heights[stack[1]]
    ≤
heights[stack[2]]
    ...
```

When a smaller height arrives:

```text
currentHeight < stack top
        ↓
     POP
        ↓
popped height has found
its RIGHT smaller boundary
```

And the new stack top gives its **LEFT smaller boundary**.

So:

```text
width =
rightSmallerIndex
-
leftSmallerIndex
-
1
```

This is the key idea behind the problem.

### ⭐ Pattern connection

You can now connect these three problems:

```text
Daily Temperatures
        ↓
Next Greater Element
        ↓
Largest Rectangle
```

All use **Monotonic Stack**, but the question changes what boundary we're looking for:

* **Daily Temperatures** → next greater temperature
* **Next Greater Element** → next greater element
* **Largest Rectangle** → nearest smaller boundaries

This is exactly the kind of progression I want for your Phase 1: **recognize the underlying pattern rather than memorize individual solutions.**


