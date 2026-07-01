Given an array:

```
nums = [2,3,1,2,4,3]
target = 7
```

Find the **minimum length** of a contiguous subarray whose sum is **greater than or equal to** the target.

Return the minimum length.

Example:

```
Input:
target = 7
nums = [2,3,1,2,4,3]

Output:
2
```

Because:

```
[4,3]
```

has length `2`, which is the minimum.

---

Tell me:

```
Pattern:
Why:
Window Type:
Expand When:
Shrink When:
Time Complexity:
Space Complexity:
```

## Review

### Pattern

```
Variable (Dynamic) Sliding Window
```

✅ Correct

---

### Why

You wrote:

```
contiguous subarray whose sum is greater than or equal to
```

✅ Perfect.

These are the recognition clues:

- Contiguous subarray
- Sum condition
- Minimum/Maximum length

→ Think **Variable Sliding Window**

---

### Window Type

```
Dynamic
```

✅ Correct

---

### Expand When

You wrote:

```
total sum < target
```

✅ Correct

Keep expanding until the window satisfies the condition.

---

### Shrink When

You wrote:

```
total sum >= target
```

✅ Correct.

One more important step:

```
Before shrinking:
Calculate current window length.

Then:
Subtract left element.
Move left.
Continue shrinking while sum >= target.
```

That's how we ensure we get the **minimum** length.

---

### Complexity

```
Time : O(n)
Space: O(1)
```

✅ Correct

Although there is a nested `while`, each element is:

- added once
- removed once

So total work is still **O(n)**.

---

# Optimal Code

```jsx
function minSubArrayLen(target,nums) {

let left=0;
let sum=0;
let minLength=Infinity;

for (let right = 0;right<nums.length;right++) {

	sum += nums[right];

	while (sum>=target) {

     minLength = Math.min(minLength,right-left+1);

     sum-=nums[left];
     left++;
        }
    }

return minLength===Infinity?0:minLength;
}

console.log(minSubArrayLen(7, [2,3,1,2,4,3]));// 2
```

---

# Dry Run

```
target=7

nums= [2,3,1,2,4,3]
```

Start

```
left = 0
sum = 0
minLength = Infinity
```

---

### right = 0

```
sum = 2
```

Less than target.

Expand.

---

### right = 1

```
sum = 5
```

Expand.

---

### right = 2

```
sum = 6
```

Expand.

---

### right = 3

```
sum = 8
```

Now

```
sum >= target
```

Window

```
[2,3,1,2]
```

Length

```
4
```

Update

```
minLength = 4
```

Shrink

```
sum = 6
left = 1
```

---

### right = 4

Add

```
4
```

Sum

```
10
```

Window

```
[3,1,2,4]
```

Length

```
4
```

Shrink

```
[1,2,4]
```

Length

```
3
```

Update

```
minLength = 3
```

Shrink again

```
sum = 6
```

Stop.

---

### right = 5

Add

```
3
```

Sum

```
9
```

Window

```
[2,4,3]
```

Length

```
3
```

Update

```
minLength = 3
```

Shrink

```
[4,3]
```

Length

```
2
```

Update

```
minLength = 2
```

Shrink

```
sum = 3
```

Stop.

Answer

```
2
```
