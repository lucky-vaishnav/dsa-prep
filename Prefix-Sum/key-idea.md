## **Prefix Sum / Difference Array**

**When to use:**

Range queries (sum, update), large input.

**Common problems:**

- Subarray sum equals K
- Range addition
- Maximum population year

**Key idea:**

Precompute prefix array → O(1) query.

### 1️⃣ Is Prefix Sum / Difference Array a Unique DSA Pattern?

### Short answer

👉 **Yes, it is a standalone pattern**, not just a subset.

### How interviewers see it

| Pattern | Purpose |
| --- | --- |
| Prefix Sum | Fast **range queries** |
| Difference Array | Fast **range updates** |
| Sliding Window | Fixed/variable window aggregation |
| Binary Search | Search on sorted or answer space |

📌 **Prefix Sum ≠ Sliding Window**

- Sliding Window → contiguous window with conditions
- Prefix Sum → precomputation for **any range**

📌 **Difference Array complements Prefix Sum**

- Prefix Sum → *Query optimization*
- Difference Array → *Update optimization*

---

### 2️⃣ Prefix Sum — Core Idea (1 Line)

> Precompute cumulative sums so any range sum can be answered in O(1).
> 

---

### 3️⃣ Prefix Sum Formula (Must Memorize)

Given array `arr`:

```
prefix[i] = arr[0] + arr[1] + ... + arr[i]

```

### Range sum (L → R)

```
sum(L, R) = prefix[R] - prefix[L - 1]

```

(if `L == 0`, just `prefix[R]`)

---

### 4️⃣ Prefix Sum Example (Visual)

```
arr     = [2, 4, 6, 8]
prefix  = [2, 6, 12, 20]

sum(1, 3) = 20 - 2 = 18

```

---

### 5️⃣ Standard Prefix Sum Template (Notes-Friendly)

```jsx
function buildPrefix(arr) {
const prefix =new Array(arr.length);
    prefix[0] = arr[0];

for (let i =1; i < arr.length; i++) {
        prefix[i] = prefix[i -1] + arr[i];
    }
return prefix;
}

// range sum
function rangeSum(prefix, L, R) {
if (L ===0)return prefix[R];
return prefix[R] - prefix[L -1];
}

```

---

### 6️⃣ Difference Array — Why & When?

### Problem

You need to apply **many range updates** like:

> Add x to all elements from L to R
> 

Doing it directly = **O(n × updates)** ❌

### Solution

👉 Use **Difference Array**

---

### 7️⃣ Difference Array Core Idea

Instead of updating all elements:

diff = Actual Problem Array

diff[L] += val

diff[R+1] -= val

Then take **prefix sum** at the end.

---

### 8️⃣ Difference Array Example

Initial array (size 5):

```
diff = [0,0,0,0,0]

```

range [1,3]

```
diff[1] +=10          //diff[L] += val
diff[4] -=10          //diff[R+1] -= val

diff = [0,10,0,0,-10]
```

Final array after prefix sum:

```
[0, 10, 10, 10, 0]

```

---

### 9️⃣ Difference Array Template

```jsx
functionrangeUpdate(n, updates) {
const diff =newArray(n).fill(0);

for (const [L, R, val]of updates) {
        diff[L] += val;
if (R +1 < n) diff[R +1] -= val; //you must check whether R + 1 is inside the array before subtracting.Prefix sum still produces correct result.
    }

// build final array
for (let i =1; i < n; i++) {
        diff[i] += diff[i -1];
    }

return diff;
}

```

---

### 🔹 Example Input

```jsx
const n =5;
const updates = [
    [1,3,2],// add 2 to index 1 → 3
    [2,4,3],// add 3 to index 2 → 4
    [0,2, -2]// subtract 2 from index 0 → 2
];

```

---

### Question:

You have **5 boxes**, all start with `0`.

```
Index:  0  1  2  3  4
Boxes:  0  0  0  0  0

```

Now apply these operations:

1. Add **2** to boxes **1 to 3**
2. Add **3** to boxes **2 to 4**
3. Subtract **2** from boxes **0 to 2**

**Final question:**

👉 What are the box values at the end?

---

### How a NORMAL Person Would Solve (Brute Force)

### Operation 1: `[1,3] +2`

```
0  2  2  2  0

```

### Operation 2: `[2,4] +3`

```
0  2  5  5  3

```

### Operation 3: `[0,2] -2`

```
-2  0  3  5  3

```

✅ Final Answer:

```
[-2, 0, 3, 5, 3]

```

This is **easy**, but slow if array is large.

---

### WHY Difference Array Exists (The Real Problem)

Imagine:

- Array size = **10⁵**
- Operations = **10⁵**

Brute force:

```
O(n ×operations)=tooslow ❌

```

So interviewers ask:

> “Can you apply range updates efficiently?”
> 

That’s where **Difference Array** comes in.

---

### Difference Array — What It REALLY Means (Simple)

Instead of updating **every index**, we do this:

> “Mark where an update starts and where it ends.”
> 

---

### Visual Explanation (MOST IMPORTANT)

We use a helper array called `diff`.

### Rule:

For operation `[L, R, val]`

```
diff[L] +=val
diff[R +1] -=val

```

That’s it.

---

### Apply SAME Example Using Difference Array

### Initial diff array:

```
[0, 0, 0, 0, 0]

```

---

### Operation 1: `[1,3] +2`

```
diff[1] +=2
diff[4] -=2

```

```
[0, 2, 0, 0, -2]

```

---

### Operation 2: `[2,4] +3`

```
diff[2] +=3

```

```
[0, 2, 3, 0, -2]

```

---

### Operation 3: `[0,2] -2`

```
diff[0] -=2
diff[3] +=2

```

```
[-2, 2, 3, 2, -2]

```

---

### Final Step: Build Actual Values (Prefix Sum)

Now **accumulate**:

```
Index:   0   1   2   3   4
Diff:   -2   2   3   2  -2
Value:  -2   0   3   5   3

```

🎯 SAME result as brute force.

🔹 Difference Array records where a value starts affecting the array and where it stops affecting the array. prefix sum converts it into final values and It is trick to avoid o(n*updates).

### Time Complexity of Difference Array

### 1️⃣ Applying one range update

**Operation:** Add `val` to range `[l, r]`

```jsx
diff[l] += val
diff[r +1] -= val

```

✅ **Time Complexity:** `O(1)`

No loop. Just **two operations**.

---

### 2️⃣ Applying `k` range updates

✅ **Time Complexity:** `O(k)`

Each update is constant time.

---

### 3️⃣ Building the final array (Prefix Sum)

```jsx
for i =1 ton:
  arr[i] = arr[i -1] + diff[i]

```

✅ **Time Complexity:** `O(n)`

---

### ✅ Total Time Complexity

| Step | Time |
| --- | --- |
| k range updates | `O(k)` |
| Build final array | `O(n)` |
| **Total** | **`O(n + k)`** |

### 🔟 Prefix Sum + HashMap (VERY IMPORTANT)

Used when:

- Subarray sum
- Count of subarrays
- Target sum problems

### Key Insight

> If prefix[j] - prefix[i] = k, then subarray (i+1 → j) sums to k
> 

---

### 1️⃣1️⃣ Template: Prefix Sum + Map

```jsx
function subarraySum(nums, k) {
const map =new Map();
    map.set(0,1);

let sum =0, count =0;

for (let num of nums) {
        sum += num;

if (map.has(sum - k)) {
            count += map.get(sum - k);
        }

        map.set(sum, (map.get(sum) ||0) +1);
    }

return count;
}

```

---

**why we are doing map.set(0, 1); for Prefix Sum + Map examaple template?**

### Short Answer (Interview-Ready)

We do:

```jsx
map.set(0,1);

```

👉 **To handle subarrays that start from index `0`**.

---

### What the Map Stores

In Prefix Sum + Map:

```
map[prefixSum] = how many times this prefixSum has appeared

```

Before processing any element:

- Prefix sum = `0`
- It has appeared **once** (empty prefix)

So we initialize:

```jsx
map.set(0,1);

```

---

### What Breaks If We Don’t Do This?

### Example

```jsx
nums = [1,2,3]
k =3

```

Correct answer = `2`

Subarrays:

- `[1, 2]`
- `[3]`

---

### Step-by-step WITH `map.set(0,1)`

| i | num | sum | sum - k | map[sum-k]? | count |
| --- | --- | --- | --- | --- | --- |
| 0 | 1 | 1 | -2 | ❌ | 0 |
| 1 | 2 | 3 | 0 | ✅ (1) | 1 |
| 2 | 3 | 6 | 3 | ✅ (1) | 2 |

✅ Works correctly

---

### WITHOUT `map.set(0,1)`

At index `1`:

- `sum = 3`
- `sum - k = 0`
- `map[0]` does **not exist**

❌ Subarray `[1,2]` is **missed**

### 1️⃣2️⃣ Interview Trigger Words (IMPORTANT)

Look for:

- **Range sum**
- **Subarray**
- **Cumulative**
- **Multiple queries**
- **Difference**
- **Add value to range**
- **Prefix**

---

### 1️⃣3️⃣ Must-Do LeetCode Questions

### 🟢 Beginner

1. **303. Range Sum Query – Immutable**
2. **1480. Running Sum of 1d Array**

### 🔵 Prefix Sum + Map

1. **560. Subarray Sum Equals K** ⭐
2. **525. Contiguous Array**
3. **974. Subarray Sums Divisible by K**

### 🔴 Difference Array

1. **370. Range Addition**
2. **1109. Corporate Flight Bookings** ⭐
3. **1094. Car Pooling**

### 🔥 Advanced / Mixed

1. **2381. Shifting Letters II**
2. **2536. Increment Submatrices**

---

### 1️⃣4️⃣ One-Page Revision Notes (Save This)

### Prefix Sum

- Used for fast range queries
- Precompute cumulative sum
- Range sum in O(1)

### Difference Array

- Used for fast range updates
- Update endpoints only
- Build final array using prefix sum

### Prefix + Map

- Used for subarray sum problems
- Key formula: `sum[j] - sum[i] = k`

### Complexity

- Time: O(n)
- Space: O(n)

---

### 1️⃣5️⃣ Interview Tip (High Value)

If interviewer asks:

> “Why does prefix sum work?”
> 

Say:

> “Because subtraction of cumulative sums isolates the exact range contribution.”
> 

💯 Clear and confident answer.
