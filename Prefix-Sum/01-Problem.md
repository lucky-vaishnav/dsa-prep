### 🟢 Q- count of Subarrays - Sum Equals K

Let's test whether the **Prefix Sum + HashMap** idea has actually stuck.

```text
nums = [1, 2, 1, 2]
k = 3

Output = 3
```

Before coding, tell me:

* Pattern?
* Why doesn't normal sliding window work reliably?
* What will the HashMap store?
* What is the key calculation we look for?
* Time & space complexity?

---
Absolutely. Here is the **Prefix Sum + HashMap** solution for **Subarray Sum Equals K**.

### Optimal — O(n) Time, O(n) Space

```javascript
function subarraySum(nums, k) {
    const prefixMap = new Map();

    // Prefix sum 0 exists once
    prefixMap.set(0, 1);

    let prefixSum = 0;
    let count = 0;

    for (const num of nums) {
        prefixSum += num;

        // We need a previous prefixSum:
        // previousSum = prefixSum - k
        if (prefixMap.has(prefixSum - k)) {
            count += prefixMap.get(prefixSum - k);
        }

        // Store/update frequency of current prefixSum
        prefixMap.set(
            prefixSum,
            (prefixMap.get(prefixSum) || 0) + 1
        );
    }

    return count;
}
```

### Example

```javascript
subarraySum([1, 1, 1], 2);
```

Returns:

```text
2
```

Because:

```text
[1, 1]   → 2
[1, 1]   → 2
```

### Core idea for your notes

```text
prefixSum - previousPrefixSum = k

Therefore:

previousPrefixSum = prefixSum - k
```

So at every element:

```text
1. Update prefixSum
2. Check prefixSum - k in HashMap
3. Add its frequency to count
4. Store current prefixSum
```

### Why `Map` stores frequency, not just existence

For example:

```text
nums = [1, 2, 1]
k = 3
```

A prefix sum can occur multiple times. Each previous occurrence can represent a different subarray ending at the current position, so we need its **count**.

**Pattern:** `Prefix Sum + HashMap`
**Time:** `O(n)`
**Space:** `O(n)`

Yes — your understanding of **Subarray Sum Equals K** is correct.

### Review

Key points:

* **Sliding window doesn't work reliably** because negative numbers destroy the monotonic behavior of the sum. Removing/shrinking from the left can make the sum **increase**, so we can't safely decide which direction to move.
* **Prefix sum** = the cumulative sum from the beginning up to the current index.
* The HashMap stores:
  **`prefixSum → frequency/count`**
* The same prefix sum can occur multiple times, which is exactly why we store a **count**, not just whether it exists.
* Complexity:

  * Time: **O(n)**
  * Space: **O(n)**

One important piece to make your explanation interview-ready:

If the current prefix sum is `S`, we want a previous prefix sum of:

**`S - k`**

because:

`S - previousPrefix = k`

So whenever `prefixMap` contains `S - k`, its frequency tells us **how many subarrays ending at the current index have sum k**.

For example, with `[1,2,3,-2,2]`, `k = 3`, the answer is **4**.

---
## Why check the required prefix sum before updating the map?

Suppose the current prefix sum is `prefixSum`. We need to find how many previous prefix sums equal:

requiredPrefix=prefixSum−k\text{requiredPrefix}=\text{prefixSum}-krequiredPrefix=prefixSum−k

Because if

prefixSum−previousPrefix=k\text{prefixSum}-\text{previousPrefix}=kprefixSum−previousPrefix=k

then the subarray between those two prefix positions has sum `k`.

### Example: `nums = [3]`, `k = 3`

Initially:

JavaScript

```
prefixMap = new Map([[0, 1]]);
prefixSum = 0;
count = 0;
```

We process the element `3`.

Step 1: Update the prefix sum

JavaScript

```
prefixSum = 3;
```

Step 2: Check the required prefix sum

JavaScript

```
requiredPrefix = prefixSum - k; // 3 - 3 = 0
count += prefixMap.get(0) || 0; // count = 1
```

The initial prefix sum `0` represents the position before the array begins. It allows us to count `[3]` as a valid subarray.

Step 3: Update the map

JavaScript

```
prefixMap.set(3, (prefixMap.get(3) || 0) + 1);
```

The answer is `1`.

### What if we update the map first?

Consider the same example, but imagine we update the map with the current prefix sum before checking.

For this particular input, the answer happens to remain correct because the current prefix sum is `3`, while the required prefix sum is `0`.

But consider `nums = [0]`, `k = 0`.

* Initially, the map contains `0 → 1`.

* The current prefix sum is `0`.

* If we update the map first, its frequency becomes `0 → 2`.

* Then we look up the required prefix sum, which is also `0`.

* We add `2` to the count, incorrectly counting two subarrays instead of one.

Why? One occurrence of prefix sum `0` represents the position before the array, and the other represents the position after the current element. Using the current occurrence to count a subarray would effectively count an empty subarray, which is invalid.

## The rule to remember

First query the map using `prefixSum - k`; then record the current prefix sum.

JavaScript

```
prefixSum += nums[i];

count += prefixMap.get(prefixSum - k) || 0;

prefixMap.set(
  prefixSum,
  (prefixMap.get(prefixSum) || 0) + 1
);
```

The order ensures that you count only subarrays ending at the current index that begin at an earlier prefix position—not an empty subarray formed by the current prefix itself.

Interview takeaway: Query first, update second. This is especially important when `k = 0` or when the current prefix sum equals the required prefix sum.


