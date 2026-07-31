This is where Heap becomes really interesting. Up to now, we've only learned **what a Heap is**. Now we'll learn **how it maintains its property automatically**.

---

# Heap Learning Roadmap

```text
✅ 2.1 What is Heap
✅ 2.2 Complete Binary Tree
✅ 2.3 Array Representation

⭐ 2.4 Insert (Heapify Up)
⬜ 2.5 Remove Top (Heapify Down)
⬜ 2.6 Build Complete Heap Class
⬜ 2.7 Dry Run
⬜ 2.8 Interview Template
```

---

# Part 2.4 - Insert (Heapify Up)

## Goal

Suppose we have a Max Heap:

```text
        90
      /    \
    70      60
   /  \    /
 40   30  20
```

Array

```text
[90,70,60,40,30,20]
```

Now insert

```text
80
```

Where should it go?

---

## Rule 1

Always insert at the **end**.

Because Heap must remain a **Complete Binary Tree**.

Array becomes

```text
[90,70,60,40,30,20,80]
```

Tree

```text
        90
      /    \
    70      60
   /  \    /  \
 40   30  20  80
```

---

## Is this still a Max Heap?

Look at

```text
60
```

and

```text
80
```

```text
60 < 80
```

❌ Heap property is broken.

---

# Solution

Move

```text
80
```

up.

This process is called

```text
Heapify Up
```

or

```text
Bubble Up
```

---

## Step 1

Swap with parent.

```text
        90
      /    \
    70      80
   /  \    /  \
 40   30  20  60
```

Array

```text
[90,70,80,40,30,20,60]
```

---

## Check again

Parent

```text
90
```

Child

```text
80
```

Everything fine.

Done.

---

# Another Example

Insert

```text
100
```

Current

```text
[90,70,60,40,30,20]
```

Insert

```text
[90,70,60,40,30,20,100]
```

Tree

```text
        90
      /    \
    70      60
   /  \    /  \
 40   30  20 100
```

Broken.

---

Swap

```text
100
```

with

```text
60
```

```text
        90
      /    \
    70      100
   /  \    /  \
 40   30  20 60
```

Still broken.

---

Swap

```text
100
```

with

```text
90
```

```text
        100
      /     \
    70       90
   /  \     /  \
 40   30   20  60
```

Finished.

---

# The Algorithm

Suppose

```text
current = last inserted index
```

Loop

```text
while(parent < current)
```

Swap.

Continue.

---

# Parent Formula

Already learned:

```text
parent = Math.floor((i-1)/2)
```

---

# Heapify Up Template

```text
Insert at end

↓

Find Parent

↓

Is parent smaller?

↓

YES

↓

Swap

↓

Continue

↓

NO

↓

Stop
```

---

# Code

```javascript
heapifyUp() {

    let index = this.heap.length - 1;

    while (index > 0) {

        const parent = Math.floor((index - 1) / 2);

        if (this.heap[parent] >= this.heap[index]) {
            break;
        }

        [this.heap[parent], this.heap[index]] =
            [this.heap[index], this.heap[parent]];

        index = parent;
    }
}
```

---

# Insert Function

```javascript
insert(value) {

    this.heap.push(value);

    this.heapifyUp();
}
```

That's it.

Insert is literally:

```text
Push

↓

Bubble Up
```

---

# Complete Max Heap (Only Insert)

```javascript
class MaxHeap {

    constructor() {
        this.heap = [];
    }

    insert(value) {

        this.heap.push(value);

        this.heapifyUp();
    }

    heapifyUp() {

        let index = this.heap.length - 1;

        while (index > 0) {

            const parent = Math.floor((index - 1) / 2);

            if (this.heap[parent] >= this.heap[index]) {
                break;
            }

            [this.heap[parent], this.heap[index]] =
                [this.heap[index], this.heap[parent]];

            index = parent;
        }
    }
}

const heap = new MaxHeap();

heap.insert(90);
heap.insert(70);
heap.insert(60);
heap.insert(100);

console.log(heap.heap);
```

Output

```text
[100,90,60,70]
```

---

# Complexity

| Operation | Complexity |
| --------- | ---------- |
| Insert    | O(log n)   |

Why?

Because in the worst case, the element travels from the **last level to the root**.

A complete binary tree has height:

```text
log₂(n)
```

So Heapify Up takes **O(log n)**.

---

# ⭐ Recognition

Whenever you insert into a Heap:

```text
Insert

↓

Last Position

↓

Heapify Up

↓

Done
```

No exceptions.

---

# 📝 Notes for Your Notebook

```text
HEAPIFY UP (Bubble Up)

Purpose:
Restore Heap after insertion.

Steps:
1. Insert at last index.
2. Find parent.
3. Compare parent and child.
4. If Heap property breaks, swap.
5. Continue until root or property is restored.

Parent:
floor((i-1)/2)

Time:
O(log n)

Insert = Push + Heapify Up
```

---

# 🎯 Small Exercise (Don't Code)

Before we move to **Heapify Down**, answer this mentally:

Starting Heap:

```text
[90,70,85,40,30,20,60]
```

Now insert:

```text
100
```

👉 **Question:**

1. What will be the array **immediately after `push(85)`**?
2. After **Heapify Up**, what is the final heap array?

If you can answer this without drawing the tree, you've understood Heapify Up. Then we'll move to **Part 2.5 - Remove Top (Heapify Down)**, which is the second half of every Heap implementation.

My Answer:

```text
100,90,85,70,30,20,60,40
```

🎯 **100% Correct!** Excellent.

Let's verify it.

---

## Initial Heap

```text
[90,70,85,40,30,20,60]
```

Tree

```text
        90
      /    \
    70      85
   /  \    /  \
 40   30  20  60
```

---

## Step 1 - Push 100

```text
[90,70,85,40,30,20,60,100]
```

Tree

```text
        90
      /    \
    70      85
   /  \    /  \
 40   30  20  60
 /
100
```

Current index = **7**

Parent

```text
floor((7-1)/2)

=3
```

Parent value = **40**

Swap

```text
[90,70,85,100,30,20,60,40]
```

---

Current index = **3**

Parent

```text
floor((3-1)/2)

=1
```

Parent value = **70**

Swap

```text
[90,100,85,70,30,20,60,40]
```

---

Current index = **1**

Parent

```text
floor((1-1)/2)

=0
```

Parent value = **90**

Swap

```text
[100,90,85,70,30,20,60,40]
```

Now root reached.

Done.

✅ Final Heap

```text
[100,90,85,70,30,20,60,40]
```

Exactly what you answered.

---

# 🎉 This tells me you've understood Heapify Up.

Earlier, you were visualizing the tree. Now you're thinking directly in terms of **array indices**, which is how experienced developers implement heaps.

---

# One Small Interview Observation

Notice something interesting.

During Heapify Up, **we never cared about the entire tree**.

We only repeatedly did:

```text
Current Index

↓

Find Parent

↓

Compare

↓

Swap

↓

Repeat
```

That's the entire algorithm.

---

# ⭐ Heapify Up Summary

```text
Insert

↓

Push at last index

↓

Parent = floor((i-1)/2)

↓

Parent smaller?

↓

Swap

↓

Continue

↓

Stop at root or when property is restored
```

You should now be able to write **Heapify Up** from memory.

---

# 🚀 Next: Part 2.5 — Remove Top (Heapify Down)

This is the second half of Heap and, in my opinion, the trickier one.

You'll learn:

* Why we replace the root with the last element.
* Why we compare with **both** children.
* Why we swap with the **larger child** in a Max Heap.
* Why Heapify Down is also **O(log n)**.

Once you understand Heapify Down, you'll know **90% of Heap internals**. The remaining parts are just combining these two operations.

