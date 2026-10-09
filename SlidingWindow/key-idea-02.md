contiguous is a clue to investigate sliding window or prefix sum, not proof that either one must be used. A monotonic deque is often an optimization inside a sliding-window problem, rather than a completely separate alternative.

## 1. How to choose the pattern for contiguous subarray problems

Problem mentions contiguous subarray / subarray / window

Treat this as a clue, not a final decision.

Question 1: Is the window size fixed?

* Yes: Try fixed-size sliding window.

* No: Investigate variable-size sliding window or prefix sum.

Question 2: Can you safely expand and shrink the window?

* Yes: Sliding window is a strong candidate. Positive numbers often provide the predictable behavior needed for sum constraints.

* No: If negative numbers can break that behavior, consider prefix sum + HashMap or a monotonic deque, depending on the requirement.

Question 3: What exactly must you find?

* Count subarrays with a target sum → Prefix sum + frequency HashMap is a strong candidate.

* Find the longest subarray with a target sum → Prefix sum + earliest-index HashMap.

* Find a minimum-length subarray with a sum constraint when negatives are allowed → Prefix sum + monotonic deque may be appropriate.

* Find maximum/minimum in every fixed-size window → Monotonic deque.

## 2. Examples from the problems we've solved

| Problem requirement                                                               | Good starting pattern                        | Why                                                                                   |
| --------------------------------------------------------------------------------- | -------------------------------------------- | ------------------------------------------------------------------------------------- |
| Maximum sum of a subarray of size `k`                                             | Fixed-size sliding window                    | Add the incoming value and remove the outgoing value.                                 |
| Longest subarray with at most `k` distinct values                                 | Variable-size sliding window + frequency map | Shrink until the distinct-value constraint is satisfied.                              |
| Count subarrays whose sum equals `k`                                              | Prefix sum + frequency map                   | Works even when negative numbers are present.                                         |
| Longest subarray whose sum equals `k`                                             | Prefix sum + earliest-index map              | The earliest matching prefix gives the longest length.                                |
| Maximum element in every window of size `k`                                       | Sliding window + monotonic deque             | The deque maintains candidates for the maximum.                                       |
| Minimum length subarray with sum at least a target, with negative numbers allowed | Prefix sum + monotonic deque                 | Ordinary sliding-window expansion and shrinking is not reliable with negative values. |

## 3. The most important distinction: when does sliding window fail?

Consider this problem:

Find the shortest subarray with sum at least `3`.

```
nums = [2, -1, 2]
```

The total sum is `3`, so the entire array is valid. But adding or removing a negative number can move the sum in an unexpected direction.

For example, removing `2` from the left changes the sum from `3` to `1`. Removing `-1`, on the other hand, would increase the sum.

That's why the usual sliding-window reasoning—expand to increase the sum, shrink to decrease it—doesn't reliably work with negative numbers.

For this kind of problem, a prefix sum + monotonic deque can be the right approach.

One important nuance: negative numbers do not automatically rule out sliding window for every problem. They rule it out when the correctness of the usual expand/shrink strategy depends on monotonic behavior that no longer holds.

## 4. Your interview decision checklist

When you see a contiguous-subarray problem, ask these questions in order:

1. What is the objective? Count, longest, shortest, maximum sum, or window maximum/minimum?

2. Is the window size fixed? If yes, consider fixed-size sliding window.

3. Are there negative numbers? If the problem involves sum constraints, check whether they invalidate the usual sliding-window logic.

4. Can the condition be expressed using prefix sums? For a target sum, consider a HashMap of frequencies or earliest indices.

5. Do I need to maintain a running maximum or minimum in a window? Consider a monotonic deque.

6. Can I prove the algorithm is correct and efficient? Don't choose a pattern solely because the word “contiguous” appears.

Your takeaway: Contiguous subarray problems should make you investigate sliding window and prefix sum first. Then use the objective, input constraints, and the behavior of the window to select the correct approach. A monotonic deque becomes especially useful when you need efficient window extrema or when combined with prefix sums for certain negative-number problems.
