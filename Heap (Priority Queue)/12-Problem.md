## Problem: Top K Frequent Elements (LeetCode 347)

```text
nums = [1,1,1,2,2,3]
k = 2

Output:
[1,2]
```

> **Important:** This time, solve it using a **Min Heap** (don't use Bucket Sort, since we've already learned that).

Tell me:

* Pattern
* Why
* Brute Force Complexity
* Optimal Data Structure
* Optimal Approach
* Time Complexity
* Space Complexity

💡 **Hint:** First count frequencies using a `Map`, then think:

> **"What should my heap store?"**

This question is excellent because it combines **HashMap + Heap**, which is one of the most common interview patterns.

# My Thoughts -
Yeah, for question, top k frequent element. So I think it is a very good question to learn what we learn, min-heap and also bucket sort as well. And I think from this problem only we explored the heap part because we do it with the bucket sort first, and then right now we are using heap. So yeah, for this problem, we can use a hashmap to count the frequency of the element, and then after we can use bucket sort or min-heap to maintain the maximum frequent element, and we can use that heapify up and heapify down to maintain that minimum heap. So just please share that both code with bucket sort and with heap for this problem, so that I can compare and learn.

Very good. I'd give your answer **9/10**. 👍

You correctly identified the **main idea**:

* ✅ Count frequencies using a `HashMap`.
* ✅ Then the optimization is **how to get the Top K elements**.
* ✅ We have learned **two approaches**:

  * Bucket Sort
  * Min Heap

That's exactly the takeaway from this problem.

---

# Approach 1 — Bucket Sort (O(n))

```javascript
function topKFrequent(nums, k) {

    const freqMap = new Map();

    for (const num of nums) {
        freqMap.set(num, (freqMap.get(num) || 0) + 1);
    }

   /*
We create nums.length + 1 buckets simply so that the frequency value can be used directly as the index, making the code clean and avoiding freq - 1 calculations.
bucket[0] will always remain empty for this problem.
No element can have a frequency of 0.
  */
    const bucket = Array(nums.length + 1)
        .fill(null)
        .map(() => []);

    for (const [num, freq] of freqMap) {
        bucket[freq].push(num);
    }

    const result = [];

    for (let freq = bucket.length - 1; freq >= 0 && result.length < k; freq--) {

        for (const num of bucket[freq]) {

            result.push(num);

            if (result.length === k) {
                return result;
            }
        }
    }

    return result;
}
```

### Complexity

```
Time : O(n)
Space: O(n)
```

---

# Approach 2 — Min Heap (O(n log k))

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

    push(node) {
        this.heap.push(node);
        this.heapifyUp();
    }

    pop() {

        if (this.heap.length === 1) {
            return this.heap.pop();
        }

        const root = this.heap[0];

        this.heap[0] = this.heap.pop();

        this.heapifyDown();

        return root;
    }

    heapifyUp() {

        let i = this.heap.length - 1;

        while (i > 0) {

            let p = Math.floor((i - 1) / 2);

            if (this.heap[p].freq <= this.heap[i].freq) break;

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
                this.heap[left].freq < this.heap[smallest].freq
            ) {
                smallest = left;
            }

            if (
                right < this.heap.length &&
                this.heap[right].freq < this.heap[smallest].freq
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

function topKFrequent(nums, k) {

    const freqMap = new Map();

    for (const num of nums) {
        freqMap.set(num, (freqMap.get(num) || 0) + 1);
    }

    const heap = new MinHeap();

    for (const [num, freq] of freqMap) {

        heap.push({ num, freq });

        if (heap.size() > k) {
            heap.pop();
        }
    }

    const result = [];

    while (heap.size()) {
        result.push(heap.pop().num);
    }

    return result.reverse();
}
```

### Complexity

```
Time : O(n log k)
Space: O(n)
```

---

# ⭐ Interview Tip

This is one of the best comparison problems you've learned so far.

| Approach     | Time             | Space | When to Use                                                      |
| ------------ | ---------------- | ----- | ---------------------------------------------------------------- |
| Sorting      | O(n log n)       | O(1)  | Simple, but slower                                               |
| Bucket Sort  | **O(n)**         | O(n)  | Best when frequencies are bounded by `n`                         |
| Min Heap     | **O(n log k)**   | O(n)  | Best when `k` is much smaller than `n`                           |
| Quick Select | **O(n)** average | O(1)  | Most optimized interview solution (we'll learn after Quick Sort) |

---

## ⭐ My recommendation

From tomorrow onward, let's start the **Binary Search pattern**. You've now covered:

* ✅ HashMap
* ✅ Two Pointers
* ✅ Sliding Window
* ✅ Monotonic Stack
* ✅ Heap
* ✅ Sorting + Greedy (introduced)

Binary Search is the next major pattern, and many interview questions build on it. After Binary Search, learning **Merge Sort + Quick Sort + Quick Select** will be much easier because they naturally connect.

# Question
So for the problem which we did that k frequency most element from an array. So it seems like bucket sort is the better one than heap sort, right? Just wanted to confirm it because bucket sort has a time of n, and heap sort have a time complexity of n log k, right? And better will be quick select, but we will run it later after binary search, as you said. But for this particular problem, we can say that bucket sort is a right approach. And when will be the right approach, the heap sort.

Yes, your understanding is correct. 👍

For **Top K Frequent Elements**:

* ✅ **Bucket Sort** is the **best solution** among the approaches we've learned so far.

  * **Time:** `O(n)`
  * **Space:** `O(n)`

* ✅ **Min Heap** is `O(n log k)`, so it is slower for this specific problem.

---

## Then when is Min Heap the better choice?

Use a **Min Heap** when:

1. **You cannot use Bucket Sort**

   * Frequencies/values are not naturally bounded by `n`.
   * Creating buckets would waste a lot of memory.

2. **The data is streaming**

   * Numbers arrive one by one.
   * You want to keep only the **Top K** at any time.
   * Bucket Sort requires seeing the entire input first.

3. **K is much smaller than N**

   * Example:

     ```text
     n = 10,000,000
     k = 10
     ```
   * A heap of size 10 is very efficient.

---

## Simple rule for interviews

* **Bucket Sort** → When frequency ranges from **1 to n** (like this problem).
* **Min Heap** → General-purpose **Top K** problems, especially when **K is small** or data arrives continuously.
* **Quick Select** → Best average time when you only need the Kth/Top K once on a static array (we'll learn it later).

So for **LeetCode 347 (Top K Frequent Elements)**:

🥇 Bucket Sort
🥈 Min Heap
🥉 Sorting

Your comparison is exactly the kind of reasoning interviewers like to hear.

