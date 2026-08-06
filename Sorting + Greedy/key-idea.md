## Problem: Merge Intervals (LeetCode 56)

```text
Input:
intervals = [[1,3],[2,6],[8,10],[15,18]]

Output:
[[1,6],[8,10],[15,18]]
```

Tell me:

* Pattern
* Why
* Brute Force Complexity
* Optimal Data Structure
* Optimal Approach
* Time Complexity
* Space Complexity

After your answer, I'll share:

* Brute force code
* Optimal code
* Any alternative approaches

---

# My Answer That Time -
So for question number one, merge interval problem, brute force complexity will be O of n square for worst case, and optimal data structure will be, for this problem to use will be a stack, monotonic stack with the increasing order of indexes, which have increasing value maintained. My optimal approach will be monotonic stack, I think, time complexity O of n, and space complexity will be O of n in worst cases. Yeah, and also share the code for possible approaches, and best approach, like brute force as well, and if there is anything else.

Nice attempt! This is actually a very common misconception. **Merge Intervals is NOT a Stack problem.**

I'd give this **5/10** because your complexity and pattern need correction, but that's expected since this is your first time seeing it.

---

# Verification

## Pattern

❌ Monotonic Stack

✅ Correct Pattern:

```text
Sorting + Greedy
```

This is an important **new pattern** for your notes.

---

## Why?

After sorting by the **start time**, we only need to compare the **current merged interval** with the **next interval**.

No stack or monotonic property is required.

---

## Brute Force

One possible brute force approach:

* Compare every interval with every other interval.
* Merge repeatedly until no more merges are possible.

Time:

```text
O(n²)
```

✔️ Correct.

---

## Optimal Data Structure

❌ Stack

✅ Just an output array (`result`).

No special data structure.

---

## Optimal Approach

1. Sort intervals by start.
2. Add the first interval to `result`.
3. For every next interval:

   * If it overlaps with the last interval in `result`, merge them.
   * Otherwise, push it as a new interval.

---

## Complexity

Sorting:

```text
O(n log n)
```

Traversal:

```text
O(n)
```

Total:

```text
O(n log n)
```

❌ Not `O(n)` because sorting dominates.

Space:

```text
O(n)
```

---

# Approaches

## 1. Brute Force

**Time**

```text
O(n²)
```

**Space**

```text
O(n)
```

Not preferred.

---

## 2. Sorting + Greedy ⭐⭐⭐⭐⭐ (Best)

**Time**

```text
O(n log n)
```

**Space**

```text
O(n)
```

This is the standard interview solution.

---

# Code

## Brute Force (Conceptual)

```javascript
function merge(intervals) {

    let merged = true;

    while (merged) {

        merged = false;

        for (let i = 0; i < intervals.length; i++) {

            for (let j = i + 1; j < intervals.length; j++) {

                if (intervals[i][1] >= intervals[j][0] &&
                    intervals[j][1] >= intervals[i][0]) {

                    intervals[i] = [
                        Math.min(intervals[i][0], intervals[j][0]),
                        Math.max(intervals[i][1], intervals[j][1])
                    ];

                    intervals.splice(j, 1);

                    merged = true;

                    break;
                }
            }

            if (merged) break;
        }
    }

    return intervals;
}
```

---

## Optimal (Sorting + Greedy)

```javascript
function merge(intervals) {

    intervals.sort((a, b) => a[0] - b[0]);

    const result = [];

    result.push(intervals[0]);

    for (let i = 1; i < intervals.length; i++) {

        const last = result[result.length - 1];

        if (intervals[i][0] <= last[1]) {

            last[1] = Math.max(last[1], intervals[i][1]);

        } else {

            result.push(intervals[i]);
        }
    }

    return result;
}
```

---

# ⭐ New Pattern for your notes

Today you've encountered a **new DSA pattern**:

### **Pattern: Sorting + Greedy**

Recognition clues:

* Intervals
* Meetings
* Time ranges
* Merge schedules
* Overlapping ranges
* Need to combine or minimize intervals

---

> **Greedy is NOT an algorithm like Binary Search or Heap.**
>
> It is a **problem-solving strategy (pattern)**.

---

## What is Greedy?

Greedy means:

> **At every step, make the best decision you can right now, hoping it leads to the overall best solution.**

There is **no fixed code template**.

Instead, every Greedy problem has its own implementation.

---

## Examples

### Merge Intervals

Current interval:

```text
[1,6]
```

Next interval:

```text
[4,8]
```

Greedy decision:

> "They overlap. Merge them immediately."

You don't delay the decision.

---

### Jump Game

At every index:

> "What's the farthest I can reach?"

Always take the farthest reachable position.

That's the greedy decision.

---

### Best Time to Buy and Sell Stock II

Whenever:

```text
Today's price < Tomorrow's price
```

Greedy decision:

> Buy today, sell tomorrow.

---

### Assign Cookies

One child needs:

```text
5
```

Cookies:

```text
3,5,7
```

Greedy decision:

> Give the smallest cookie that satisfies the child.

---

## Compare with other patterns

### Binary Search

Has a fixed template:

```javascript
while (left <= right) {
    ...
}
```

---

### Sliding Window

Has a fixed template:

```javascript
expand

shrink

expand

shrink
```

---

### Heap

Has a fixed data structure and operations.

---

### Greedy

❌ No fixed template.

Every problem asks:

> **"What is the best local decision?"**

Then you prove that making that decision every time leads to the global optimum.

---

# How to recognize a Greedy problem?

Ask yourself:

* Can I make the **best decision right now**?
* Do I **never need to revisit** that decision?
* Once I make the decision, can I safely move forward?

If the answer is yes, it's often Greedy.

---

# Merge Intervals

Why is it Greedy?

Suppose you've sorted the intervals.

Current merged interval:

```text
[1,6]
```

Next interval:

```text
[4,8]
```

There is **never a benefit** in waiting.

The best decision is:

```text
Merge now → [1,8]
```

Then move on.

That's why it's called a **Sorting + Greedy** solution.

---

## ⭐ Notes

```
Greedy is not an algorithm.

Greedy is a strategy:

"Make the best local decision at every step."

Unlike Binary Search or Sliding Window, Greedy has no fixed code template.

The implementation depends on the problem.
```

This is an important concept because you'll encounter Greedy in many classic interview questions like Merge Intervals, Jump Game, Gas Station, Task Scheduler, Meeting Rooms, and Interval Scheduling. Once you've solved a few of these, recognizing the Greedy pattern becomes much easier.
