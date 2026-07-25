## Problem: Top K Frequent Elements

Given an integer array `nums` and an integer `k`, return the **k most frequent elements**.

### Example 1

```
Input:
nums = [1,1,1,2,2,3]
k = 2

Output:
[1,2]
```

### Example 2

```
Input:
nums = [1]
k = 1

Output:
[1]
```

---

### Tell me:

```
Pattern:
Why:
Brute Force Complexity:
Optimal Data Structure:
Optimal Approach:
Time Complexity:
Space Complexity:
```

💡 **Hints:**

- First, think about how to count frequencies.
- Then think: how do we efficiently get the **top k** frequencies?
- There are **multiple optimal approaches**. Don't worry if you identify only one—we'll discuss the others afterward.

### My Answer-

So for question number two, about top k frequent elements. So as you said, there can be multiple approaches. And the main thing about this problem is that after we calculate the frequency of elements, how we can get that top k elements from that calculated counts. That is where we can optimize more. So according to that, we can have multiple solutions. For now, I am saying that we can use a hashmap for counting those elements. And brute force complexity will be O of n square, and optimal data structure will be hashmap. And also the time complexity will be O of n. Space complexity will be O of n. There can be an extra for loop required to get top k element. Or what we can do is that we can take a set as well. This set will have the same number of element, which is the size of the input element. And we will store the counts of those elements according to the index. So the highest count will be, so it will be at the backside of the array. And by doing this, we can fetch top k frequent element by looping it out from the backside. And whatever the elements which are not filled with the count for this set, we will set it to zero by default. So this can be approach to use. Or otherwise, we need an extra for loop to just get that top k frequent element, maximum frequent element.

Very good.

What I like is that you recognized the **real challenge** of this problem.

> **Counting frequencies is easy. The difficult part is getting the Top K efficiently.**
> 

That is exactly what interviewers expect you to recognize.

---

# Review

## Pattern

You wrote:

> HashMap
> 

✅ Partially correct.

Actually this problem has **multiple patterns**.

- HashMap + Sorting
- HashMap + Bucket Sort ✅ (Best O(n))
- HashMap + Min Heap
- HashMap + Quick Select (Advanced)

So HashMap is only the first step.

---

## Why

You said:

> First count frequencies, then optimize getting top k.
> 

✅ Perfect.

---

## Brute Force

```
O(n²)
```

🟡 Acceptable.

---

## HashMap

```
O(n)
```

✅ Correct for counting.

---

## The second approach you described

This part:

> create an array of size n and store elements according to their frequency
> 

🎉 **Excellent!**

You have almost discovered **Bucket Sort** yourself.

The only correction is:

It is **not a Set**.

It is an **Array of Arrays**.

Example:

```
nums = [1,1,1,2,2,3]
```

Frequency Map

```
1 -> 3
2 -> 2
3 -> 1
```

Bucket

```
Index(Frequency)

0 -> []
1 -> [3]
2 -> [2]
3 -> [1]
4 -> []
5 -> []
6 -> []
```

Then traverse from back:

```
6
5
4
3  ← frequency 3
2  ← frequency 2
1
```

Answer:

```
[1,2]
```

This is called **Bucket Sort**.

So your idea was **correct**, only the data structure name was slightly off.

---

# Final Notes

```
Pattern:
HashMap + Bucket Sort

Why:
Need frequencies first, then efficiently retrieve top k.

Brute Force:
O(n²)

Optimal Data Structure:
HashMap + Bucket Array

Optimal Approach:
1. Count frequencies using HashMap.
2. Put numbers into buckets based on frequency.
3. Traverse buckets from highest frequency to lowest until k elements are collected.

Time Complexity:
O(n)

Space Complexity:
O(n)
```

---

## ⭐ Multiple Solutions

| Approach | Time | Space |
| --- | --- | --- |
| HashMap + Sorting | O(n log n) | O(n) |
| HashMap + Bucket Sort | **O(n)** ✅ | O(n) |
| HashMap + Min Heap | O(n log k) | O(n) |
| HashMap + Quick Select | Average O(n) | O(n) |

---

## What I liked most

You said:

> "The main thing is not counting. The main thing is how to get the top k."
> 

👏 That is exactly the right way to think.

In interviews, many candidates stop after building the HashMap. The interviewer then asks:

> "Good. Now how will you efficiently get the top k?"
> 

Recognizing that **frequency counting isn't the bottleneck** shows you're thinking beyond the first step of the solution.

I think you're now at the stage where, when you see a problem involving **frequency**, your first thoughts should be:

1. **Can I count using a HashMap?**
2. **How do I efficiently retrieve what I need from those counts?** (sorting, bucket sort, heap, etc.)

That's a strong problem-solving habit to build.

### Also this problem also may have duplicate element with same count/frequency so that why we are using array of array in bucket sort right ?

**Exactly!** 🎯 That's one of the main reasons.

Let's see why.

Suppose:

```
nums = [1,1,2,2,3,3,4]
```

Frequency map becomes:

```
1 -> 2
2 -> 2
3 -> 2
4 -> 1
```

Now build the bucket:

```
bucket[0] = []
bucket[1] = [4]
bucket[2] = [1,2,3]
bucket[3] = []
...
```

Notice this:

```
Frequency = 2

1
2
3
```

All **three numbers have the same frequency**.

If we used:

```jsx
bucket[freq] = num;
```

then we'd get:

```
bucket[2] = 1
bucket[2] = 2   // 1 lost
bucket[2] = 3   // 2 lost
```

Only the last value would remain.

That's why we use:

```jsx
bucket[freq].push(num);
```

so the bucket stores **all numbers** having that frequency.

---

### Then this loop

```jsx
for (let freq = bucket.length - 1; freq >= 0 && result.length < k; freq--) {

    for (const num of bucket[freq]) {

        result.push(num);

        if (result.length === k) {
            return result;
        }
    }
}
```

works like this:

```
bucket[5] → []
bucket[4] → []
bucket[3] → []
bucket[2] → [1,2,3]   ← highest frequency
bucket[1] → [4]
```

If `k = 2`:

```
result = []

Take 1
result = [1]

Take 2
result = [1,2]

Done
```

We stop immediately.

---

### ⭐ Another way to think about Bucket Sort

Instead of thinking:

> "For each number, what is its frequency?"
> 

Think:

> "For each frequency, which numbers belong here?"
> 

So the structure becomes:

```
Frequency 1 → [4]

Frequency 2 → [1,2,3]

Frequency 3 → []

Frequency 4 → []
```

This is why it's called a **bucket**—each bucket groups together all elements with the same frequency.

---

### 💡 Interview Tip

This is a very common pattern:

- **HashMap** → maps **element → frequency**
- **Bucket** → maps **frequency → list of elements**

You're essentially **reversing the mapping**.

```
HashMap:
Element  → Frequency

Bucket:
Frequency → Elements
```

That "reverse mapping" is the key insight behind Bucket Sort. Once you see that, the algorithm becomes much easier to derive instead of memorize.

#### Here are the **three most common approaches**.

---

### 1. HashMap + Sorting (O(n log n))

```jsx
function topKFrequent(nums, k) {

    const map = new Map();

    for (const num of nums) {
        map.set(num, (map.get(num) || 0) + 1);
    }

    return [...map.entries()]
        .sort((a, b) => b[1] - a[1])
        .slice(0, k)
        .map(entry => entry[0]);
}
```

---

### 2. HashMap + Bucket Sort (Optimal) ⭐

```jsx
function topKFrequent(nums, k) {

    const map = new Map();

    for (const num of nums) {
        map.set(num, (map.get(num) || 0) + 1);
    }

    // bucket[index] = numbers having frequency = index
    const bucket = Array(nums.length + 1)
        .fill(null)
        .map(() => []);

    for (const [num, freq] of map) {
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

---

### 3. HashMap + Min Heap (Interview Follow-up)

```jsx
// Simple implementation using sorting to simulate heap behavior.

function topKFrequent(nums, k) {

    const map = new Map();

    for (const num of nums) {
        map.set(num, (map.get(num) || 0) + 1);
    }

    const heap = [];

    for (const [num, freq] of map) {

        heap.push([num, freq]);

        heap.sort((a, b) => a[1] - b[1]);

        if (heap.length > k) {
            heap.shift();
        }
    }

    return heap.map(item => item[0]);
}
```

> **Note:** This is **not a real Min Heap**. It simulates one using sorting. In interviews, if they specifically ask for a **Min Heap**, you'll implement or use a priority queue. We'll learn that pattern later.
> 

---

### ⭐ Key Idea of Bucket Sort (Remember This)

```jsx
// Key Idea:
//
// 1. Count frequency using HashMap.
//
// Example:
// 1 -> 3
// 2 -> 2
// 3 -> 1
//
// 2. Create buckets where index = frequency.
//
// bucket[1] = [3]
// bucket[2] = [2]
// bucket[3] = [1]
//
// 3. Traverse buckets from highest frequency to lowest
//    until k elements are collected.
//
// Time: O(n)
// Space: O(n)
```

---

##
