Prefix + Suffix Array is one of the highest-value DSA patterns for interviews because it turns many O(n²) problems into O(n).

Think of this pattern as: “Precompute information from the left and right so each index can be answered in O(1).”

### 1. Core Idea

For every index i, you often need:

- Something from left side (0..i-1)
- Something from right side (i+1..n-1)

Instead of recalculating every time, build:

- prefix[i] = answer for left side up to i
- suffix[i] = answer for right side from i

### 2. Visual Intuition

Prefix + Suffix Array is one of the highest-value DSA patterns for interviews because it turns many O(n²) problems into O(n).

Think of this pattern as: “Precompute information from the left and right so each index can be answered in O(1).”

### 1. Core Idea

For every index i, you often need:

- Something from left side (0..i-1)
- Something from right side (i+1..n-1)

Instead of recalculating every time, build:

- prefix[i] = answer for left side up to i
- suffix[i] = answer for right side from i

### 2. Visual Intuition

<img width="1400" height="803" alt="image (5)" src="https://github.com/user-attachments/assets/295ebba2-d2bf-4145-a704-677588d30256" />

Example array:

Index

0

1

2

3

4

Value

1

2

3

4

5

Suppose we need product of all elements except self.

For index 2:

- Left product = 1 × 2 = 2
- Right product = 4 × 5 = 20
- Answer = 2 × 20 = 40

This is the essence of the pattern.

### 3. Recognition Pattern

### When should you think Prefix + Suffix?

Interview Pattern

Problem statements containing:

- For each index
- Except self
- Left and right contribution
- Range information
- Maximum/Minimum before and after
- Water trapped
- Products/Sums excluding current element

Big signal

“For every element, compute something using all other elements.”

### 4. Generic Template

Step 1: Build prefix

Step 2: Build suffix

Step 3: Answer each index

### 5. Most Important Interview Problem

**LeetCode 238 — Product of Array Except Self**

Problem

Return an array where:

ans[i] = product of all nums except nums[i]

Optimal O(n) Solution

Why This Is Brilliant

| Pass | Stores |
| --- | --- |
| First pass | Left products |
| Second pass | Right products |

Complexity

Time

O(n)

Space

O(1) extra (excluding output)

### 6. Another Classic — Trapping Rain Water

<img width="949" height="594" alt="image (6)" src="https://github.com/user-attachments/assets/0b6994c0-4d69-4acf-b30f-44791e7db1e8" />

For each index:

water[i] = min(maxLeft[i], maxRight[i]) - height[i]

Here:

- prefix max = highest wall on left
- suffix max = highest wall on right

This is one of the most famous prefix/suffix applications.

### 7. Prefix Sum Variant

Sometimes you only need prefix.

Example:

Range Sum Query

### 8. How To Identify Quickly in Interviews

**Ask yourself**

- Do I need information from both left and right?
- Am I recomputing ranges repeatedly?
- Is there a for each index requirement?
- Can I precompute left and right answers once?

If YES → Prefix/Suffix pattern.

### 9. Must-Practice LeetCode List

**Easy**

- 303. Range Sum Query - Immutable
- 1480. Running Sum of 1d Array
- 724. Find Pivot Index

**Medium (Must Do)**

- 238. Product of Array Except Self ⭐
- 42. Trapping Rain Water ⭐
- 560. Subarray Sum Equals K (prefix + hashmap)
- 974. Subarray Sums Divisible by K

**Advanced**

- 1524. Number of Sub-arrays With Odd Sum
- 2483. Minimum Penalty for a Shop
- 2017. Grid Game

### 10. Interview Cheat Sheet

**Prefix + Suffix Pattern**

Use when

Need left + right info

Core idea

Precompute once, answer in O(1)

Time

Usually O(n)

Space

O(n) or O(1) optimized

Most important problem

LC 238

Classic variant

LC 42

Recognition keywords

except self, left/right, range

### Mental Model (Most Important)

**Remember this sentence**

“If every index needs information from both sides, build prefix and suffix arrays once.”

That single thought will help you recognize most interview problems using this pattern.

Example array:

Index

0

1

2

3

4

Value

1

2

3

4

5

Suppose we need product of all elements except self.

For index 2:

- Left product = 1 × 2 = 2
- Right product = 4 × 5 = 20
- Answer = 2 × 20 = 40

This is the essence of the pattern.

### 3. Recognition Pattern

### When should you think Prefix + Suffix?

Interview Pattern

Problem statements containing:

- For each index
- Except self
- Left and right contribution
- Range information
- Maximum/Minimum before and after
- Water trapped
- Products/Sums excluding current element

Big signal

“For every element, compute something using all other elements.”

### 4. Generic Template

Step 1: Build prefix

Step 2: Build suffix

Step 3: Answer each index

### 5. Most Important Interview Problem

**LeetCode 238 — Product of Array Except Self**

Problem

Return an array where:

ans[i] = product of all nums except nums[i]

Optimal O(n) Solution

Why This Is Brilliant

| Pass | Stores |
| --- | --- |
| First pass | Left products |
| Second pass | Right products |

Complexity

Time

O(n)

Space

O(1) extra (excluding output)

### 6. Another Classic — Trapping Rain Water

Trapping Rainwater - TUF+

For each index:

water[i] = min(maxLeft[i], maxRight[i]) - height[i]

Here:

- prefix max = highest wall on left
- suffix max = highest wall on right

This is one of the most famous prefix/suffix applications.

### 7. Prefix Sum Variant

Sometimes you only need prefix.

Example:

Range Sum Query

### 8. How To Identify Quickly in Interviews

**Ask yourself**

- Do I need information from both left and right?
- Am I recomputing ranges repeatedly?
- Is there a for each index requirement?
- Can I precompute left and right answers once?

If YES → Prefix/Suffix pattern.

### 9. Must-Practice LeetCode List

**Easy**

- 303 Range Sum Query - Immutable
- 1480 Running Sum of 1d Array
- 724 Find Pivot Index

**Medium (Must Do)**

- 238 Product of Array Except Self ⭐
- 42 Trapping Rain Water ⭐
- 560 Subarray Sum Equals K (prefix + hashmap)
- 974 Subarray Sums Divisible by K

**Advanced**

- 1524 Number of Sub-arrays With Odd Sum
- 2483 Minimum Penalty for a Shop
- 2017 Grid Game

### 10. Interview Cheat Sheet

**Prefix + Suffix Pattern**

Use when

Need left + right info

Core idea

Precompute once, answer in O(1)

Time

Usually O(n)

Space

O(n) or O(1) optimized

Most important problem

LC 238

Classic variant

LC 42

Recognition keywords

except self, left/right, range

### Mental Model (Most Important)

**Remember this sentence**

“If every index needs information from both sides, build prefix and suffix arrays once.”

That single thought will help you recognize most interview problems using this pattern.
