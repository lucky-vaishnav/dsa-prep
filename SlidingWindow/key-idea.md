# Key Idea

Expand → shrink window while maintaining a condition using a frequency/map.

**Use when:**

You need something from *contiguous / continuous* subarrays or substrings.

Typical patterns:

- Max / Min
- Longest / Shortest
- Count of something inside window
- Valid / Invalid windows
- Exactly K… / At most K…

## **When to immediately think Sliding Window**

👉 If the problem has:

- “Subarray”
- “Substring”
- “Contiguous”
- “At most K”
- “Longest / shortest”
- “Maximum sum / minimum size”

→ 99% chance **sliding window**.

# **Sliding Window Types**

## **1. Fixed-size window**

Window size K is known.

Use when:

- max sum of size K
- average of size K
- count subarrays of size K

### **Template — Fixed Window**

```jsx
let left = 0;
let windowSum = 0;
let result = something;

for (let right = 0; right < arr.length; right++) {
    windowSum += arr[right];

    // shrink when window size > k
    if (right - left + 1 > k) {
        windowSum -= arr[left];
        left++;
    }

    // when exactly size k → process
    if (right - left + 1 == k) {
        result = Math.max(result, windowSum); // or min, or update
    }
}

```

---

## **2. Variable-size window**

Window expands and shrinks based on some *condition* (frequency, uniqueness, sum limit, etc.)

Use when:

- longest substring without repeating characters
- minimum window substring
- subarray sum ≤ K
- count subarrays with at most K odd numbers
- sliding window with frequency maps

### **Template —Variable Window (general)** longestSubstringAtMostM
```jsx
let left = 0;
let map = {};         // freq map if needed
let best = 0;         // longest/shortest result

for (let right = 0; right < s.length; right++) {

    // expand: include s[right]
    map[s[right]] = (map[s[right]] || 0) + 1;

    // shrink while invalid
    while (windowIsInvalid(map)) {
        map[s[left]]--;
        if (map[s[left]] === 0) delete map[s[left]];
        left++;
    }

    // window is valid here → update result
    best = Math.max(best, right - left + 1);
}

    return best;
}
```

