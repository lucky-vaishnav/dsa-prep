## 1. What is a Heap?

A Heap is a special data structure that always keeps either:

- the **smallest** element on top (**Min Heap**)
- the **largest** element on top (**Max Heap**)

Think of it as a "smart collection" where you can always access the highest-priority element in **O(1)**.

---

## 2. When should my brain think "Heap"?

This is the most important part.

Whenever you see words like:

```
Top K
K Largest
K Smallest
Closest K
Most Frequent K
Highest Priority
Lowest Cost
Merge K Lists
Task Scheduling
```

Immediately think:

```
Maybe Heap
```

---

## 3. Recognition Table

| Problem Statement | Think |
| --- | --- |
| Top 5 salaries | Heap |
| K Closest Points | Heap |
| Top K Frequent | Heap |
| Kth Largest | Heap |
| Merge K Sorted Lists | Heap |
| Dijkstra | Heap |
| Median Stream | Heap |

---

# 4. Why use Heap?

Suppose there are

```
1 million numbers
```

Need

```
Top 10
```

Sorting

```
O(n log n)
```

Heap

```
O(n log 10)
```

Since

```
log 10
```

is tiny,

Heap is much faster.

---

# 5. Min Heap vs Max Heap

## Min Heap

Top is smallest.

```
      2
    /   \
   5     7
  / \
 8   9
```

Always

```
Top = Minimum
```

---

## Max Heap

Top is largest.

```
      9
    /   \
   6     5
  / \
 3   2
```

Always

```
Top = Maximum
```

---

# 6. Complexity

| Operation | Complexity |
| --- | --- |
| Peek | O(1) |
| Insert | O(log n) |
| Remove Top | O(log n) |

These three are all you need for interviews.

---

# 7. The Most Important Idea

Heap is **NOT** for sorting everything.

Heap is for keeping only the important elements.

Example

Need

```
Top 3 largest
```

Instead of storing

```
100000 numbers
```

Store only

```
3 numbers
```

That's why Heap is efficient.

---

# 8. Which Heap should I use?

This confuses almost everyone initially.

## Need Largest K

Example

```
Top 5 largest
```

Use

```
Min Heap
```

Why?

Keep only 5 elements.

Whenever heap size > 5,

remove the smallest.

Finally

only the 5 largest remain.

---

## Need Smallest K

Example

```
Top 5 smallest
```

Use

```
Max Heap
```

Whenever heap size exceeds k,

remove the largest.

Finally

only the smallest remain.

---

## ⭐ Memory Trick

```
Need Largest

↓

Remove Smallest

↓

Min Heap
```

```
Need Smallest

↓

Remove Largest

↓

Max Heap
```

This one rule solves 90% of Heap interview questions.

---

# 9. Generic Template

## Top K Largest

```jsx
for (const num of nums) {

    heap.insert(num);

    if (heap.size() > k) {
        heap.removeMin();
    }
}

return heap;
```

---

## Top K Smallest

```jsx
for (const num of nums) {

    heap.insert(num);

    if (heap.size() > k) {
        heap.removeMax();
    }
}

return heap;
```

---

# 10. Decision Tree

```
Need Top K?

        │
        ▼

Need Largest?

        │
      YES
        │
        ▼

Use Min Heap

-------------------------

Need Smallest?

        │
      YES
        │
        ▼

Use Max Heap
```

---

# 11. Common Interview Problems

⭐ Easy

- Kth Largest Element
- Last Stone Weight

⭐⭐ Medium

- Top K Frequent Elements
- K Closest Points
- K Closest Elements
- Sort Characters By Frequency

⭐⭐⭐ Hard

- Median From Data Stream
- Merge K Sorted Lists
- Dijkstra
- Task Scheduler

---

# 12. Things NOT to use Heap for

Don't use Heap when:

- Need every element sorted
- Need binary search
- Need prefix sums
- Need sliding window
- Need monotonic behavior

---

# 📝 Notes to Write

```
HEAP (Priority Queue)

Use When:
- Top K
- K Largest
- K Smallest
- Closest K
- Highest Priority
- Merge K Lists

Operations:
Peek -> O(1)
Insert -> O(log n)
Remove Top -> O(log n)

Recognition:
Need Top K?

Need Largest?
→ Min Heap

Need Smallest?
→ Max Heap

Key Idea:
Don't keep all elements.
Keep only K useful elements.
```

---

## 📚 Learning Plan

I suggest this sequence:

### Part 1 ✅

- Heap intuition (completed)

### Part 2

- Build a Heap from scratch in JavaScript (so you truly understand how it works internally, not just use a library)

### Part 3

- Solve **8–10 Heap interview problems** from easy to hard.

Only after Heap is solid, we'll move to **Quick Select**, because Quick Select solves many of the same "Top K" problems but with a completely different idea. Understanding Heap first will make the comparison much clearer.
