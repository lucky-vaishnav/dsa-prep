## Problem: Longest Repeating Character Replacement

You are given a string `s` and an integer `k`.

You can replace **at most `k` characters**.

Return the length of the **longest substring** that can be made of the **same character** after at most `k` replacements.

### Example

```
Input:
s = "AABABBA"
k = 1

Output:
4
```

Explanation:

Replace one `'A'` with `'B'`:

```
AABBBBA
```

Longest repeating substring length = **4**

---

### Tell me:

```
Pattern:
Why:
Window Type:
Brute Force Complexity:
Optimal Data Structure:
Optimal Approach:
Expand When:
Shrink When:
Time Complexity:
Space Complexity:
```

💡 **Hints:**

- This is **not** a fixed-size window.
- Think about **Variable Sliding Window**.
- You'll need to know the **most frequent character** in the current window.

### My Answer -

So for question number two, pattern we can use is sliding window, dynamic sliding window and map to store the traversed value and count of that. And window type will be dynamic, brute force will be O of n square, optimal data structure will be a map. And we will expand till k is zero, like whenever the k reaches to the limit, till then we will expand. And once we replace the value, then we will shrink the window. Time complexity will be O of n, and space complexity will be O of n. And also share the code for it without the explanation.

## Review

Good! I'd give this **8.5/10**.

You identified the **main pattern correctly**, but there's one key condition that makes this problem different from normal variable sliding window problems.

---

## Pattern

```
Variable Sliding Window + HashMap
```

✅ Correct.

---

## Why

You wrote:

> use sliding window and map to store count
> 

✅ Correct.

The HashMap stores the **frequency of each character** in the current window.

---

## Window Type

```
Variable
```

✅ Correct.

---

## Brute Force

```
O(n²)
```

✅ Correct.

---

## Optimal Data Structure

```
HashMap
```

✅ Correct.

---

## Expand Condition

You wrote:

> Expand till k is zero.
> 

🟡 This is the only important correction.

We **do not decrease `k`** in this algorithm.

Instead, we maintain:

```
maxFreq = frequency of the most common character in the current window
```

Then we check:

```
windowLength - maxFreq <= k
```

If this is true:

✅ Expand.

---

## Shrink Condition

Instead of:

> once we replace the value, shrink
> 

The actual condition is:

```
windowLength - maxFreq > k
```

Then:

- Remove the left character.
- Move `left++`.

---

## Time Complexity

```
O(n)
```

✅ Correct.

---

## Space Complexity

```
O(n)
```

More precisely:

```
O(26)
```

for uppercase English letters, which is effectively **O(1)**.

If characters are unrestricted (general strings), then **O(n)** is acceptable.

---

# Final Notes

```
Pattern:
Variable Sliding Window + HashMap

Why:
Need the longest valid contiguous substring while tracking character frequencies.

Window Type:
Variable

Brute Force:
O(n²)

Optimal Data Structure:
HashMap

Optimal Approach:
Maintain character frequencies and the maximum frequency in the current window.
Expand while:
windowLength - maxFreq <= k
Shrink when:
windowLength - maxFreq > k

Time Complexity:
O(n)

Space Complexity:
O(1) (English uppercase) / O(n) (general case)
```

---

# Code

```jsx
function characterReplacement(s, k) {
  const map = newMap();
  let left = 0;
  let maxFreq = 0;
  let maxLength = 0;

  for (let right = 0; right < s.length; right++) {
    map.set(s[right], (map.get(s[right]) || 0) + 1);

    maxFreq = Math.max(maxFreq, map.get(s[right]));

    while (right - left + 1 - maxFreq > k) {
      map.set(s[left], map.get(s[left]) - 1);
      left++;
    }
    maxLength = Math.max(maxLength, right - left + 1);
  }
  return maxLength;
}

console.log(characterReplacement("AABABBA", 1));
```

---

## ⭐ One thing to remember

This problem has a **unique sliding window condition** that you'll see in several interview problems:

Instead of checking the sum, distinct count, or window size, we check:

```
windowLength - maxFrequency
```

Think of it as:

> **"How many characters do I need to replace to make the entire window consist of the same character?"**
> 

If that number is more than `k`, the window is no longer valid, so we shrink it.

Other than that one condition, your pattern recognition was correct. You're getting much better at identifying sliding window problems.
