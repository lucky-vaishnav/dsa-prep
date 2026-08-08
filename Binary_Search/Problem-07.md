## Problem: Capacity To Ship Packages Within D Days (LeetCode 1011)

```text
weights = [1,2,3,4,5,6,7,8,9,10]
days = 5

Output:
15
```

### Hint

You're **not searching for an element**.

You're searching for the **minimum ship capacity** that satisfies the condition.

Think about:

* Pattern
* Why
* Brute Force Complexity
* Optimal Data Structure
* Optimal Approach
* Time Complexity
* Space Complexity

---

### ⭐ Small Hint

These two problems belong to the **same Binary Search pattern**.

Today's new pattern is:

```text
Binary Search on Answer
```

This is one of the most important Binary Search interview patterns. Once you master these two problems, you'll be able to solve many similar questions like:

* Split Array Largest Sum
* Minimum Speed to Arrive on Time
* Allocate Books
* Painter's Partition Problem
---
# My Thought -
So this problem, second problem, capacity to ship packages within D days, it is the similar, it is the similar problem as we done the cocoa eating banana. So all the time complexity and all the things will be the same. I think there is not that much difference in the approach as well. So yeah, share your validation.

---
Yes — **your understanding is correct.** These are essentially the **same Binary Search on Answer pattern**.

### Validation

|                | Koko Eating Bananas               | Ship Packages                |
| -------------- | --------------------------------- | ---------------------------- |
| Pattern        | Binary Search on Answer           | Binary Search on Answer      |
| Search space   | `1 → max(pile)`                   | `max(weight) → sum(weights)` |
| Check function | Can Koko finish within `h` hours? | Can we ship within `days`?   |
| Goal           | Minimum valid speed               | Minimum valid capacity       |
| Time           | `O(n log M)`                      | `O(n log M)`                 |
| Space          | `O(1)`                            | `O(1)`                       |

The **main difference is only the validation/check function**:

* Koko → calculate required hours for a given speed.
* Shipping → calculate required days for a given capacity.

So yes, **learn the pattern from Koko, then recognize the same pattern here.**

## Capacity To Ship Packages Within D Days

```javascript
function shipWithinDays(weights, days) {

    let left = Math.max(...weights);
    let right = weights.reduce((sum, weight) => sum + weight, 0);

    while (left < right) {

        const capacity = Math.floor((left + right) / 2);

        let requiredDays = 1;
        let currentLoad = 0;

        for (const weight of weights) {

            if (currentLoad + weight > capacity) {
                requiredDays++;
                currentLoad = 0;
            }

            currentLoad += weight;
        }

        if (requiredDays <= days) {
            // Capacity works → try smaller
            right = capacity;
        } else {
            // Capacity doesn't work → need larger
            left = capacity + 1;
        }
    }

    return left;
}
```

### ⭐ Notes

**Search space:**

```text
min capacity = max(weights)
max capacity = sum(weights)
```

Why?

* Capacity cannot be less than the **heaviest package**.
* Capacity equal to the **total weight** can ship everything in one day.

**Validation function:**

```text
Given capacity
      ↓
Calculate required days
      ↓
days <= allowed days?
      ↓
YES → decrease capacity
NO  → increase capacity
```

**Complexity:**

```text
Time  = O(n log(sum(weights)))
Space = O(1)
```

### Pattern to remember

```text
Binary Search on Answer

Koko:
speed → required hours

Shipping:
capacity → required days

Same Binary Search.
Different validation function.
```

This is the key thing to remember—not the exact code.


Let's see your approach first, then we'll discuss and compare the solutions.

