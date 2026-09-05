### Q2 — Variation Of Longest Subarray With Sum K

**Problem: Count Subarrays With Sum Divisible by K**

Given:

```text
nums = [4, 5, 0, -2, -3, 1]
k = 5
```

Find the number of **contiguous subarrays whose sum is divisible by `k`**.

Again, don't jump directly to code. Explain:

1. What would you try first?
2. What makes this different from the previous subarray-sum problem?
3. What information would you need to remember while traversing the array?
4. Complexity.

**No pattern/solution hint from me this time.** You identify it first.

### My Thoughts-
So for question number two, the count subarray with sum divisible by K. So approach will be the similar, that we will be using the prefix sum plus hashmap because the problem statement and problem structure and solution structure will be almost same. Just the logic will be changed where we check. For the previous example, like we need, we will check that for current prefix sum minus K is exist in the hashmap or not. That what we do. That logic only will be changed and we will replace that logic, but the rest of the functionality will be same. And yeah, and what will be the logic according to me is that we will find, we will use the modulo operator and we will divide the prefix sum with five, and if this prefix sum is greater than five, then only this logic will be applied. So first will be that if the prefix sum is divided by five totally, then we will increase the count. Or second, if the prefix sum is more than the K, then we will find the remainder, and then we will search for the remainder in the negative value because let's say for 13 that the remainder will be 3, so we will search for minus 3 because 13 minus 3 will be 10. So it will be our check for S, and we will increase the count. Time complexity will be same, O of N, and space complexity will be same, O of N. And also share the code as well for this optimized solution for this problem for my notes.

Your **core idea is correct**: this is still prefix sum + HashMap, but the condition changes from an exact difference to a **remainder match**.

There are two important corrections to your reasoning.

### 1. We don't need `prefixSum > K`

We care about whether:

> **two prefix sums have the same remainder when divided by `K`**

Because if:

`prefixSum1 % K === prefixSum2 % K`

then their difference is divisible by `K`.

For example:

```text
prefixSum1 = 3
prefixSum2 = 13

3 % 5  = 3
13 % 5 = 3
```

Therefore:

```text
13 - 3 = 10
10 % 5 = 0
```

So the subarray between those two prefix sums has a sum divisible by 5.

### 2. We don't search for the negative remainder

Your `-3` idea is the part to correct.

We simply store and search for the **same remainder**.

So:

```text
currentPrefixSum = 13
remainder = 13 % 5 = 3
```

We ask:

> Have we seen remainder `3` before?

If yes, every previous occurrence of remainder `3` gives us one subarray whose sum is divisible by 5.

There is one JavaScript-specific detail: `%` can produce a negative remainder. So we normalize it:

```js
const remainder = ((prefixSum % k) + k) % k;
```

For example:

```text
-2 % 5 = -2

((-2 % 5) + 5) % 5
= 3
```

So `-2` and `3` are treated as the same modulo class.

---

## Optimized solution

```js
function subarraysDivByK(nums, k) {
    const remainderMap = new Map();

    // Prefix sum 0 has remainder 0.
    // This handles subarrays starting from index 0.
    remainderMap.set(0, 1);

    let prefixSum = 0;
    let count = 0;

    for (const num of nums) {
        prefixSum += num;

        // Normalize negative remainders
        const remainder = ((prefixSum % k) + k) % k;

        // If we've seen this remainder before,
        // each occurrence gives one valid subarray.
        if (remainderMap.has(remainder)) {
            count += remainderMap.get(remainder);
        }

        // Store/increment frequency of this remainder
        remainderMap.set(
            remainder,
            (remainderMap.get(remainder) || 0) + 1
        );
    }

    return count;
}
```

For:

```text
nums = [4, 5, 0, -2, -3, 1]
k = 5
```

the result is:

```text
7
```

### The key difference from our previous problem

| Problem                  | HashMap stores               | Lookup           |
| ------------------------ | ---------------------------- | ---------------- |
| Subarray Sum = K         | `prefixSum → frequency`      | `currentSum - K` |
| Sum Divisible by K       | `remainder → frequency`      | same remainder   |
| Longest Subarray Sum = K | `prefixSum → earliest index` | `currentSum - K` |

That's a very useful family of variations to remember.

**Q2 8.5/10.** You identified the right underlying technique immediately; the main thing to fix is the modulo condition and the unnecessary negative-remainder lookup.

