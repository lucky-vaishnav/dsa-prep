**Search a 2D Matrix II** — LeetCode 240

```text
matrix = [
  [1,  4,  7, 11, 15],
  [2,  5,  8, 12, 19],
  [3,  6,  9, 16, 22],
  [10,13,14,17,24],
  [18,21,23,26,30]
]

target = 5

Output = true
```

Important difference from the **Search a 2D Matrix** problem we did earlier:

* Every row is sorted left → right.
* Every column is sorted top → bottom.
* But the entire matrix **cannot simply be treated as one sorted array**.

Think about:

* Pattern/approach
* Why?
* Brute force
* Optimal approach
* Time & space complexity

**Hint:** There is a very useful trick involving starting from a **corner** of the matrix.

---
### My Thought-
the brute force complexity will be O of n log d, where d is the size of the sub-array. Yeah, and better approach will be binary search. For that, we will use two binary search. So right now my thought or the approach is not the best optimal approach. But what I can think of is that we will perform binary search on this matrix, then we will find the mid, and left and the right. And then we will compare that mid sub-array first element with the target. If it is greater than the first element, then we will also check for the next sub-array in the matrix, which is also greater than the target. So we will minimize the scope which sub-array to traverse. So let's say for target 5, there are two arrays which target. First is the index 1 and index 2. Then perform two binary search on this.

---
You're thinking in the right direction about **using the sorted properties**, but for this particular problem, your proposed approach is more complicated than necessary.

Also, one correction: this matrix is **not** sorted in a way that lets us binary-search the rows and then binary-search selected rows reliably.

### The better insight

For:

```text
1   4   7   11  15
2   5   8   12  19
3   6   9   16  22
10  13  14  17  24
18  21  23  26  30
```

Start from the **top-right corner**:

```text
                    ↓
1   4   7   11  [15]
2   5   8   12   19
3   6   9   16   22
10  13  14  17   24
18  21  23  26   30
```

For target `5`:

* `15 > 5` → move **left**
* `11 > 5` → move **left**
* `7 > 5` → move **left**
* `4 < 5` → move **down**
* `5 === 5` → found ✅

### Why this works

At the **top-right corner**:

* If current > target → everything **below** current is even larger, so eliminate the **column**.
* If current < target → everything **to the left** is smaller, so eliminate the **row**.

So each step eliminates an entire row or column.

### Complexity

```text
Time  = O(m + n)
Space = O(1)
```

So your binary-search idea isn't the best approach for **Search a 2D Matrix II**.

### Important distinction from our previous 2D problem

**Search a 2D Matrix:**

```text
Entire matrix behaves like one sorted array
→ Binary Search
→ O(log(m × n))
```

**Search a 2D Matrix II:**

```text
Rows sorted
Columns sorted
But not globally sorted
→ Top-right / bottom-left traversal
→ O(m + n)
```

This is a useful pattern to add to your notes:

> **Matrix with rows + columns sorted → start from a corner and eliminate one row/column at every step.**

So for **Search a 2D Matrix II**, there isn't a specific named pattern like Binary Search or Sliding Window.

It's mainly a **matrix traversal / elimination logic** problem:

* Start from a useful corner.
* Compare current value with target.
* Eliminate an entire row or column.
* Continue until found or out of bounds.

### Code

```javascript
function searchMatrix(matrix, target) {

    if (!matrix.length || !matrix[0].length) {
        return false;
    }

    let row = 0;
    let col = matrix[0].length - 1;

    while (row < matrix.length && col >= 0) {

        const current = matrix[row][col];

        if (current === target) {
            return true;
        }

        if (current > target) {
            // Current is too large → eliminate this column
            col--;
        } else {
            // Current is too small → eliminate this row
            row++;
        }
    }

    return false;
}
```

**Complexity:**

```text
Time  = O(m + n)
Space = O(1)
```

So for your notes:

> **Rows sorted + columns sorted → corner traversal/elimination. No special algorithm required; derive the direction from the ordering properties.**

