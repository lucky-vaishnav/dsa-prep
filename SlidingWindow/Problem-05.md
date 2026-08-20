### 🔵 Q — : Longest Substring Without Repeating Characters

```text id="0v9n2k"
s = "abcabcbb"

Output = 3
```

The longest substring without repeating characters is:

```text id="y8x6q1"
"abc"
```

Think about:

* Brute force approach
* Which pattern you've already learned?
* What will your window contain?
* When do we move `left`?
* When do we move `right`?
* Time & space complexity?

This is a good test of whether your **variable-size Sliding Window** understanding is strong, especially after the Subarray Sum discussion.

---
### My Thought-
finding longest substring without repeating characters. So as we know it, substring will be the continuous string. So, and we have a limitation to use, which is the unique value should be there. So by using those value, we can use sliding window approach, better approach. And we can use the left pointer and the right pointer, and we should also use hash map just to store the character count. And we will be expanding the window if there is no repeated character by checking in the map. And if there is repeated character, we will set the left pointer to right, the right pointer value will be assigned to left, and right will be plus plus. I think that will work with this approach. And for brute force, the case will be O of n square. So yeah, and you can also share the code for both the approach. And time complexity of sliding window is O of n, space complexity will be O of 1.

---
Yes — your **pattern recognition is correct: Sliding Window + HashSet/HashMap**. I'd give this **8.5/10**.

There are two corrections.

### 1. When duplicate is found

You said:

> set `left = right`

Not quite.

If the duplicate character is already inside the current window, we need to move `left` **only past the previous occurrence of that character**, not necessarily all the way to `right`.

Using a `Map`, we can store the character's latest index:

```text id="h3s6k2"
s = "abcabcbb"

When we reach the second 'a':

window = "abc"
             ↑
previous 'a' was at index 0

left = 0 + 1 = 1
```

So the window becomes:

```text id="x6v8q1"
"bca"
```

### 2. Space complexity

You said `O(1)`.

For the standard English-character version, you can technically call it **`O(1)`** because there are at most 26/128/256 possible characters depending on the assumed character set.

For a **general Unicode string**, it's safer to say:

```text
O(min(n, character-set-size))
```

For interview purposes, **`O(1)` auxiliary space** is commonly accepted when the character set is fixed.

---

## Brute Force

Generate every substring and check whether it contains duplicates:

```javascript
function lengthOfLongestSubstring(s) {
    let maxLength = 0;

    for (let i = 0; i < s.length; i++) {

        const seen = new Set();

        for (let j = i; j < s.length; j++) {

            if (seen.has(s[j])) {
                break;
            }

            seen.add(s[j]);

            maxLength = Math.max(
                maxLength,
                j - i + 1
            );
        }
    }

    return maxLength;
}
```

Worst case:

```text
Time  → O(n²)
Space → O(n)
```

---

## Optimal — Sliding Window + Map

```javascript
function lengthOfLongestSubstring(s) {

    const lastSeen = new Map();

    let left = 0;
    let maxLength = 0;

    for (let right = 0; right < s.length; right++) {

        const char = s[right];

        if (lastSeen.has(char)) {
            left = Math.max(
                left,
                lastSeen.get(char) + 1
            );
        }

        lastSeen.set(char, right);

        maxLength = Math.max(
            maxLength,
            right - left + 1
        );
    }

    return maxLength;
}
```

For:

```text
"abcabcbb"
```

the longest window is:

```text
"abc"
```

so:

```text
3
```

### Complexity

```text
Time  → O(n)
Space → O(1) for a fixed character set
```

### ⭐ Important Sliding Window distinction

This is slightly different from the **Subarray Sum = K** problem we discussed.

Here, the window has a property we can maintain:

```text
"window contains no duplicate characters"
```

So Sliding Window works naturally.

With **Subarray Sum = K**, especially with negative numbers, we couldn't reliably decide whether to shrink or expand based on the sum, which is why we needed **Prefix Sum + HashMap**.

That distinction is worth remembering.
