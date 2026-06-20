**"in-place replacement"** is not a single DSA algorithm like Kadane, but it belongs to a very important family of patterns that interviewers love.

I would group it under:

```
In-Place Array Manipulation
```

or

```
Two-Pointer Write Index Pattern
```

This pattern appears constantly in FAANG-style interviews.

---

# Why Does This Pattern Exist?

Suppose:

```
[1,1,2,2,3]
```

Need:

```
Remove duplicates
```

Expected:

```
[1,2,3,?,?]
```

without:

```
newArray()
extra space
HashMap
```

Interviewer says:

```
Must modify array in-place
O(1) extra space
```

This is the signal.

---

# Core Idea

Maintain:

```
Read Pointer
Write Pointer
```

---

Visual

```
Read → scans all elements

Write → writes valid elements
```

---

# Template

```
let write=0;

for (let read=0;read<nums.length;read++) {

if (valid(nums[read])) {

nums[write]=nums[read];

write++;
    }
}
```

---

# Recognition Pattern

If problem says:

```
Modify array in-place
Return new length
O(1) extra space
Remove elements
Move elements
Compress array
```

Immediately think:

```
Read Pointer
Write Pointer
```

---

# Example 1

## LC 27 Remove Element

Input:

```
[3,2,2,3]
```

Remove:

```
3
```

---

Solution

```
let write=0;

for (let read=0;read<nums.length;read++) {

if (nums[read]!==val) {

nums[write]=nums[read];

write++;
    }
}

return write;
```

---

Complexity

```
Time: O(n)

Space: O(1)
```

---

# Example 2

## LC 26 Remove Duplicates From Sorted Array

Input:

```
[1,1,2,2,3]
```

Output:

```
[1,2,3]
```

---

Key observation:

```
Array already sorted
```

---

Solution

```
let write=1;

for (let read=1;read<nums.length;read++) {

if (nums[read]!==nums[read-1]) {

nums[write]=nums[read];

write++;
    }
}

return write;
```

---

# Example 3

## LC 283 Move Zeroes

Input:

```
[0,1,0,3,12]
```

Output:

```
[1,3,12,0,0]
```

---

Interview Favorite.

---

Step 1

Move non-zeroes.

```
let write=0;

for (let read=0;read<nums.length;read++) {

if (nums[read]!==0) {

nums[write]=nums[read];

write++;
    }
}
```

---

Step 2

Fill remaining.

```
while (write<nums.length) {

nums[write]=0;

write++;
}
```

---

# Example 4

## LC 75 Sort Colors

Input:

```
[2,0,2,1,1,0]
```

Output:

```
[0,0,1,1,2,2]
```

---

Pattern:

```
Dutch National Flag
```

This is an advanced version of in-place manipulation.

Uses:

```
Left Pointer
Current Pointer
Right Pointer
```

---

# Example 5

## LC 88 Merge Sorted Array

Input:

```
nums1=[1,2,3,0,0,0]
nums2=[2,5,6]
```

---

Very famous.

Instead of shifting elements:

Start from end.

```
Three Pointers
```

---

This is another in-place pattern.

---

# Pattern Categories

---

## Pattern A

### Filter Valid Elements

Examples:

```
Remove Element
Move Zeroes
```

Template:

```
if(valid){

nums[write]=nums[read];

write++;
}
```

---

## Pattern B

### Remove Duplicates

Examples:

```
LC 26
LC 80
```

Template:

```
if(nums[read]!=previous)
```

---

## Pattern C

### Reverse / Swap

Examples:

```
Reverse String
Reverse Array
```

Template:

```
left++
right--
```

---

## Pattern D

### Dutch National Flag

Examples:

```
Sort Colors
```

Uses:

```
3 pointers
```

---

## Pattern E

### Merge In Place

Examples:

```
Merge Sorted Array
```

Work from:

```
Backwards
```

---

# Interview Recognition Cheat Sheet

If problem says:

```
In-place
```

Think:

```
Can I overwrite existing positions?
```

---

If problem says:

```
Remove
Delete
Filter
```

Think:

```
Read Pointer
Write Pointer
```

---

If problem says:

```
Return new length
```

Think:

```
Write Pointer Pattern
```

---

If problem says:

```
Move all X to end
```

Think:

```
Compaction Pattern
```

---

# Must Practice Questions

### Easy

```
LC 27 Remove Element
LC 26 Remove Duplicates
LC 283 Move Zeroes
LC 344 Reverse String
```

---

### Medium

```
LC 75 Sort Colors
LC 80 Remove Duplicates II
LC 88 Merge Sorted Array
```

---

### Advanced

```
LC 41 First Missing Positive
LC 287 Find Duplicate Number
```

These use in-place indexing tricks.

---

# Notes Summary

```
In-Place Array Manipulation

Recognition:
- O(1) space
- Modify array
- Remove elements
- Return new length
- Move values

Core Pattern:

Read Pointer
Write Pointer

Template:

for(read){

   if(valid){

      nums[write]=nums[read];
      write++;
   }
}

Complexity:

Time O(n)
Space O(1)

Common Problems:

LC 26
LC 27
LC 75
LC 80
LC 88
LC 283
```

This pattern is one of the most common interview patterns after:

```
1. Two Pointers
2. Sliding Window
3. Prefix Sum
4. Kadane
5. In-Place Array Manipulation
```
