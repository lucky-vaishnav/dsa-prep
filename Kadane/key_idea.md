### Problem It Solves

Find:

```
Maximum Sum Contiguous Subarray
```

Example:

```
[ -2, 1, -3, 4, -1, 2, 1, -5, 4 ]
```

Best subarray:

```
[4, -1, 2, 1]
```

Sum:

```
6
```

---

### Core Idea

Ask yourself at every element:

```
Should I:

1. Continue previous subarray?
OR
2. Start a new subarray from current element?
```

That's the entire algorithm.

---

### Visual Example

```
[-2, 1, -3, 4, -1, 2]
```

At:

```
1
```

Choices:

```
Previous sum + current
= -2 + 1
= -1

Current element only
= 1
```

Choose:

```
1
```

Because:

```
1 > -1
```

Start fresh.

---

At:

```
4
```

Choices:

```
Previous sum + 4
= -2 + 4
= 2

Start fresh
= 4
```

Choose:

```
4
```

Start fresh.

---

### Formula

This is the heart of Kadane:

```
currentSum =
max(
    nums[i],
    currentSum + nums[i]
)
```

Meaning:

```
Start New
OR
Extend Previous
```

---

### Template

```
functionkadane(nums) {
letcurrentSum=nums[0];
letmaxSum=nums[0];

for (leti=1;i<nums.length;i++) {

currentSum=Math.max(
nums[i],
currentSum+nums[i]
        );

maxSum=Math.max(
maxSum,
currentSum
        );
    }

returnmaxSum;
}
```

---

### How To Identify Kadane Problems

When reading problem statement, look for:

```
Maximum Sum
Minimum Sum
Maximum Profit
Contiguous
Subarray
Largest Gain
Continuous Segment
```

---

Keywords:

```
Contiguous
Continuous
Subarray
Range
Segment
```

Huge signal for Kadane.

---

### Pattern Recognition

If problem says:

```
Find best continuous range
```

Think:

```
Kadane
```

---

Example:

```
Find maximum sum subarray
```

Kadane.

---

Example:

```
Find minimum sum subarray
```

Kadane variant.

---

Example:

```
Maximum profit from one transaction
```

Can be converted to Kadane.

---

### Dry Run

Input:

```
[-2,1,-3,4,-1,2,1,-5,4]
```

| num | currentSum | maxSum |
| --- | --- | --- |
| -2 | -2 | -2 |
| 1 | 1 | 1 |
| -3 | -2 | 1 |
| 4 | 4 | 4 |
| -1 | 3 | 4 |
| 2 | 5 | 5 |
| 1 | 6 | 6 |
| -5 | 1 | 6 |
| 4 | 5 | 6 |

Answer:

```
6
```

---

### Interview Explanation

Say:

```
At every index I decide whether extending the previous subarray is beneficial or whether starting a new subarray from the current element gives a larger sum.

currentSum tracks the best subarray ending at current index.

maxSum tracks the global best answer.
```

Interviewers love this explanation.

---

### Important Variant #1

#### Maximum Sum Circular Subarray

LeetCode:

```
918. Maximum Sum Circular Subarray
```

Example:

```
[5,-3,5]
```

Answer:

```
10
```

Kadane + Minimum Kadane

Very common interview follow-up.

---

### Important Variant #2

#### Maximum Product Subarray

LeetCode:

```
152. Maximum Product Subarray
```

Not pure Kadane.

Need:

```
maxProduct
minProduct
```

because negative numbers flip sign.

Frequently asked.

---

### Important Variant #3

#### Maximum Absolute Sum

LeetCode:

```
1749. Maximum Absolute Sum of Any Subarray
```

Need:

```
Max Kadane
+
Min Kadane
```

---

### Important Variant #4

#### Maximum Profit

LeetCode:

```
121. Best Time to Buy and Sell Stock
```

Can be solved by:

```
Convert prices into differences

Apply Kadane
```

Though min-price approach is cleaner.

---

### Minimum Kadane

Sometimes asked.

Template:

```
functionminKadane(nums) {

letcurrentMin=nums[0];
letminSum=nums[0];

for (leti=1;i<nums.length;i++) {

currentMin=Math.min(
nums[i],
currentMin+nums[i]
        );

minSum=Math.min(
minSum,
currentMin
        );
    }

returnminSum;
}
```

Same logic.

Just:

```
max → min
```

---

### Common Mistake

Wrong:

```
letcurrentSum=0;
letmaxSum=0;
```

Fails:

```
[-5,-2,-8]
```

Expected:

```
-2
```

Returns:

```
0
```

Wrong.

---

Always:

```
letcurrentSum=nums[0];
letmaxSum=nums[0];
```

---

### Kadane Mental Model

Imagine:

```
currentSum
```

is your backpack.

At every number:

```
If backpack becomes worse than starting fresh,
throw it away.
```

That's literally Kadane.

---

### Practice Order

#### Easy

1. LeetCode 53 — Maximum Subarray
2. LeetCode 121 — Best Time to Buy and Sell Stock

---

#### Medium

1. LeetCode 918 — Maximum Sum Circular Subarray
2. LeetCode 1749 — Maximum Absolute Sum
3. LeetCode 152 — Maximum Product Subarray

---

#### Advanced

1. Maximum Sum Rectangle in Matrix
2. Maximum Sum Subarray With One Deletion (LC 1186)

---

### Notes Summary

```
Kadane Algorithm

Purpose:
- Maximum contiguous subarray sum

Core Idea:
- Extend previous subarray
OR
- Start new subarray

Formula:
currentSum = max(
    nums[i],
    currentSum + nums[i]
)

maxSum = max(
    maxSum,
    currentSum
)

Recognition:
- Maximum/Minimum Sum
- Contiguous
- Continuous Segment
- Subarray

Time:
O(n)

Space:
O(1)

Variants:
- Minimum Kadane
- Circular Kadane
- Maximum Product Subarray
- Maximum Absolute Sum
- Stock Profit Problems
```
