Awesome! 😄 Now comes the most satisfying part.

You'll see that **Heap Sort is not a new algorithm**.

It is simply using the operations you've already learned:

* ✅ Build Heap
* ✅ Remove Max (Heapify Down)

That's it.

---

# Part 2.7 - Heap Sort

## First Question

Suppose I give you

```text
[40,20,90,10,30,80,70]
```

Need to sort in ascending order.

How would you use Heap?

---

## Your First Thought

Since Max Heap always keeps

```text
Largest Element
```

at the top,

why not repeatedly remove it?

Like this

```text
Heap

↓

Remove Max

↓

Store it

↓

Repeat
```

Exactly!

That's Heap Sort.

---

# Step 1

Original Array

```text
[40,20,90,10,30,80,70]
```

---

## Build Max Heap

We already know this.

Result

```text
[90,30,80,10,20,40,70]
```

(Tree shape doesn't matter here, only that it's a valid Max Heap.)

---

Now the maximum is already at the root.

---

# Step 2

Remove Max

```text
90
```

Store it.

Remaining Heap

```text
[80,30,70,10,20,40]
```

Sorted Part

```text
[90]
```

---

Remove again

```text
80
```

Remaining Heap

```text
[70,30,40,10,20]
```

Sorted

```text
[90,80]
```

---

Remove again

```text
70
```

Sorted

```text
[90,80,70]
```

Continue...

Finally

```text
[90,80,70,40,30,20,10]
```

---

Reverse it

```text
[10,20,30,40,70,80,90]
```

Ascending.

Works perfectly.

---

# But...

There is an even smarter way.

We don't create another array.

We sort **inside the same array**.

This is the Heap Sort used in interviews.

---

# ⭐ Key Observation

Suppose Heap is

```text
[90,70,85,40,30,20,60]
```

Largest

```text
90
```

already belongs at the **last index** of the sorted array.

So instead of storing it separately,

swap it with the last element.

---

Current

```text
[90,70,85,40,30,20,60]
```

Swap

```text
90

↔

60
```

Result

```text
[60,70,85,40,30,20,90]
```

Notice

```text
90
```

is now in its final sorted position.

We never touch it again.

---

# Heap Size Shrinks

Now ignore

```text
90
```

Heap becomes

```text
[60,70,85,40,30,20]
```

Heapify Down

Result

```text
[85,70,60,40,30,20]
```

Whole array

```text
[85,70,60,40,30,20,90]
```

Again

Swap

```text
85

↔

20
```

```text
[20,70,60,40,30,85,90]
```

Ignore last two elements.

Heapify Down

Repeat.

---

Eventually

```text
[10,20,30,40,60,70,85,90]
```

Sorted.

---

# ⭐⭐⭐ The Algorithm

```text
Build Max Heap

↓

Swap Root

↓

Last Element

↓

Reduce Heap Size

↓

Heapify Down

↓

Repeat
```

That's Heap Sort.

---

# Code

```javascript
function heapSort(nums) {

    buildHeap(nums);

    for (let end = nums.length - 1; end > 0; end--) {

        [nums[0], nums[end]] =
            [nums[end], nums[0]];

        heapifyDown(nums, 0, end);
    }

    return nums;
}

function buildHeap(nums) {

    const lastNonLeaf =
        Math.floor(nums.length / 2) - 1;

    for (let i = lastNonLeaf; i >= 0; i--) {
        heapifyDown(nums, i, nums.length);
    }
}

function heapifyDown(heap, index, heapSize) {

    while (true) {

        let largest = index;

        const left = 2 * index + 1;
        const right = 2 * index + 2;

        if (
            left < heapSize &&
            heap[left] > heap[largest]
        ) {
            largest = left;
        }

        if (
            right < heapSize &&
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

# ⭐ New Thing

Notice this line

```javascript
heapifyDown(heap, 0, end);
```

Earlier

```javascript
heapifyDown(heap, 0);
```

Now

```javascript
heapSize = end
```

Why?

Because

```text
Last Part

Already Sorted
```

We must ignore it.

---

# Complexity

Build Heap

```text
O(n)
```

Heapify Down

```text
O(log n)
```

Performed

```text
n
```

times.

Total

```text
O(n log n)
```

---

# Comparison

| Algorithm  | Best       | Average    | Worst      | Extra Space |
| ---------- | ---------- | ---------- | ---------- | ----------- |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n)        |
| Quick Sort | O(n log n) | O(n log n) | O(n²)      | O(log n)    |
| Heap Sort  | O(n log n) | O(n log n) | O(n log n) | **O(1)** ✅  |

Heap Sort is one of the few comparison sorts with **guaranteed O(n log n)** time and **constant extra space**.

---

# 🎯 The Biggest Insight

Heap Sort is **not a separate algorithm**.

It's just:

```text
Build Heap

+

Remove Max

again

again

again...
```

Everything you've learned so far naturally leads to Heap Sort.

---

# 📝 Notes for Your Notebook

```text
HEAP SORT

Idea:
1. Build Max Heap.
2. Largest element is at root.
3. Swap root with last element.
4. Reduce heap size.
5. Heapify Down.
6. Repeat until one element remains.

Time:
Build Heap -> O(n)
Sorting -> O(n log n)

Overall:
O(n log n)

Space:
O(1)

Key Idea:
Heap Sort = Build Heap + Repeated Heapify Down
```

---

# 🎯 Quick Check (No Coding)

Suppose you have a Max Heap:

```text
[100,90,80,70,60,50,40]
```

After the **first iteration of Heap Sort**:

1. Which two elements are swapped?
2. Which element is now **permanently sorted**?
3. Why do we pass `heapSize = n - 1` to `heapifyDown()` instead of using the full array length?

🎉 **Excellent! 9.5/10.** You're understanding the concept instead of memorizing it.

Let's refine your third answer slightly.

---

## 1. Which two elements are swapped?

Heap:

```text
[100,90,80,70,60,50,40]
```

Swap

```text
100 ↔ 40
```

Result

```text
[40,90,80,70,60,50,100]
```

✅ Correct.

---

## 2. Which element is permanently sorted?

```text
100
```

✅ Correct.

It is now at its **final position** in the sorted array and will never move again.

---

## 3. Why do we pass `heapSize = n - 1`?

Your answer:

> because we have already swapped first element and need to ignore index which are already swapped

✅ Correct idea.

A slightly better interview answer would be:

> **Because the last element is already in its correct sorted position. We reduce the heap size so that Heapify Down works only on the unsorted portion of the array.**

That's the key.

---

# ⭐⭐⭐ One Beautiful Observation

Let's connect everything you've learned.

## Heap Operations

```text
INSERT

↓

Heapify Up

-------------------

REMOVE

↓

Heapify Down

-------------------

BUILD HEAP

↓

Heapify Down
(from last non-leaf)

-------------------

HEAP SORT

↓

Build Heap

↓

Heapify Down repeatedly
```

Notice something?

👉 **Everything revolves around Heapify Down.**

That's why understanding Heapify Down is more important than memorizing Heap Sort.

---

# 🎉 Congratulations!

You now know **how Heap works internally**.

This is much deeper than what most interview candidates know.

---

# 📍Final Section

Only one learning section is left:

# ⭐ Part 2.8 — Priority Queue & Interview Templates

This is the **most important interview section**.

Here we'll learn things like:

## 1. How to recognize a Heap problem in under 30 seconds

Example:

```text
Top K Frequent Elements

↓

Heap
```

Why?

---

## 2. Min Heap vs Max Heap

Many people get confused here.

We'll learn a simple decision rule.

---

## 3. Generic templates

Instead of memorizing 20 Heap problems, you'll learn 5 reusable templates:

* ✅ Top K Largest
* ✅ Top K Smallest
* ✅ K Closest Points
* ✅ Merge K Sorted Lists
* ✅ Find Median from Data Stream

Most Heap interview questions are just variations of these templates.

---

## 4. When NOT to use a Heap

Sometimes sorting or Quick Select is actually the better choice.

We'll compare them.

---


