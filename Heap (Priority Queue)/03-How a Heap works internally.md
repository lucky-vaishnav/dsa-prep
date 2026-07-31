This is the most important Heap operation. In interviews, **Heapify Down** is actually used more often than Heapify Up because many problems involve repeatedly removing the top element.

---

# Part 2.5 - Remove Top (Heapify Down)

## Goal

Suppose we have a Max Heap:

```text
        100
      /      \
    90        85
   /  \      /  \
 70   30   20   60
 /
40
```

Array

```text
[100,90,85,70,30,20,60,40]
```

Suppose someone asks:

> Remove the maximum.

Since this is a Max Heap,

the maximum is always

```text
100
```

---

# Question

Can we simply delete it?

If we delete the root,

we get

```text
        X
      /   \
    90     85
```

Now the tree is **not complete**.

❌ Invalid Heap.

---

# ⭐ Heap Rule #2

Never leave a gap.

Instead,

take the **last element**

and move it to the root.

---

## Step 1

Remove

```text
100
```

Take last element

```text
40
```

Move it to root.

Tree becomes

```text
        40
      /      \
    90        85
   /  \      /  \
 70   30   20   60
```

Array

```text
[40,90,85,70,30,20,60]
```

Tree is complete again.

But...

---

# Heap Property Broken

Root

```text
40
```

Children

```text
90

85
```

Clearly

```text
40
```

cannot stay there.

---

# Solution

Move

```text
40
```

down.

This process is called

```text
Heapify Down
```

or

```text
Bubble Down
```

---

# ⭐ Important Question

Which child should we swap with?

Current

```text
40
```

Children

```text
90

85
```

Swap with

```text
90
```

or

```text
85
```

---

Answer:

Always swap with the

```text
LARGER CHILD
```

Why?

Because after swapping,

the parent should still be larger than **both** children.

---

## Step 2

Swap

```text
40
```

with

```text
90
```

Tree

```text
        90
      /      \
    40        85
   /  \      /  \
 70   30   20   60
```

Array

```text
[90,40,85,70,30,20,60]
```

Still broken.

---

Current

```text
40
```

Children

```text
70

30
```

Largest child

```text
70
```

Swap.

Tree

```text
        90
      /      \
    70        85
   /  \      /  \
 40   30   20   60
```

Array

```text
[90,70,85,40,30,20,60]
```

Now

```text
40
```

has no children.

Done.

---

# ⭐ The Algorithm

Current index

```text
0
```

Loop

```text
Find Left Child

Find Right Child

Find Larger Child

Swap

Continue
```

---

# Child Formula

Already learned.

Left

```text
2*i+1
```

Right

```text
2*i+2
```

---

# Heapify Down Template

```text
Root

↓

Find Left Child

↓

Find Right Child

↓

Which child is larger?

↓

Swap

↓

Continue
```

---

# Code

```javascript
heapifyDown() {

    let index = 0;

    while (true) {

        let largest = index;

        const left = 2 * index + 1;
        const right = 2 * index + 2;

        if (
            left < this.heap.length &&
            this.heap[left] > this.heap[largest]
        ) {
            largest = left;
        }

        if (
            right < this.heap.length &&
            this.heap[right] > this.heap[largest]
        ) {
            largest = right;
        }

        if (largest === index) {
            break;
        }

        [this.heap[index], this.heap[largest]] =
            [this.heap[largest], this.heap[index]];

        index = largest;
    }
}
```

---

# Remove Function

```javascript
removeMax() {

    if (this.heap.length === 0) return null;

    if (this.heap.length === 1) {
        return this.heap.pop();
    }

    const max = this.heap[0];

    this.heap[0] = this.heap.pop();

    this.heapifyDown();

    return max;
}
```

Notice how small it is.

```text
Save root

↓

Move last element to root

↓

Heapify Down

↓

Return old root
```

That's the entire removal algorithm.

---

# Complete Class (Insert + Remove)

```javascript
class MaxHeap {

    constructor() {
        this.heap = [];
    }

    insert(value) {
        this.heap.push(value);
        this.heapifyUp();
    }

    removeMax() {

        if (this.heap.length === 0) return null;

        if (this.heap.length === 1) {
            return this.heap.pop();
        }

        const max = this.heap[0];

        this.heap[0] = this.heap.pop();

        this.heapifyDown();

        return max;
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

    heapifyDown() {

        let index = 0;

        while (true) {

            let largest = index;

            const left = 2 * index + 1;
            const right = 2 * index + 2;

            if (
                left < this.heap.length &&
                this.heap[left] > this.heap[largest]
            ) {
                largest = left;
            }

            if (
                right < this.heap.length &&
                this.heap[right] > this.heap[largest]
            ) {
                largest = right;
            }

            if (largest === index) break;

            [this.heap[index], this.heap[largest]] =
                [this.heap[largest], this.heap[index]];

            index = largest;
        }
    }
}
```

---

# Complexity

| Operation  | Time         |
| ---------- | ------------ |
| Remove Top | **O(log n)** |

Again, because the element moves at most one path from the root to a leaf.

---

# ⭐ Memory Trick

## Insert

```text
Push

↓

Heapify Up
```

---

## Remove

```text
Take Root

↓

Move Last to Root

↓

Heapify Down
```

These are the **only two operations** that modify a Heap.

---

# 📝 Notes for Your Notebook

```text
HEAPIFY DOWN (Bubble Down)

Purpose:
Restore Heap after removing the root.

Steps:
1. Save root.
2. Move last element to root.
3. Compare with both children.
4. Swap with the larger child (Max Heap).
5. Continue until Heap property is restored.

Left Child:
2*i + 1

Right Child:
2*i + 2

Time:
O(log n)

Remove = Save Root + Move Last to Root + Heapify Down
```

---

## 🎯 Your Turn (No Coding)

Start with this Max Heap:

```text
[100,90,85,70,30,20,60,40]
```

Perform **one `removeMax()`**.

Tell me:

1. What is the array **immediately after moving the last element to the root**?
2. After **Heapify Down**, what is the final heap array?

If you get this right, you've understood both core Heap operations, and the remaining sections (building the heap, heap sort intuition, and interview templates) will be much easier.

My Answer:
```text
1. [40,90,85,70,30,20,60]
2. 90,70,85,40,30,20,60
```
🎉 **Perfect! 10/10.**

You got **both answers exactly right.**

---

## Initial Heap

```text
[100,90,85,70,30,20,60,40]
```

---

## Step 1 — Save Root

Removed value

```text
100
```

---

## Step 2 — Move Last to Root

Move

```text
40
```

to root.

Array

```text
[40,90,85,70,30,20,60]
```

✅ Your answer was correct.

---

## Step 3 — Heapify Down

Current

```text
40
```

Children

```text
90

85
```

Largest child

```text
90
```

Swap

```text
[90,40,85,70,30,20,60]
```

---

Current

```text
40
```

Children

```text
70

30
```

Largest

```text
70
```

Swap

```text
[90,70,85,40,30,20,60]
```

Now

```text
40
```

has no children.

Done.

✅ Your final answer is correct.

---

# 🎉 Congratulations!

You now understand the **two core Heap algorithms**.

Everything else in Heap is built on these two.

```text
INSERT

Push

↓

Heapify Up

------------------------

REMOVE

Move Last to Root

↓

Heapify Down
```

That's almost the entire implementation.

---

# ⭐ One Important Observation

Notice something:

### Heapify Up

We compare with

```text
Parent
```

only.

---

### Heapify Down

We compare with

```text
Left Child

Right Child
```

both.

This difference confuses many beginners.

### Why?

Because during insertion,

only the **new element** can violate the Heap property with **its parent**.

During removal,

the **root** can violate the Heap property with **either child**.

That's why Heapify Down always checks both children.

---

# ⭐ The Biggest Interview Insight

You don't actually need to memorize Heapify Up or Down.

Just remember:

## Insert

```text
New element

↓

Can only move UP

↓

Compare Parent
```

---

## Remove

```text
Root replaced

↓

Can only move DOWN

↓

Compare Children
```

That's enough to derive both algorithms during an interview.

---

# 📚 Where are we now?

```text
✅ 2.1 What is Heap
✅ 2.2 Complete Binary Tree
✅ 2.3 Array Representation
✅ 2.4 Heapify Up
✅ 2.5 Heapify Down
⬜ 2.6 Build Heap (from an array)
⬜ 2.7 Heap Sort intuition
⬜ 2.8 Priority Queue & Interview Template
```

---

## Next

In the next session, I'd like to cover **Part 2.6: Build Heap (Heapify an entire array)**.

This is a famous interview question because most people think:

> "To build a heap, I'll insert every element."

That works in **O(n log n)**.

But there is a **surprising O(n) algorithm** called **Build Heap (Heapify)**.

It's one of the most beautiful algorithms in data structures, and I think you'll enjoy understanding *why* it's **O(n)** instead of **O(n log n)**. After that, Heap will be completely mastered.
