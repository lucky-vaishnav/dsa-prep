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
