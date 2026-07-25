**Use When:**

- Frequency/count is important.
- Maximum possible frequency is known (often `n`).
- Need Top K frequent elements.

**Key Idea:**

```
Index = Frequency

bucket[1] -> Elements appearing once
bucket[2] -> Elements appearing twice
bucket[3] -> Elements appearing three times
...
bucket[n]
```

Instead of sorting by frequency, place elements directly into buckets and traverse the buckets from the highest frequency to the lowest.

We'll cover **Bucket Sort** properly as its own pattern later, just like we did for Monotonic Stack and Sliding Window. For now, remember it as the optimal approach for **Top K Frequent Elements**.

One more thing before we formally learn **Bucket Sort** later.

Your thought process was actually very close to Bucket Sort:

> "Create an array of size `n` and place elements according to their count."
> 

That is exactly the core idea. The only correction is:

- ❌ Not a `Set`
- ✅ An **array of arrays (buckets)**

Think of it like this:

```
Frequency Map

1 -> 3
2 -> 2
3 -> 1
```

Create buckets:

```
bucket= [
    [],// frequency 0
    [3],// frequency 1
    [2],// frequency 2
    [1],// frequency 3
    [],
    [],
    []
]
```

Then simply traverse from the back.

Practice Problem -

### Problem: Top K Frequent Elements

Given an integer array `nums` and an integer `k`, return the **k most frequent elements**.

#### Example 1

```
Input:
nums = [1,1,1,2,2,3]
k = 2

Output:
[1,2]
```

#### Example 2

```
Input:
nums = [1]
k = 1

Output:
[1]
```

---

#### HashMap + Bucket Sort (Optimal) ⭐

```jsx
function topKFrequent(nums, k) {
  const map = new Map();

  for (const num of nums) {
    map.set(num, (map.get(num) || 0) + 1);
  }

  // bucket[index] = numbers having frequency = index
  const bucket = Array(nums.length + 1)
    .fill(null)
    .map(() => []);

  for (const [num, freq] of map) {
    bucket[freq].push(num);
  }

  const result = [];

  for (let freq = bucket.length - 1; freq >= 0 && result.length < k; freq--) {
    for (const num of bucket[freq]) {
      result.push(num);

      if (result.length === k) {
        return result;
      }
    }
  }

  return result;
}
```
