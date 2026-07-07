## Problem: Product of Array Except Self

Given an integer array:

```
nums = [1,2,3,4]
```

Return:

```
[24,12,8,6]
```

Explanation:

```
24 = 2×3×4
12 = 1×3×4
8  = 1×2×4
6  = 1×2×3
```

**Constraints:**

- Do **not** use division.
- Solve in **O(n)** time.

---

### Tell me:

```
Pattern:
Why:
Brute Force Complexity:
Optimal Data Structure:
Optimal Approach:
Time Complexity:
Space Complexity:
```

## Code (Optimal O(n))

```jsx
function productExceptSelf(nums) {
  const n = nums.length;
  const result = newArray(n).fill(1);

  // Prefix products
  let prefix = 1;
  for (let i = 0; i < n; i++) {
    result[i] = prefix;
    prefix *= nums[i];
  }

  // Suffix products
  let suffix = 1;
  for (let i = n - 1; i >= 0; i--) {
    result[i] *= suffix;
    suffix *= nums[i];
  }

  return result;
}

console.log(productExceptSelf([1, 2, 3, 4])); // [24,12,8,6]
```

---

## Another Approach (Using Two Extra Arrays)

This is easier to understand but uses more space.

```jsx
function productExceptSelf(nums) {
  const n = nums.length;
  const prefix = newArray(n).fill(1);
  const suffix = newArray(n).fill(1);
  const result = newArray(n);

  for (let i = 1; i < n; i++) {
    prefix[i] = prefix[i - 1] * nums[i - 1];
  }

  for (let i = n - 2; i >= 0; i--) {
    suffix[i] = suffix[i + 1] * nums[i + 1];
  }

  for (let i = 0; i < n; i++) {
    result[i] = prefix[i] * suffix[i];
  }

  return result;
}
```

---

## Interview Preference ⭐

| Approach | Time | Space | Preferred? |
| --- | --- | --- | --- |
| Brute Force | O(n²) | O(1) | ❌ |
| Prefix Array + Suffix Array | O(n) | O(n) | ✅ Easy to explain |
| Prefix Variable + Suffix Variable (above) | O(n) | O(1) extra* | ⭐ Best |
- Ignoring the required output array, as is standard in interview discussions.
