## Q — Problem

Given an integer array `nums`, find the maximum product of any non-empty contiguous subarray and return that product.

Input:

```
nums = [2, 3, -2, 4, -1]
```

Explain your reasoning using:

- Pattern / approach
- Why it works
- Brute-force approach and complexity
- Optimal data structure, if needed
- Optimal approach
- Time and space complexity

### My Answer -
Pattern / approach -kadane algorithm
Because  we can decide if need to continue with previous subarray or start with new with current element to get out result.
Brute-force - O(n*n)
Optimal data structure - not needed
Time and space complexity - O(n), O(1)

---

Your approach is on the right track. Score: 7/10.

- Pattern: Kadane’s algorithm is a good starting point, but maximum product subarray is a variation of it.
- Why it works: Correct — we track whether extending the previous subarray or starting from the current element gives a better result.
- Brute force: \\(O(n^2)\\) time is possible if you calculate each subarray’s product incrementally. A naive approach that recalculates every product can take \\(O(n^3)\\).
- Data structure: No extra data structure is required.
- Optimal complexity: \\(O(n)\\) time and \\(O(1)\\) auxiliary space.

The key difference from ordinary Kadane: negative numbers can reverse which product is best. For example, multiplying a very negative product by another negative number can create the new maximum. So we need to track both the maximum and minimum product ending at the current position.

## JavaScript solution

```javascript

function maxProduct(nums) {
    let maxEnding = nums[0];
    let minEnding = nums[0];
    let result = nums[0];

    for (let i = 1; i < nums.length; i++) {
        const current = nums[i];

        // A negative number can swap max and min roles
        if (current < 0) {
            [maxEnding, minEnding] = [minEnding, maxEnding];
        }

        maxEnding = Math.max(current, maxEnding * current);
        minEnding = Math.min(current, minEnding * current);

        result = Math.max(result, maxEnding);
    }

    return result;
}

console.log(maxProduct([2, 3, -2, 4, -1])); // 6

```

## Dry run

| Number | Maximum product ending here | Minimum product ending here | Overall maximum |
| ------ | --------------------------- | --------------------------- | --------------- |
| 2      | 2                           | 2                           | 2               |
| 3      | 6                           | 3                           | 6               |
| -2     | -6                          | -12                         | 6               |
| 4      | 4                           | -48                         | 6               |
| -1     | 48                          | -4                          | 48              |

The answer is 48, from the subarray `[2, 3, -2, 4, -1]`? Let's verify: its product is \\(2 \times 3 \times (-2) \times 4 \times (-1) = 48\\), so the maximum product is indeed 48.

### Interview takeaway

For ordinary maximum-sum Kadane, you track the best sum ending at the current index. For maximum product, track both maximum and minimum products, because a negative number can turn the minimum into the maximum.

Complexity: \\(O(n)\\) time and \\(O(1)\\) auxiliary space.
