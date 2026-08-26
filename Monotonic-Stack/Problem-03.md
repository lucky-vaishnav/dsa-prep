### 🔵 Q — : Daily Temperatures

```text
temperatures = [73,74,75,71,69,72,76,73]

Output = [1,1,4,2,1,1,0,0]
```

For each day, find how many days you have to wait until a **warmer temperature**.

Think about:

* Brute-force approach
* Which pattern might help?
* What information do we need to remember while traversing?
* Why might a normal stack not be enough?
* Time & space complexity?

**Don't worry if Q2 is unfamiliar.** If you recognize a new pattern, I'll tell you before we formally consider it part of your learned Phase 1 patterns.

---
### My Thought-
the brute force approach will be checking each element with the next element until we found a larger temperature and calculate the difference between the... if we found a larger temperature, then yeah, calculate the difference between indices, and we can set that how many days it is required for the next temperature, higher temperature. So the brute force approach will be O of n square, with, I think, stack, or the decreasing maintained stack will be the better approach here, by which we can keep the decreasing stack, and whenever a higher value comes, which is higher than the top stack element, then we will keep removing the stack element and calculating the number of days by using those indices in the stack and current index of times. Time complexity will be O of n, space complexity will be roughly O of n. And yeah, also share the code as well after you review.

---
Yes — your understanding is **very strong: 9.5/10**. You correctly recognized the **Monotonic Stack** pattern, specifically a **monotonically decreasing stack of indices**.

### Review

* **Brute force:** `O(n²)` ✅
* **Pattern:** Monotonic Decreasing Stack ✅
* **Store indices, not temperatures:** ✅
* When current temperature > temperature at stack top → resolve the waiting day for that index and pop it. ✅
* **Time:** `O(n)` ✅
* **Space:** `O(n)` worst case ✅

The important reason it's `O(n)` is that **each index is pushed once and popped at most once**.

### Code

```javascript
function dailyTemperatures(temperatures) {
    const result = new Array(temperatures.length).fill(0);
    const stack = []; // stores indices

    for (let i = 0; i < temperatures.length; i++) {

        while (
            stack.length > 0 &&
            temperatures[i] > temperatures[stack[stack.length - 1]]
        ) {
            const previousIndex = stack.pop();

            result[previousIndex] = i - previousIndex;
        }

        stack.push(i);
    }

    return result;
}
```

For:

```text
[73,74,75,71,69,72,76,73]
```

we get:

```text
[1,1,4,2,1,1,0,0]
```

### ⭐ Key note for your Phase 1

This is actually a **very important Monotonic Stack problem**, and you recognized it correctly without needing the solution.

Your mental trigger should now be:

> **"For every element, find the next greater/smaller element to the left/right" → think Monotonic Stack.**
