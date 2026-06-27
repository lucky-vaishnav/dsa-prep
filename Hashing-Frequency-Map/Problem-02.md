Given an array:

```
nums = [3,4,-1,1]
```

Find the **smallest missing positive integer**.

Output:

```
2
```

Because:

```
1 exists
2 is missing
```

Another example:

```
nums = [1,2,0]
```

Output:

```
3
```

---

Tell me only:

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
Do I really need sorting?

Or do I just need to know whether a number exists?
```

### My Response -

> Pattern: HashSet  
Why: we can useif element exists logic 
Brute Force Complexity: o(n^2) 
Optimal Data Structure: HashSet 
Optimal Approach: Create a new set from input array and traverse it, if current element -1 exists then samallest will current element+1 else current element-1, aslo store finalResult =Math.min(currentSmallest, finalResult ) 
Time Complexity: O(2n)->)O(n) 
Space Complexity: O(n)
> 

### Pattern

You wrote:

```
HashSet
```

🟡 **Partially correct.**

A HashSet gives an **O(n)** solution, so it's a valid approach.

However, the **most optimal interview solution** is actually an **Array / In-place Index Placement (Cyclic Sort idea)** pattern with **O(1)** extra space.

So there are two good approaches:

- ✅ Better: **HashSet** — `O(n)` time, `O(n)` space
- ⭐ Optimal: **In-place Index Placement** — `O(n)` time, `O(1)` extra space

Since we haven't learned the in-place pattern yet, **HashSet is a perfectly acceptable answer**.

---

# Why

You wrote:

> we can use if element exists logic
> 

✅ Correct.

The key observation is:

```
Need to quickly know:
Does 1 exist?
Does 2 exist?
Does 3 exist?
...
```

That's exactly what a HashSet is good at.

---

# Brute Force

You wrote:

```
O(n²)
```

✅ Correct.

For every positive integer:

```
1
2
3
4
...
```

search the entire array.

---

# Your Approach

You wrote:

> if current element -1 exists then smallest will current element+1 else current element-1
> 

❌ This is where the logic breaks.

Let's test it.

Example:

```
nums = [3,4,-1,1]
```

Set:

```
{-1,1,3,4}
```

Take:

```
current = 3
```

`3 - 1 = 2`

Does 2 exist?

```
No
```

Your logic would say:

```
Answer = 2
```

That happens to be correct **by coincidence**.

Now try:

```
nums = [1,2,3]
```

Take:

```
current = 3
```

`3 - 1 = 2`

Exists.

So your logic says:

```
Answer = 4
```

Correct.

Now take:

```
current = 2
```

`2 - 1 = 1`

Exists.

Your logic says:

```
Answer = 3
```

Now you have multiple candidate answers (3 and 4), and it's unclear how to decide. The approach doesn't consistently identify the **smallest missing positive**.

---

## Correct HashSet Approach

The standard HashSet solution is simpler:

1. Put all numbers into a `Set`.
2. Start checking from `1`.
3. The **first positive integer not in the set** is the answer.

Example:

```
Set = {3,4,-1,1}

Check 1 → Yes
Check 2 → No

Answer = 2
```

Or:

```
Set = {1,2,0}

Check 1 → Yes
Check 2 → Yes
Check 3 → No

Answer = 3
```

---

# Complexity

You wrote:

```
Time: O(2n) -> O(n)
Space: O(n)
```

# HashSet Solution

```
function firstMissingPositive(nums) {

const set=newSet(nums);

for (let i=1;i<=nums.length+1;i++) {
if (!set.has(i)) {
return i;
        }
    }
}
```
