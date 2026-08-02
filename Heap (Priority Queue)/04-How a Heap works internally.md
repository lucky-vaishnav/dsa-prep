This is honestly one of my favorite data structure concepts because it **looks impossible at first**.

Most people think:

> "If insertion is O(log n), then building a heap with n elements must be O(n log n)."

**Surprisingly, that's wrong.** Today you'll understand why.

---

# Part 2.6 - Build Heap (Heapify an Entire Array)

## First Question

Suppose I give you this array:

```text
[40,20,90,10,30,80,70]
```

I say:

> Convert this into a **Max Heap**.

How would you do it?

Most people say:

```text
Create an empty heap

↓

Insert 40

↓

Insert 20

↓

Insert 90

↓

Insert 10

...
```

That's absolutely correct.

### Complexity

There are `n` insertions.

Each insertion is

```text
O(log n)
```

Total

```text
O(n log n)
```

Works perfectly.

---

# But...

Interviewer asks:

> Can you do better?

🤔

---

# The Brilliant Observation

Instead of building a heap one element at a time...

Ask yourself:

> **Which nodes can actually violate the heap property?**

Look at this tree:

```text
          40
        /    \
      20      90
     /  \    /  \
   10   30 80   70
```

Leaves are

```text
10
30
80
70
```

Can a leaf violate the heap property?

No.

Why?

A leaf has **no children**.

Heap property is:

```text
Parent >= Children
```

Leaves have no children.

So they're **already valid heaps**.

💡 **This is the key insight.**

---

# So where do we start?

We **don't** start from the root.

We **don't** start from index 0.

We start from the **last non-leaf node**.

---

# ⭐ How do we find the last non-leaf?

Formula:

```text
Math.floor(n / 2) - 1
```

Memorize this.

---

Example

```text
Array length = 7
```

Last non-leaf:

```text
Math.floor(7/2)-1

3-1

2
```

Index

```text
2
```

Value

```text
90
```

Everything after index 2

```text
3
4
5
6
```

are leaves.

---

# The Algorithm

Start from

```text
last non-leaf
```

Move backwards.

```text
2

↓

1

↓

0
```

At every node

perform

```text
Heapify Down
```

That's it.

---

# Example

Initial array

```text
[40,20,90,10,30,80,70]
```

---

## Index 2

Value

```text
90
```

Children

```text
80

70
```

Already valid.

Nothing changes.

---

## Index 1

Value

```text
20
```

Children

```text
10

30
```

Largest child

```text
30
```

Swap.

Array

```text
[40,30,90,10,20,80,70]
```

Done.

---

## Index 0

Current

```text
40
```

Children

```text
30

90
```

Largest

```text
90
```

Swap.

```text
[90,30,40,10,20,80,70]
```

Continue Heapify Down.

Current index

```text
2
```

Children

```text
80

70
```

Largest

```text
80
```

Swap.

Final

```text
[90,30,80,10,20,40,70]
```

Done.

That's now a valid Max Heap.

---

# Code

```javascript
function buildMaxHeap(nums) {

    const lastNonLeaf = Math.floor(nums.length / 2) - 1;

    for (let i = lastNonLeaf; i >= 0; i--) {
        heapifyDown(nums, i);
    }

    return nums;
}

function heapifyDown(heap, index) {

    while (true) {

        let largest = index;

        const left = 2 * index + 1;
        const right = 2 * index + 2;

        if (
            left < heap.length &&
            heap[left] > heap[largest]
        ) {
            largest = left;
        }

        if (
            right < heap.length &&
            heap[right] > heap[largest]
        ) {
            largest = right;
        }

        if (largest === index) break;

        [heap[index], heap[largest]] =
            [heap[largest], heap[index]];

        index = largest;
    }
}
```

---

# 🤯 The Big Question

Why is this

```text
O(n)
```

and **not**

```text
O(n log n)
```

At first glance,

we're calling Heapify Down multiple times.

Shouldn't that be

```text
n × log n
```

?

**No.**

This is one of the most famous interview proofs.

---

# Intuition (Don't memorize the proof)

Most nodes are **near the bottom**.

Example:

```text
Level 0

1 node

Can move 3 levels

---------------

Level 1

2 nodes

Can move 2 levels

---------------

Level 2

4 nodes

Can move 1 level

---------------

Level 3

8 nodes

Leaves

Can move 0 levels
```

Notice something?

Almost every node can move only

```text
0

or

1
```

step.

Only

```text
1
```

node can move all the way down.

So although each Heapify Down is **at most** O(log n), **most calls finish almost immediately**.

When you add all the work together, the total is **O(n)**.

---

# Interview Memory

Don't memorize the mathematical proof.

Remember this sentence:

> **Most nodes are leaves or close to leaves, so they move very little during Heapify Down.**

That's usually enough unless you're interviewing for a very algorithm-heavy role.

---

# ⭐ Comparison

| Method              | Time       |
| ------------------- | ---------- |
| Insert each element | O(n log n) |
| Build Heap          | **O(n)** ✅ |

---

# 📝 Notes for Your Notebook

```text
BUILD HEAP

Goal:
Convert an array into a valid Heap.

Key Idea:
Leaves are already valid heaps.

Start from:
lastNonLeaf = floor(n/2) - 1

Algorithm:
Loop from last non-leaf to root.
Perform Heapify Down at every node.

Time:
O(n)

Why?
Most nodes are leaves or near leaves, so Heapify Down does very little work.
```

---

## 🎯 Quick Check (No Coding)

Array:

```text
[10, 40, 30, 5, 20]
```

1. What is the **last non-leaf index**?
2. Which indices will you call `heapifyDown()` on?
3. Why do we **never** call `heapifyDown()` on the leaf nodes?
---

## Q1. Last non-leaf index?

Array:

```text
[10,40,30,5,20]
```

Length = 5

Formula:

```text
floor(5/2)-1

=2-1

=1
```

✅ Correct.

---

## Q2. Which indices will Heapify Down?

Start from

```text
lastNonLeaf
```

↓

```text
1

↓

0
```

✅ Correct.

---

## Q3. Why don't we Heapify leaf nodes?

You answered:

> because there is no level after that, end nodes

✅ Exactly right.

A slightly more interview-oriented answer is:

> **Leaf nodes already satisfy the Heap property because they have no children to compare with. Therefore, Heapify Down on a leaf would do nothing.**

Remember the Heap property:

```text
Parent >= Children   (Max Heap)

or

Parent <= Children   (Min Heap)
```

A leaf has **no children**, so it is **already a valid heap of size 1**.

---

# ⭐ A Beautiful Observation

Notice something...

### Heapify Up

```text
Start

↓

Bottom

↓

Go Up
```

---

### Heapify Down

```text
Start

↓

Top

↓

Go Down
```

---

### Build Heap

```text
Start

↓

Last Non-Leaf

↓

Go Backwards

↓

Heapify Down
```

See the pattern?

```text
Insert

Bottom → Top

----------------

Remove

Top → Bottom

----------------

Build Heap

Bottom Internal Nodes → Top
```

Everything is beautifully symmetrical.

---

# 🎉 Congratulations!

At this point, you've learned **almost all of Heap internals**.

You now understand:

* ✅ Complete Binary Tree
* ✅ Array Representation
* ✅ Parent / Child formulas
* ✅ Heapify Up
* ✅ Heapify Down
* ✅ Build Heap (O(n))

This is more than enough to implement a Heap from scratch in an interview.

---

# Remaining Topics

Only two are left:

### Part 2.7 — Heap Sort ⭐⭐⭐⭐⭐

This is one of the coolest sorting algorithms because it uses **Build Heap + Remove Top**.

You'll realize:

> **Heap Sort is literally just repeatedly calling `removeMax()`.**

---

### Part 2.8 — Priority Queue & Interview Templates ⭐⭐⭐⭐⭐

This is the practical part.

We'll learn:

* How to recognize Heap problems in seconds.
* Min Heap vs Max Heap decision tree.
* Generic templates for:

  * Top K Largest
  * Top K Smallest
  * K Closest
  * Merge K Lists
  * Median problems

These templates are what you'll actually use during interviews.

---
If you can answer these three, you've understood Build Heap conceptually before we move on to **Heap Sort** and **Priority Queue**.

