Given an array:

```
nums = [1,2,1,3,5,6,4]
```

A **peak element** is an element that is **greater than its neighbors**.

Return **the index of any peak element**.

**"any peak values can be if element greater nearby element?”**

Example:

```
Input:
[1,2,3,1]

Output:
2
```

because:

```
3 > 2
3 > 1
```

---

Tell me:

```
Pattern:
Why:
Brute Force Complexity:
Optimal Approach:
Time Complexity:
Space Complexity:
```

### Hint

Ask yourself:

> The array isn't completely sorted, but can I eliminate half of the search space?
> 

---

# Review

### Pattern

You wrote:

```
Sliding Window
or
Binary Search
or
Brute Force
```

### Sliding Window ❌

Not really.

Why?

Sliding Window is used when we need something about a **window**:

- sum
- maximum
- minimum
- longest
- shortest

Here we're just checking **one element**.

So Sliding Window doesn't fit.

---

### Brute Force ✅

Absolutely.

```
foreach element
compare left neighbor
compare right neighbor

ifgreater than both
returnindex
```

Time:

```
O(n)
```

---

### Binary Search ✅ (Optimal)

Correct.

This is one of those rare problems where the array **isn't sorted**, but Binary Search still works.

---

# Why Binary Search Works

This is the important interview insight.

Suppose

```
1 2 3 1
      ^
     mid
```

If

```
nums[mid] > nums[mid+1]
```

then

```
a peak definitely exists
on the LEFT side
(including mid)
```

---

Suppose

```
1 2 3 4 5
      ^
     mid
```

Since

```
3 < 4
```

the array is increasing.

A peak must exist on the **right**.

So move

```
left = mid + 1
```

---

Notice something.

We're not searching for an exact value.

We're searching using the **slope**.

That's why Binary Search works.

---

# Why

You wrote

> contiguous element matters
> 

🟡 Close.

A stronger interview answer would be:

```
Need to compare only neighboring elements.
Using the increasing/decreasing slope, we can eliminate half of the search space.
```

---

# Brute Force

You wrote

```
O(n)
```

✅ Correct.

Unlike most problems, brute force here is **linear**, not `O(n²)`.

---

# Optimal

You wrote

```
Binary Search
```

✅ Correct.

---

# Complexity

```
Time : O(log n)

Space: O(1)
```

✅ Correct.

---

# Optimal Code

```jsx
function findPeakElement(nums) {
  let left = 0;
  let right = nums.length - 1;

  while (left < right) {
    const mid = Math.floor((left + right) / 2);

    if (nums[mid] > nums[mid + 1]) {
      right = mid;
    } else {
      left = mid + 1;
    }
  }

  return left;
}
```

---

#
