This is actually one of the **best XOR interview problems** because it demonstrates the core XOR property very cleanly.

# Problem

```
nums = [3,0,1]

Output = 2
```

Numbers are from:

```
0..n
```

Here:

```
n = 3

Expected numbers:
0,1,2,3
```

Array contains:

```
0,1,3
```

Missing:

```
2
```

---

# Approach 1: HashSet

```
functionmissingNumber(nums) {
constset=newSet(nums);

for (leti=0;i<=nums.length;i++) {
if (!set.has(i)) {
returni;
        }
    }
}
```

### Complexity

```
Time: O(n)
Space: O(n)
```

---

# Approach 2: Sum Formula

Expected sum:

```
functionmissingNumber(nums) {
constn=nums.length;

constexpected=n* (n+1)/2;

letactual=0;

for (constnumofnums) {
actual+=num;
    }

returnexpected-actual;
}
```

### Complexity

```
Time: O(n)
Space: O(1)
```

---

# Approach 3: XOR (Interview Favorite)

## XOR Rules

Remember:

```
a ^ a = 0
```

Example:

```
5 ^ 5 = 0
```

---

```
a ^ 0 = a
```

Example:

```
5 ^ 0 = 5
```

---

```
XOR is commutative
```

```
a ^ b ^ a = b
```

because:

```
(a ^ a) ^ b
= 0 ^ b
= b
```

---

# Key Idea

XOR all numbers from:

```
0..n
```

and XOR all numbers in array.

Everything cancels except the missing number.

---

## Example

```
nums = [3,0,1]
```

Expected:

```
0 ^ 1 ^ 2 ^ 3
```

Array:

```
3 ^ 0 ^ 1
```

Combined:

```
(0 ^ 1 ^ 2 ^ 3)
^
(3 ^ 0 ^ 1)
```

Rearrange:

```
0 ^ 0
^
1 ^ 1
^
3 ^ 3
^
2
```

All cancel:

```
0 ^ 0 ^ 0 ^ 2
```

Result:

```
2
```

---

# XOR Code

```
function missingNumber(nums) {
let xor=nums.length;

for (let i=0;i<nums.length;i++) {
xor^=i;
xor^=nums[i];
    }

return xor;
}

console.log(missingNumber([3,0,1]));// 2
```

---

# Dry Run

```
nums= [3,0,1]
```

Start:

```
xor=3
```

---

i = 0

```
xor^=0
```

```
3 ^ 0 = 3
```

```
xor^=3
```

```
3 ^ 3 = 0
```

---

i = 1

```
xor^=1
```

```
0 ^ 1 = 1
```

```
xor^=0
```

```
1 ^ 0 = 1
```

---

i = 2

```
xor^=2
```

```
1 ^ 2 = 3
```

```
xor^=1
```

```
3 ^ 1 = 2
```

Return:

```
2
```

---

# Why Interviewers Like XOR Here

Because it achieves:

| Approach | Time | Space |
| --- | --- | --- |
| HashSet | O(n) | O(n) |
| Sum Formula | O(n) | O(1) |
| XOR | O(n) | O(1) |

The XOR solution demonstrates that you understand:

```
Bit Manipulation
XOR Cancellation
```

which is a common interview topic.

### Question - why let xor=nums.length; ?

This is the part that confuses most people when they first see the XOR solution.

Let's look again:

```
functionmissingNumber(nums) {
letxor=nums.length;

for (leti=0;i<nums.length;i++) {
xor^=i;
xor^=nums[i];
    }

returnxor;
}
```

For:

```
nums = [3,0,1]
```

we have:

```
nums.length = 3
```

---

## What are we trying to XOR?

We need to XOR **all numbers from 0 to n**:

```
0 ^ 1 ^ 2 ^ 3
```

and also XOR all array elements:

```
3 ^ 0 ^ 1
```

so that everything cancels except the missing number.

---

## What does the loop XOR?

The loop runs:

```
for (leti=0;i<nums.length;i++)
```

which means:

```
i = 0,1,2
```

Notice:

```
3 is missing from i
```

because the loop stops at:

```
nums.length - 1
```

---

### Without the initial assignment

Suppose:

```
letxor=0;
```

Then loop does:

```
xor ^= 0
xor ^= 1
xor ^= 2
```

You only included:

```
0 ^ 1 ^ 2
```

But you needed:

```
0 ^ 1 ^ 2 ^ 3
```

You're missing the last number.

---

### That's why we start with

```
letxor=nums.length;
```

For this example:

```
letxor=3;
```

Now before loop even starts, we already have:

```
3
```

Then loop contributes:

```
0 ^ 1 ^ 2
```

Combined:

```
3 ^ 0 ^ 1 ^ 2
```

which is exactly:

```
0 ^ 1 ^ 2 ^ 3
```

the complete range we wanted.

---

## Another Way to Write It

This may look clearer:

```
functionmissingNumber(nums) {
letxor=0;

for (leti=0;i<=nums.length;i++) {
xor^=i;
    }

for (constnumofnums) {
xor^=num;
    }

returnxor;
}
```

Here we explicitly XOR:

```
0..n
```

first.

This works too.

---

## Why Interviewers Prefer the First Version

```
letxor=nums.length;

for (leti=0;i<nums.length;i++) {
xor^=i;
xor^=nums[i];
}
```

Because it combines both loops into one.

Complexity is still:

```
Time: O(n)
Space: O(1)
```

but fewer operations.
