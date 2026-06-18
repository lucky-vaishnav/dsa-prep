# Question

Given an array:

```
nums = [2,7,11,15]
target = 9
```

Return the indices of the two numbers such that they add up to target.

Output:

```
[0,1]
```

Because:

```
2 + 7 = 9
```

---

### Tell me only:

```
Pattern:
Why:
Brute Force Complexity:
Optimal Data Structure:
Optimal Approach:
Time Complexity:
Space Complexity:
```

### Answer

### Your Answer

Pattern

```
HashMap
```

✅ Correct.

---

### Why

You wrote:

```
map[target - nums[i]]
```

✅ Exactly.

That's the key insight.

If current number is:

```
7
```

and target is:

```
9
```

then we need:

```
9 - 7 = 2
```

Check if we've already seen:

```
2
```

in the map.

---

### Brute Force

You wrote:

```
O(n²)
```

✅ Correct.

---

### Optimal Data Structure

```
Map
```

✅ Correct.

---

### Optimal Approach

```
HashMap
```

✅ Correct.

---

### Complexity

```
Time O(n)
Space O(n)
```

✅ Correct.

---

## Bonus Question

Can Two Pointers solve it?

### Answer

✅ Yes

But only if the array is sorted.

Example:

```
[2,7,11,15]
target = 9
```

Already sorted.

```
left = 0
right = 3

2 + 15 = 17
```

Too large.

Move right.

```
2 + 11 = 13
```

Too large.

Move right.

```
2 + 7 = 9
```

Found.

---

### Why HashMap is preferred?

The original problem asks for:

```
indices
```

and the array may be:

```
[3,2,4]
```

If you sort it:

```
[2,3,4]
```

you lose the original indices.

That's why the standard interview solution is:

```
HashMap
```

---

# Pattern Recognition Note

Add this to your notes:

```
Two Sum

Pattern:
HashMap

Recognition Clues:
- Find pair
- Sum equals target
- Need indices
- Unsorted array

Brute Force:
O(n²)

Optimal:
HashMap

Logic:
needed = target - nums[i]

if map has needed:
    return indices

Complexity:
Time O(n)
Space O(n)
```
