### Q — A different version of problem-07

Given:

```text
nums = [1, 2, 1, 3, 2, 3, 4]
```

Find the **length of the longest contiguous subarray containing exactly 3 distinct values**.

Give me:

1. Approach
2. Data structure
3. When to shrink
4. When to update the answer
5. Time and space complexity

---
### My answer was according to Problem-07

1. Approach = hashMap+ sliding window
2.  Data structure - hasmap
3.  When to shrink  - when freq hashmap size is grater than 3
4.  When to update the answer - after shrinking including freq hashmap size is grater than 3
5.  Time and space complexity- 0(n), 0(3)

---
Q is mostly correct — **8.5/10**.

The important correction is point **4**.

### Q correction

You said:

> update the answer after shrinking including freq hashmap size is greater than 3

It should be:

> **Shrink while `freq.size > 3`, then update the answer once the window is valid (`freq.size === 3`).**

You don't need to explicitly check `=== 3` after shrinking because once the `while` loop finishes, the window has **at most 3 distinct values**. Since we're looking for **exactly 3**, we should check:

```js
if (freq.size === 3) {
    maxLength = Math.max(maxLength, right - left + 1);
}
```

Also, your space complexity `O(3)` is technically correct for this specific problem because the map holds at most 3 distinct values, but in an interview I'd say **O(1)**. `O(3)` is still constant space.

### Correct structure

```js
for (let right = 0; right < nums.length; right++) {
    // add nums[right]

    while (freq.size > 3) {
        // remove nums[left]
        left++;
    }

    if (freq.size === 3) {
        // update max length
    }
}
```

So the key distinction is:

* **At most 3 distinct:** update whenever `freq.size <= 3`
* **Exactly 3 distinct:** update only when `freq.size === 3`
