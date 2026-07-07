## Problem: Next Greater Element I

Given:

```
nums1 = [4,1,2]
nums2 = [1,3,4,2]
```

For every element in `nums1`, find its **next greater element** in `nums2`.

If none exists, return `-1`.

Example:

```
nums1 = [2,4]

nums2 = [1,2,3,4]

Output:

[3,-1]
```

Because

```
2 → next greater is 3

4 → no greater element
```

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

### 💡 Hint

This is **the parent problem** of **Daily Temperatures**.

Ask yourself:

```
"Am I looking for the next greater element?"
```

# Optimal Approach

> loop through nums2 and maintain stack
> 

✅ Correct idea.

1. Traverse **nums2**.
2. Build a **HashMap**:

```
element -> next greater element
```

Example:

```
1 -> 3

3 -> 4

4 -> -1

2 -> -1
```

Then simply loop through `nums1`.

```
nums1 = [4,1,2]
```

Answer becomes

```
map[4]
map[1]
map[2]
```

Very fast.

---

# Complexity

You wrote

```
Time:
O(n)

Space:
O(n)
```

✅ Correct.

More precisely:

```
Time:
O(nums1 + nums2)

Space:
O(nums2)
```

---

# ⭐ Optimal Code

```jsx
function nextGreaterElement(nums1, nums2) {
  const stack = [];
  const map = newMap();

  for (const num of nums2) {
    while (stack.length && num > stack[stack.length - 1]) {
      map.set(stack.pop(), num);
    }

    stack.push(num);
  }

  while (stack.length) {
    map.set(stack.pop(), -1);
  }

  const result = [];

  for (const num of nums1) {
    result.push(map.get(num));
  }

  return result;
}

console.log(nextGreaterElement([4, 1, 2], [1, 3, 4, 2]));
// [-1,3,-1]
```

---

# 💡 Why do we need a HashMap?

Imagine:

```
nums1 = [4,1,2]
nums2 = [1,3,4,2]
```

After processing `nums2`, the map looks like:

```
1 → 3
3 → 4
4 → -1
2 → -1
```

Now answering `nums1` is easy:

```
4 → -1
1 → 3
2 → -1
```

No need to search `nums2` again.
