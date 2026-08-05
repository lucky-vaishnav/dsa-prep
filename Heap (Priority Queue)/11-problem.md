## Problem: Kth Largest Element in an Array (LeetCode 215)

```text
nums = [3,2,1,5,6,4]
k = 2

Output:
5
```

Tell me:

* Pattern
* Why
* Brute Force Complexity
* Optimal Data Structure
* Optimal Approach
* Time Complexity
* Space Complexity

💡 **Hint:** Use the discussion we had yesterday about **Top K Largest → Min Heap of size K**. Think about **why** we remove the smallest candidate and how the heap size is maintained.

Once you answer both, we'll review them together and then move on to the code.

**My Answer**-
So for question number two, new topic, heap, kth largest element in array. So as we learn, we can use here that heap sorting. And as we are talking about the largest element, we can use a min heap, and we can keep track of two minimum elements. And then we can, after maintaining the heap by using heapify down, whenever a new element comes, we can maintain top two elements. And then we can return the second largest element from that heap. So the time complexity will be O of N log N, and space complexity will be O of maybe 2. So in short, O of 1. And for brute force complexity, it will be O of N square. And yeah, after that, also share the code for the best approach and possible approaches as well, like brute force, or if there is any other approach which can be used. Like, maybe the time complexity will be higher, but the second approach we can use, that also I need to understand.

I'd give this **8.5/10**.

---

# Verification

## Pattern

✅ Heap

More specifically:

```text
Min Heap of size K
```

Perfect.

---

## Why?

✅ Correct.

We keep only the **K largest candidates**.

Whenever a better number comes, we remove the weakest candidate (smallest).

---

## One correction

You said:

> keep track of two minimum elements

Not exactly.

It should be:

> **Keep track of the K largest elements using a Min Heap.**

For this example,

```text
k = 2
```

the heap contains

```text
2 Largest Elements
```

NOT

```text
2 Minimum Elements
```

Those are very different.

---

## Heap Size

For

```text
k = 2
```

Heap size is always

```text
2
```

For

```text
k = 5
```

Heap size is always

```text
5
```

---

## Time Complexity

You answered

```text
O(n log n)
```

❌

It is

```text
O(n log k)
```

Why?

Because heap size is only

```text
k
```

not

```text
n
```

This is the biggest advantage.

---

## Space

You answered

```text
O(1)
```

❌

Heap stores

```text
k
```

elements.

Therefore

```text
O(k)
```

---

## Brute Force

You answered

```text
O(n²)
```

❌

Brute force is simply

```text
Sort
```

Complexity

```text
O(n log n)
```

There isn't really an `O(n²)` brute-force solution people use for this problem.

---

# Approaches

---

## Approach 1 — Sorting

Time

```text
O(n log n)
```

Space

```text
O(1)
```

(Simple and acceptable unless the interviewer asks for better.)

---

## Approach 2 — Min Heap ⭐⭐⭐⭐

Time

```text
O(n log k)
```

Space

```text
O(k)
```

This is the solution we've learned.

---

## Approach 3 — Max Heap

Time

```text
Build Heap : O(n)

Pop k-1 : O(k log n)

Total : O(n + k log n)
```

Space

```text
O(n)
```

Not preferred.

---

## Approach 4 — Quick Select ⭐⭐⭐⭐⭐

Average

```text
O(n)
```

Worst

```text
O(n²)
```

We'll learn after Quick Sort.

---

# Code

## Sorting

```javascript
function findKthLargest(nums, k) {
    nums.sort((a, b) => b - a);
    return nums[k - 1];
}
```

---

## Min Heap (Best so far)

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

function findKthLargest(nums, k) {

    const heap = new MinHeap();

    for (const num of nums) {

        heap.push(num);

        if (heap.size() > k) {
            heap.pop();
        }
    }

    return heap.peek();
}
```

---

## ⭐ One note for your notebook

For Heap problems, always ask yourself:

> **"What exactly should my heap contain?"**

For this problem:

```
Heap contains:
Top K Largest Elements
```

For another problem like **K Closest Points to Origin**, the heap contains:

```
Heap contains:
K Closest Points
```

For **Merge K Sorted Lists**, the heap contains:

```
Heap contains:
Current smallest node from each list
```

The question **"What does my heap store?"** is one of the most important questions to ask when solving Heap problems. It helps you identify the right Heap strategy quickly.


