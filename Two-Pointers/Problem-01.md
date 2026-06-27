Given an array:

```
height = [1,8,6,2,5,4,8,3,7]
```

Each number represents the height of a vertical line.

Choose two lines that together with the x-axis form a container that holds the **maximum amount of water**.

Return the maximum area.

Output:

```
49
```

(Between heights `8` and `7`.)

---

Tell me:

```
Pattern:
Why:
Brute Force Complexity:
Optimal Data Structure:
Optimal Approach:
Time Complexity:
Space Complexity:
```

### Hint

Ask yourself:

```
Do I need to check every pair?

Or can I intelligently move pointers?
```

### My Response -

```jsx
Pattern: Two Pointer
Why: we can move from both end to calculate max area 
Brute Force Complexity: O(n^2)
Optimal Data Structure: tow pointer 
Optimal Approach: Two pointer 
Time Complexity: O(n) 
Space Complexity:O(1)
```

# Approach 1 (Brute Force)

```
function maxArea(height) {

let maxArea=0;

for (let i=0;i<height.length;i++) {

for (let j=i+1;j<height.length;j++) {

const width = j-i;
const minHeight= Math.min(height[i],height[j]);
const area = width*minHeight;

maxArea = Math.max(maxArea,area);
        }
    }

return maxArea;
}
```

Complexity

```
Time : O(n²)
Space: O(1)
```

---

# Approach 2 (Optimal - Two Pointers)

```
function maxArea(height) {

let left=0;
let right=height.length-1;

let maxArea=0;

while (left < right) {

const width = right-left;
const minHeight = Math.min(height[left],height[right]);

maxArea = Math.max(maxArea,width*minHeight);

if (height[left]<height[right]) {
left++;
}else {
right--;
    }
 }

return maxArea;
}

console.log(maxArea([1,8,6,2,5,4,8,3,7]));
```

Output

```
49
```

Complexity

```
Time : O(n)
Space: O(1)
```

---

# Dry Run

```
[1,8,6,2,5,4,8,3,7]
 L               R
```

Area

```
width = 8
height = 1

Area = 8
```

Move

```
left++
```

because

```
1 < 7
```

---

Now

```
[1,8,6,2,5,4,8,3,7]
    L           R
```

Area

```
width = 7
height = 7

Area = 49
```

Current maximum

```
49
```

---

Now compare

```
8 vs 7
```

Move

```
right--
```

---

Continue until

```
left == right
```

---

# The Most Important Question

Most people memorize:

```
if (height[left] < height[right])
left++;
else
right--;
```

without understanding **why**.

Let's understand it.

Suppose

```
8             7
|             |
|             |
|             |
--------------
```

Area is

```
width × minHeight

= width × 7
```

The limiting height is **7**.

If we move the **left pointer (8)**:

```
?
        7
```

Width **decreases**.

Height can be at most

```
7
```

or even smaller.

So area **cannot increase** because:

- width decreases
- limiting height doesn't improve

Therefore moving the **taller line is never useful**.

Instead, move the **shorter line**, hoping to find a taller one.

That's the entire proof behind the algorithm.

---

# Is There Any Other Better Approach?

| Approach | Time | Space |
| --- | --- | --- |
| Brute Force | O(n²) | O(1) |
| Two Pointers | O(n) | O(1) |

There is **no practical intermediate approach** like:

- HashMap ❌
- HashSet ❌
- Binary Search ❌
- Sliding Window ❌
- Prefix/Suffix ❌

The interview progression is simply:

```
Brute Force
        ↓
Two Pointers (Optimal)
```

---

# Pattern Recognition Notes

Add this to your notebook:

```
Container With Most Water

Pattern:
Two Pointers

Recognition Clues:
- Two ends
- Maximize area/distance
- Width decreases as pointers move
- Need optimal pair

Pointer Movement:
Move the pointer with the smaller height.

Reason:
The smaller height limits the area.
Moving the taller pointer cannot increase the area because the width decreases while the limiting height stays the same or becomes smaller.

Brute Force:
O(n²)

Optimal:
Two Pointers

Time:
O(n)

Space:
O(1)
```
