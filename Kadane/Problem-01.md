Given an array:

```
nums = [-2,1,-3,4,-1,2,1,-5,4]
```

Find the maximum possible sum of a contiguous subarray.

Output:

```
6
```

because:

```
[4,-1,2,1]
```

sum is:

```
6
```

Tell me:

```
Pattern:
Why:
Brute Force Complexity:
Optimal Approach:
When do we continue current subarray?
When do we start a new subarray?
Time Complexity:
Space Complexity:
```

### My Answer
```
Pattern: Kadane Algo 
Why: maximum possible sum of a contiguous subarray , window size need to be decided if take next element or start new window
Brute Force Complexity: O(n^2) 
Optimal Approach: kadane 
When do we continue current subarray? till sum is increasing 
When do we start a new subarray? when sum decreases on taking next element and next element is grater than that sum 
Time Complexity: O(n) 
Space Complexity:O(1)
```
### Response

### Pattern

```
Kadane's Algorithm
```

✅ Correct

---

### Why

You wrote:

```
maximum possible sum of a contiguous subarray
```

✅ Perfect

The strongest clue is:

```
Maximum Sum
Contiguous Subarray
```

Whenever you see both together:

```
Kadane
```

should immediately come to mind.

---

### Brute Force

```
O(n²)
```

✅ Correct

---

### Optimal Approach

```
Kadane
```

✅ Correct

---

## Important Correction

You wrote:

```
continue till sum is increasing
```

❌ Not exactly.

Kadane doesn't care whether the sum is increasing or decreasing.

It only asks:

```
Is my current running sum helping me?
```

---

### Real Rule

Continue current subarray when:

```
currentSum >= 0
```

Because a positive sum helps future elements.

---

Start a new subarray when:

```
currentSum < 0
```

Because a negative sum hurts future elements.

---

### Example

```
[-2,1]
```

Current sum:

```
-2
```

Should we continue?

No.

Because:

```
-2 + 1 = -1
```

is worse than:

```
1
```

alone.

So:

```
start new subarray
```

---

### Kadane Formula

The most important line:

```
currentSum=Math.max(nums[i],currentSum+nums[i]);
```

This line asks:

```
Option 1:
Start new subarray

Option 2:
Continue current subarray
```

Choose whichever is better.
