### Q - New Variation

Given a binary array:

```text
nums = [0, 1, 0, 0, 1, 1, 0, 1]
```

Find the **length of the longest contiguous subarray containing an equal number of `0`s and `1`s**.

For example, `[0, 1]` has one `0` and one `1`, so its length is `2`.

Explain:

1. Your approach.
2. What information you would maintain while traversing.
3. How you would determine whether a subarray has equal `0`s and `1`s.
4. Time and space complexity.

Again, **identify the pattern yourself**.

### My Thoughts-
So for approach-wise or pattern-wise, so it will be not a pattern, but we can just traverse this nums input array and use a map to store the frequency of zeros and ones. So we will use two for loops. First for loop will be traversing all the way to the complete array, and if whenever the zeros count and ones count is equal, we will just calculate the max continuous subarray length using Math.max. And after this traversing complete, we will use one more for loop. So if the nums length we reached the input array is equal to the max length, then which means that the complete array length is the answer for this problem. Else we will be traversing through the map and use the right pointer as nums.length, which will be fixed, and left pointer we will be moving until zero and ones count is not equal, and we will be keep decreasing according to the left pointer value, frequency decreasing from the map, and we will be keep calculating the max length again using the Math.max. So yeah, so it will be not a proper pattern, but yeah, approach-wise we can solve it using two for loops. Time complexity will be O of n, because O of n plus O of n, max for worst cases. And space complexity will be O of maybe you can say 2, because we just storing map for two values, zeros and ones, but it will be O of 1 then, I think. Yeah, share the answer and share the code as well for this problem.

Your complexity assessment at the end is correct, but the **approach itself is more complicated than necessary**. I'd give this **6.5/10**.

The important part is that this problem has a much cleaner way to think about it.

### The key transformation

Because the array contains only `0` and `1`, we can treat:

```text
0 → -1
1 → +1
```

Then the problem becomes:

> Find the longest contiguous subarray whose transformed sum is `0`.

For example:

```text
[0, 1, 0, 0, 1, 1]
```

becomes:

```text
[-1, +1, -1, -1, +1, +1]
```

Now whenever the **same prefix sum occurs twice**, the elements between those two positions have sum `0`.

That's the key observation.

### Why?

Suppose:

```text
prefixSum at i = 2
prefixSum at j = 2
```

Then:

```text
sum between i and j = 2 - 2 = 0
```

And because `0` represents `-1` and `1` represents `+1`, a sum of `0` means:

> equal number of 0s and 1s.

### What should the HashMap store?

Not frequencies.

Store:

```text
prefixSum → earliest index
```

We specifically want the **earliest occurrence**, because that gives us the longest possible subarray.

Initialize:

```js
map.set(0, -1);
```

This handles a valid subarray that starts at index `0`.

### Code

```js
function findMaxLength(nums) {
    const map = new Map();

    // Prefix sum 0 exists before the array starts
    map.set(0, -1);

    let prefixSum = 0;
    let maxLength = 0;

    for (let i = 0; i < nums.length; i++) {
        // Convert 0 → -1, 1 → +1
        prefixSum += nums[i] === 0 ? -1 : 1;

        if (map.has(prefixSum)) {
            // Same prefix sum means subarray sum is 0
            const length = i - map.get(prefixSum);
            maxLength = Math.max(maxLength, length);
        } else {
            // Store only the first/earliest occurrence
            map.set(prefixSum, i);
        }
    }

    return maxLength;
}
```

For:

```text
[0, 1, 0, 0, 1, 1, 0, 1]
```

the answer is **8**, because the entire array contains four `0`s and four `1`s.

### Complexity

Your final complexity conclusion was right:

* **Time:** O(n)
* **Space:** O(n)

Even though the array contains only `0` and `1`, the **prefix sum can take O(n) different values**, so the HashMap is potentially O(n), not O(1).

### The pattern connection

This is actually a useful extension of something you've already practiced:

**Subarray Sum Equals K**

```text
prefixSum → earliest/frequency information
```

Here we transform the problem so that:

```text
equal 0s and 1s
        ↓
sum = 0
        ↓
same prefix sum
```

So you were right that the problem can be solved by traversal, but the **second traversal isn't necessary**. The prefix-sum observation lets us solve the whole problem in a single pass.
