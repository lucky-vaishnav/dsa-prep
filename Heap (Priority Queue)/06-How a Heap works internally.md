Awesome! 🎉 This is the final learning chapter before we start Heap problems.

I actually think this is **the most valuable part** because in interviews, you're rarely asked:

> "Implement a Heap."

Instead, you're asked:

> "Solve this problem."

Your job is to recognize:

> **"This is a Heap problem."**

So today we'll learn **how to recognize Heap problems instantly.**

---

# Part 2.8 — Priority Queue & Interview Templates

---

# Step 1 — First Understand Priority Queue

This is where many people get confused.

## Heap ≠ Priority Queue

Think of it like this:

```text
ArrayList  → Data Structure
Stack      → Data Structure
Heap       → Data Structure

Priority Queue → Abstract Data Type (Behavior)
```

Heap is **how** we implement a Priority Queue.

---

## What is a Priority Queue?

Normal Queue

```text
10

20

30

↓

10 comes first (FIFO)
```

Priority Queue

```text
10 (priority 2)

20 (priority 10)

30 (priority 5)

↓

20 comes first
```

The **highest priority** element comes out first.

That's exactly what a Max Heap gives us.

---

## Example

Hospital Emergency Room

```text
Patient A
Priority 2

Patient B
Priority 10

Patient C
Priority 5
```

Doctor doesn't see patients in arrival order.

Doctor sees

```text
B

↓

C

↓

A
```

Priority Queue.

---

# Heap is used because...

It gives

```text
Insert

O(log n)

Remove Highest Priority

O(log n)

Peek Highest Priority

O(1)
```

Exactly what a Priority Queue needs.

---

# ⭐ Recognition Rule #1

Whenever you read...

```text
Highest

Lowest

Maximum

Minimum
```

Don't immediately think Heap.

Ask:

> **One time or repeatedly?**

This is the biggest interview trick.

---

# Case 1

Find

```text
Largest Element
```

once.

Example

```text
Maximum element in array
```

Need Heap?

❌ No.

Just scan once.

```text
O(n)
```

---

# Case 2

Find

```text
Largest

again

again

again...
```

Need Heap?

✅ Yes.

Because removing repeatedly from a Heap is efficient.

---

# ⭐ Recognition Rule #2

Whenever you see

```text
Top K
```

Your brain should immediately say

```text
Heap
```

Examples

```text
Top K Frequent Elements

Top K Largest

Top K Smallest

K Closest Points

K Closest Numbers
```

These are classic Heap problems.

---

# Why Heap?

Suppose

```text
1 million numbers
```

Need only

```text
Top 10
```

Sorting

```text
O(n log n)
```

Wasteful.

Heap

```text
O(n log k)
```

Much better.

---

# ⭐ Recognition Rule #3

Whenever you see

```text
Stream
```

Think Heap.

Example

```text
Find Median from Data Stream
```

Numbers arrive continuously.

Need to maintain

Median

Can't sort every time.

Use

```text
Two Heaps
```

---

# ⭐ Recognition Rule #4

Whenever you see

```text
Merge K
```

Think Heap.

Examples

```text
Merge K Sorted Lists

Merge K Sorted Arrays
```

Very famous interview question.

---

# ⭐ Recognition Rule #5

Whenever you repeatedly need the

```text
Next Smallest

Next Largest
```

Think Heap.

---

# Decision Tree

This is what I personally think during interviews.

```text
Need Largest Once?

↓

Linear Scan

-------------------------

Need Smallest Once?

↓

Linear Scan

-------------------------

Need Top K?

↓

Heap

-------------------------

Need Repeated Maximum?

↓

Heap

-------------------------

Need Repeated Minimum?

↓

Heap

-------------------------

Need Streaming?

↓

Heap

-------------------------

Need Merge K?

↓

Heap
```

---

# ⭐ Min Heap vs Max Heap

This confuses almost everyone initially.

Here's the easiest rule.

---

## Want Largest?

Use

```text
Max Heap
```

Root

```text
Largest
```

---

## Want Smallest?

Use

```text
Min Heap
```

Root

```text
Smallest
```

Easy.

---

## But...

What about

```text
Top K Largest
```

Most beginners say

```text
Max Heap
```

❌ Surprisingly, that's **not** the best choice.

---

Imagine

```text
1 million numbers

Need Top 10 Largest
```

If you use a Max Heap,

you insert

```text
1 million
```

elements.

Huge.

Instead...

Maintain a **Min Heap of size K**.

Example

K = 3

Numbers

```text
5 1 9 2 8 7
```

Heap

```text
1 5 9
```

Next

```text
2
```

Remove

```text
1
```

Insert

```text
2
```

Heap

```text
2 5 9
```

Continue...

At the end,

Heap contains

```text
Top 3 Largest
```

Only.

---

# ⭐ Interview Rule

| Problem           | Heap         |
| ----------------- | ------------ |
| Largest Element   | No Heap      |
| Smallest Element  | No Heap      |
| Top K Largest     | **Min Heap** |
| Top K Smallest    | **Max Heap** |
| Repeated Largest  | Max Heap     |
| Repeated Smallest | Min Heap     |
| Merge K Lists     | Min Heap     |
| Median Stream     | Two Heaps    |

🚨 This table is worth memorizing.

---

# The 5 Templates

These are the only Heap patterns you'll repeatedly use.

---

## Template 1

Top K Largest

```text
Maintain

Min Heap

Size K
```

---

## Template 2

Top K Smallest

```text
Maintain

Max Heap

Size K
```

---

## Template 3

K Closest

```text
Maintain

Heap

Based on Distance
```

---

## Template 4

Merge K Lists

```text
Always remove

Smallest

Insert next element
```

---

## Template 5

Median

```text
Max Heap

+

Min Heap
```

---

# When NOT to Use Heap

Very important.

Suppose

```text
Need Largest Once
```

Heap

```text
O(n)
```

Scan

```text
O(n)
```

Scan is simpler.

---

Suppose

```text
Need Top K

Very large array

Need answer once
```

Quick Select

may be better.

---

Suppose

Need

```text
Fully Sorted Array
```

Heap?

Works.

But Merge Sort / Quick Sort are usually preferred.

---

# Recognition Cheat Sheet (Notebook)

```text
HEAP RECOGNITION

Think Heap when you see:

✓ Top K
✓ K Closest
✓ Merge K
✓ Repeated Maximum
✓ Repeated Minimum
✓ Stream
✓ Priority Queue

Min Heap:
✓ Smallest
✓ Top K Largest

Max Heap:
✓ Largest
✓ Top K Smallest

No Heap:
✓ Largest Once
✓ Smallest Once
✓ Full Sorting
```

---

# How min heap is useful for finding k largest elements ?

Absolutely. This confusion is **the single biggest hurdle** in Heap problems. Once this clicks, you'll solve most Top K problems naturally.

Let's forget code completely and think like an interviewer.

---

# The Problem

> Find the **3 largest** numbers.

Array:

```text
[5, 1, 9, 2, 8, 7]
```

---

# First Thought

Most people think:

> "Largest means Max Heap."

That seems logical.

Let's see.

---

# Approach 1 - Max Heap

Build Max Heap with all numbers.

```
9
8
7
5
2
1
```

Now remove top 3.

```
9

8

7
```

Works.

But...

How many numbers did we store?

```
6
```

Imagine

```
1,000,000 numbers

Need only Top 10.
```

You're storing

```
1,000,000
```

numbers.

That's unnecessary.

---

# ⭐ Think differently

Ask yourself:

> What information do I actually need?

Need

```
Top 3 Largest
```

Not all one million.

So why keep one million?

---

# New Idea

Suppose I promise:

> I'll never store more than **3** numbers.

Can we still solve it?

Yes.

---

# Which 3 numbers should we keep?

Start reading numbers.

```
5
```

Keep it.

Heap

```
5
```

---

Read

```
1
```

Keep it.

Heap

```
1 5
```

---

Read

```
9
```

Keep it.

Heap

```
1 5 9
```

Heap size reached

```
K = 3
```

Now ask yourself...

---

# Very Important Question

Among these three,

```
1 5 9
```

Which one is the **least useful**?

Obviously

```
1
```

Because we're looking for the **largest** numbers.

If a larger number comes later,

who should leave?

```
1
```

Exactly.

So we want the **smallest** among our Top K to be easy to remove.

---

# Which Heap gives the smallest instantly?

✅ **Min Heap**

Root

```
1
```

Perfect.

---

Next number

```
2
```

Compare with root.

```
2 > 1
```

Great!

That means

```
2
```

deserves to be in Top 3 more than

```
1
```

So remove

```
1
```

Insert

```
2
```

Heap

```
2 5 9
```

---

Next

```
8
```

Compare with root

```
2
```

```
8 > 2
```

Remove

```
2
```

Insert

```
8
```

Heap

```
5 8 9
```

---

Next

```
7
```

Compare with root

```
5
```

```
7 > 5
```

Remove

```
5
```

Insert

```
7
```

Heap

```
7 8 9
```

Done.

---

# ⭐⭐⭐ The Biggest Insight

Notice something amazing.

The Min Heap **never contains the answer in sorted order**.

It only guarantees:

> **The smallest among the Top K is always at the root.**

That's exactly what we need.

---

# The Memory Trick

Suppose you're selecting the **top 5 students** in a class.

Current selected students:

```
80

85

90

92

95
```

A new student arrives with

```
88
```

Who should leave?

The

```
80
```

student.

Not

```
95
```

Not

```
92
```

Always the **smallest** among the selected students.

So you want instant access to the smallest selected student.

That's why you use a **Min Heap**.

---

# Rule You'll Never Forget

## Top K Largest

Ask yourself:

> If a better candidate comes, who should leave?

Answer:

> The smallest among the current Top K.

So we keep the smallest at the top.

➡️ **Min Heap**

---

## Top K Smallest

Now reverse it.

Current

```
1

2

3
```

New number

```
0
```

Who should leave?

```
3
```

The largest.

So we need instant access to the largest.

➡️ **Max Heap**

---

# One Sentence to Memorize

### Top K Largest

> **Use a Min Heap because the smallest among the current Top K is the one that may need to be removed.**

### Top K Smallest

> **Use a Max Heap because the largest among the current Top K is the one that may need to be removed.**

---
```javascript
class MinHeap {
    constructor() {
        this.heap = [];
    }

    size() {
        return this.heap.length;
    }

    peek() {
        return this.heap[0];
    }

    push(val) {
        this.heap.push(val);
        this.heapifyUp();
    }

    pop() {
        if (this.heap.length === 1) return this.heap.pop();

        const root = this.heap[0];
        this.heap[0] = this.heap.pop();
        this.heapifyDown();

        return root;
    }

    heapifyUp() {
        let i = this.heap.length - 1;

        while (i > 0) {
            let p = Math.floor((i - 1) / 2);

            if (this.heap[p] <= this.heap[i]) break;

            [this.heap[p], this.heap[i]] =
                [this.heap[i], this.heap[p]];

            i = p;
        }
    }

    heapifyDown() {
        let i = 0;

        while (true) {

            let smallest = i;

            let left = 2 * i + 1;
            let right = 2 * i + 2;

            if (
                left < this.heap.length &&
                this.heap[left] < this.heap[smallest]
            ) {
                smallest = left;
            }

            if (
                right < this.heap.length &&
                this.heap[right] < this.heap[smallest]
            ) {
                smallest = right;
            }

            if (smallest === i) break;

            [this.heap[i], this.heap[smallest]] =
                [this.heap[smallest], this.heap[i]];

            i = smallest;
        }
    }
}

function topKLargest(nums, k) {

    const heap = new MinHeap();

    for (const num of nums) {

        heap.push(num);

        if (heap.size() > k) {
            heap.pop();
        }
    }

    return heap.heap.sort((a, b) => b - a);
}

console.log(topKLargest([5,1,9,2,8,7],3));

// [9,8,7]
```
| Approach              | Time           | Best When                                     |
| --------------------- | -------------- | --------------------------------------------- |
| Sort                  | O(n log n)     | Small arrays / easiest solution               |
| **Min Heap (size K)** | **O(n log k)** | ⭐ General interview solution for Top K        |
| Quick Select          | Average O(n)   | Fastest, but more complex (we'll learn later) |
