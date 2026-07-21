## Problem: Minimum Window Substring

Given two strings `s` and `t`, return the **smallest substring** of `s` that contains **all the characters of `t`** (including duplicates).

If there is no such substring, return an empty string.

### Example 1

```
Input:
s = "ADOBECODEBANC"
t = "ABC"

Output:
"BANC"
```

---

### Example 2 (Duplicates)

```
s = "AAABBC"
t = "AABC"
```

Need:

```
A = 2
B = 1
C = 1
```

Notice:

We need **2 As**, not just one.

Answer:

```
"AABBC"
```

Not:

```
"ABC"
```

because:

```
ABC

A = 1 ❌
```

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

- This is one of the **hardest Variable Sliding Window** problems.
- You need **two HashMaps** (or arrays for character counts).
- Unlike previous sliding window problems, the window is valid only when **all required characters and their frequencies are present**.

---

### Review

---

### Pattern

You said:

> Sliding Window + HashMap
> 

✅ Correct.

---

### Why

You said:

> Store the counts of characters from string `t`.
> 

✅ Exactly.

This is the key difference from other sliding window problems.

---

### Brute Force

```
O(n²)
```

✅ Correct.

---

### Optimal Data Structure

```
HashMap
```

✅ Correct.

Actually, we use **two HashMaps**:

- One for `t` (required counts)
- One for the current window

---

### Optimal Approach

You said:

> Expand the window.
> 
> 
> If all characters and their counts match, shrink the window.
> 
> While shrinking, keep updating the minimum length.
> 

✅ Excellent.

That is exactly how the algorithm works.

One small addition:

While shrinking, if removing one character makes the window invalid again, stop shrinking and continue expanding.

---

### Time Complexity

```
O(n)
```

✅ Correct.

---

## Space Complexity

You wrote:

```
O(n)
```

✅ Acceptable.

More precisely:

```
O(m)
```

where `m` is the number of unique characters in `t`.

For English letters, interviewers usually treat it as **O(1)**.

---

### Final Notes

```
Pattern:
Variable Sliding Window + HashMap

Why:
Need the smallest valid window containing all characters (including duplicate counts).

Window Type:
Variable

Brute Force:
O(n²)

Optimal Data Structure:
Two HashMaps

Optimal Approach:
Expand the window and maintain character counts.
When all required characters and counts match:
- Update the minimum window.
- Shrink from the left until the window becomes invalid.

Expand When:
Window is not valid.

Shrink When:
Window is valid (contains all required characters with correct frequencies).

Time Complexity:
O(n)

Space Complexity:
O(m) / O(1) for fixed character set
```

---

### Code (No Explanation)

```jsx
function minWindow(s, t) {

    if (t.length > s.length) return "";

    const need = new Map();
    const window = new Map();

    for (const ch of t) {
        need.set(ch, (need.get(ch) || 0) + 1);
    }

    let have = 0;
    const needCount = need.size;

    let left = 0;
    let minLength = Infinity;
    let start = 0;

    for (let right = 0; right < s.length; right++) {

        const ch = s[right];
        window.set(ch, (window.get(ch) || 0) + 1);

        if (
            need.has(ch) &&
            window.get(ch) === need.get(ch)
        ) {
            have++;
        }

        while (have === needCount) {

            if (right - left + 1 < minLength) {
                minLength = right - left + 1;
                start = left;
            }

            const leftChar = s[left];
            window.set(leftChar, window.get(leftChar) - 1);

            if (
                need.has(leftChar) &&
                window.get(leftChar) < need.get(leftChar)
            ) {
                have--;
            }

            left++;
        }
    }

    return minLength === Infinity
        ? ""
        : s.substring(start, start + minLength);
}
```

---
