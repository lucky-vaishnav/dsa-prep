### 🟢 Q- Subarray Sum Equals K

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
