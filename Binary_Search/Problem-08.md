### **Split Array Largest Sum** — LeetCode 410

Given an integer array nums and an integer k, split nums into k non-empty subarrays such that the largest sum of any subarray is minimized.

Return the minimized largest sum of the split.

A subarray is a contiguous part of the array.
```
Example 1:

Input: nums = [7,2,5,10,8], k = 2
Output: 18
Explanation: There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8], where the largest sum among the two subarrays is only 18.
Example 2:

Input: nums = [1,2,3,4,5], k = 2
Output: 9
Explanation: There are four ways to split nums into two subarrays.
The best way is to split it into [1,2,3] and [4,5], where the largest sum among the two subarrays is only 9.
```
Think about:

* Pattern
* Why?
* Brute-force approach
* Optimal approach
* Time complexity
* Space complexity

**Hint:** Same family as Koko and Shipping. What are we searching for?

---

Yes. Your **pattern identification is correct**: this is **Binary Search on Answer**, but the checking function is different from Koko. Your DSA notes also emphasize learning to recognize the pattern/approach rather than just memorizing solutions. 

One correction first:

* Brute force is not really `O(2n²)`.
* A straightforward brute-force solution can be around **O(nᵏ)** if you enumerate all possible `k-1` split positions.
* We can write a simpler recursive brute-force solution for learning.

## 1. The key idea of Binary Search

For:

```text
nums = [7,2,5,10,8]
k = 2
```

We are looking for the **minimum possible largest sum**.

The answer must be somewhere between:

```text
left  = max(nums) = 10
right = sum(nums) = 32
```

So our search space is:

```text
10 ... 32
```

Now pick a candidate capacity, say:

```text
candidate = 20
```

Ask:

> Can I split the array into **at most 2 subarrays**, where every subarray has sum ≤ 20?

Try:

```text
[7,2,5]   → 14
[10,8]    → 18
```

Yes ✅

So `20` **works**.

Since we want the **minimum** possible value, try smaller:

```text
right = 20
```

---

Try `15`:

```text
[7,2,5] → 14
[10]    → 10
[8]     → 8
```

We need **3 subarrays**, but `k = 2`.

So `15` **doesn't work** ❌

Therefore we need a larger answer:

```text
left = 16
```

Eventually:

```text
18 → works
17 → doesn't work
```

Therefore:

```text
answer = 18
```

### ⭐ This is the important pattern

```text
Candidate answer
       ↓
Can I satisfy the problem with this answer?
       ↓
YES → try smaller
NO  → try larger
```

That's exactly the same structure as Koko.

The difference is only the **validation function**.

---

# 2. Validation function

For a given `maxSum`, we greedily create subarrays.

```javascript
function canSplit(nums, k, maxSum) {

    let subarrays = 1;
    let currentSum = 0;

    for (const num of nums) {

        if (currentSum + num > maxSum) {
            subarrays++;
            currentSum = 0;
        }

        currentSum += num;
    }

    return subarrays <= k;
}
```

Example:

```text
nums = [7,2,5,10,8]
maxSum = 18
```

We get:

```text
[7,2,5] → 14
[10,8]  → 18
```

`subarrays = 2`

So:

```text
2 <= k
```

✅ Valid.

---

# 3. Optimal Binary Search

```javascript
function splitArray(nums, k) {

    let left = Math.max(...nums);
    let right = nums.reduce((sum, num) => sum + num, 0);

    while (left < right) {

        const maxSum = Math.floor((left + right) / 2);

        let subarrays = 1;
        let currentSum = 0;

        for (const num of nums) {

            if (currentSum + num > maxSum) {
                subarrays++;
                currentSum = 0;
            }

            currentSum += num;
        }

        if (subarrays <= k) {
            // This maximum sum works.
            // Try to make it smaller.
            right = maxSum;
        } else {
            // Too many subarrays required.
            // Need a larger maximum sum.
            left = maxSum + 1;
        }
    }

    return left;
}
```

### Complexity

```text
Binary Search:
O(n log(sum(nums)))
```

Space:

```text
O(1)
```

---

# 4. Brute Force — Recursive

For learning the brute-force idea, we can try every possible split.

```javascript
function splitArray(nums, k) {

    function solve(start, groups) {

        // Last group gets all remaining elements
        if (groups === 1) {

            let sum = 0;

            for (let i = start; i < nums.length; i++) {
                sum += nums[i];
            }

            return sum;
        }

        let currentSum = 0;
        let best = Infinity;

        // Try every possible split position
        for (let i = start; i <= nums.length - groups; i++) {

            currentSum += nums[i];

            const remaining = solve(i + 1, groups - 1);

            const largestSum = Math.max(
                currentSum,
                remaining
            );

            best = Math.min(best, largestSum);
        }

        return best;
    }

    return solve(0, k);
}
```

This explores different ways of placing the `k - 1` split points, so it becomes expensive very quickly.

---

## ⭐ Compare this with Koko

This is the connection I want you to remember:

### Koko

```text
Answer = eating speed

Check:
Can she finish within H hours?

Works → smaller speed
Fails → larger speed
```

### Split Array

```text
Answer = maximum allowed subarray sum

Check:
Can we split into ≤ K subarrays?

Works → smaller maximum sum
Fails → larger maximum sum
```

So the **Binary Search template is almost identical**.

Only this part changes:

```text
        ↓
   VALIDATE(candidate)
        ↓
```

That's the real skill behind **Binary Search on Answer**.

