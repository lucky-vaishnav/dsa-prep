**Bit Manipulation** is one of the highest ROI topics for interviews because:

```
Many problems that look O(n) or O(n²)
can become O(1) or O(log n)
using bit tricks.
```

For senior interviews, you're not expected to memorize 50 tricks. You need:

```
1. Binary fundamentals
2. Core operators
3. Common patterns
4. Recognition skills
5. Top LeetCode questions
```

---

# 1. Why Bit Manipulation Exists

Computers store everything as:

```
0
1
```

Example:

```
13

Binary:

1101
```

```
8 + 4 + 0 + 1
```

---

# 2. Core Operators

---

## AND (&)

Rule:

```
1 & 1 = 1

1 & 0 = 0

0 & 1 = 0

0 & 0 = 0
```

Example:

```
13 = 1101
10 = 1010

AND

1000

= 8
```

```
13&10
```

returns:

```
8
```

---

## OR (|)

Rule:

```
1 | 1 = 1
1 | 0 = 1
0 | 1 = 1
0 | 0 = 0
```

Example:

```
1101
1010
----
1111

= 15
```

---

## XOR (^)

Most important operator.

Rule:

```
1 ^ 1 = 0
0 ^ 0 = 0
1 ^ 0 = 1
0 ^ 1 = 1
```

Think:

```
Same → 0
Different → 1
```

Example:

```
1101
1010
----
0111

= 7
```

---

## NOT (~)

Flips bits.

```
1010

↓

0101
```

---

## Left Shift (<<)

```
x<<1
```

means:

```
multiply by 2
```

Example:

```
5 = 0101

<< 1

1010 = 10
```

---

## Right Shift (>>)

```
x>>1
```

means:

```
divide by 2
```

Example:

```
8 = 1000

>> 1

0100 = 4
```

---

# Most Important Bit Patterns

---

# Pattern 1

## Check Even/Odd

Question:

```
Number even or odd?
```

Logic:

Last bit tells everything.

```
Even

100
110
1000

last bit = 0
```

```
Odd

101
111
1001

last bit = 1
```

Code:

```
if ((n&1)===0)
```

---

Recognition:

```
Check parity
Even/Odd
```

Immediately think:

```
n & 1
```

---

# Pattern 2

## Check Power Of Two

Example:

```
1
2
4
8
16
32
```

Binary:

```
1      = 0001
2      = 0010
4      = 0100
8      = 1000
```

Observation:

```
Exactly ONE bit set
```

---

Magic Formula:

```
n>0&& (n& (n-1))===0
```

---

Why?

Example:

```
8

1000
```

```
8 - 1

0111
```

AND:

```
1000
0111
----
0000
```

---

Recognition:

```
Power of Two
Power of Four
Single set bit
```

---

LeetCode:

```
231. Power of Two
```

---

# Pattern 3

## Count Set Bits

Example:

```
13

1101

Count = 3
```

---

Naive:

```
while(n){
count+=n&1;
n>>=1;
}
```

---

Optimized

Brian Kernighan Algorithm

Magic:

```
n=n& (n-1)
```

removes one set bit.

Example:

```
1101

↓

1100

↓

1000

↓

0000
```

Count:

```
3
```

---

Recognition:

```
Count 1s
Hamming Weight
Number of set bits
```

---

LeetCode:

```
191. Number of 1 Bits
```

---

# Pattern 4

## Find Single Number

Question:

```
All numbers appear twice.
One appears once.
```

Example:

```
[2,2,1]
```

Answer:

```
1
```

---

Magic XOR properties:

```
a ^ a = 0

a ^ 0 = a
```

Example:

```
2 ^ 2 ^ 1

0 ^ 1

1
```

Code:

```
letans=0;

for (constnumofnums)
ans^=num;
```

---

Recognition:

```
Every element twice
One unique
```

Immediately think:

```
XOR
```

---

LeetCode:

```
136. Single Number
```

---

# Pattern 5

## Missing Number

Example:

```
[3,0,1]

Missing 2
```

Use XOR.

---

LeetCode:

```
268. Missing Number
```

---

# Pattern 6

## Get ith Bit

Question:

```
Check 3rd bit
```

Formula:

```
(n>>i)&1
```

---

Example:

```
13

1101
```

Check bit 2:

```
1
```

---

# Pattern 7

## Set ith Bit

Formula:

```
n| (1<<i)
```

---

Example:

```
1000

Set bit 1

1010
```

---

# Pattern 8

## Clear ith Bit

Formula:

```
n&~(1<<i)
```

---

Example:

```
1111

Clear bit 2

1011
```

---

# Pattern 9

## Toggle ith Bit

Formula:

```
n^ (1<<i)
```

---

Example:

```
1010

Toggle bit 1

1000
```

---

# Pattern 10

## Subset Generation

Very common.

Example:

```
[1,2,3]
```

Total subsets:

```
2^n
```

For:

```
n = 3
```

```
000
001
010
011
100
101
110
111
```

Each bit:

```
Take element
Don't take element
```

---

LeetCode:

```
78. Subsets
```

---

# Interview Recognition Guide

If problem says:

```
Unique number
```

Think:

```
XOR
```

---

If problem says:

```
Power of Two
```

Think:

```
n & (n - 1)
```

---

If problem says:

```
Count bits
```

Think:

```
Brian Kernighan
```

---

If problem says:

```
Subset generation
```

Think:

```
Bitmasking
```

---

If problem says:

```
Toggle flags
```

Think:

```
XOR
```

---

# Most Important LeetCode Practice

### Easy

```
136. Single Number
191. Number of 1 Bits
231. Power of Two
338. Counting Bits
268. Missing Number
```

---

### Medium

```
78. Subsets
137. Single Number II
260. Single Number III
318. Maximum Product of Word Lengths
```

---

### Hard

```
421. Maximum XOR of Two Numbers
```

---

# Interview Cheat Sheet

```
Check Odd:
n & 1

Power of Two:
n & (n - 1)

Remove Lowest Set Bit:
n & (n - 1)

Count Bits:
Brian Kernighan

Get Bit:
(n >> i) & 1

Set Bit:
n | (1 << i)

Clear Bit:
n & ~(1 << i)

Toggle Bit:
n ^ (1 << i)

Unique Number:
XOR

Generate Subsets:
Bitmask
```

---

# Notes Summary

```
Bit Manipulation

Core Operators:
&
|
^
~
<<
>>

Most Important Patterns:
1. Even/Odd
2. Power of Two
3. Count Set Bits
4. Single Number
5. Missing Number
6. Get Bit
7. Set Bit
8. Clear Bit
9. Toggle Bit
10. Bitmask Subsets

Recognition:
Unique Number -> XOR
Power of Two -> n&(n-1)
Count Bits -> Brian Kernighan
Subsets -> Bitmask

Complexities:
Most operations O(1)
Count bits O(number of set bits)
```

For interviews, if you master the first **5 patterns (Odd/Even, Power of Two, Count Bits, Single Number, Missing Number)**, you'll solve roughly **80% of bit manipulation questions** that appear in coding rounds.
