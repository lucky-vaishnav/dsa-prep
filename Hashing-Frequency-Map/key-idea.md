**When to use:**

Counting, lookups, duplicates, pairing, anagrams.

**Common problems:**

- Two sum
- Anagram check
- Longest substring

**Key idea:**

Store visited states → fast lookup.

### 1️⃣ Is Hashing a separate pattern?

### ✅ Yes — but also a **foundational pattern**

Think of **Hashing / Frequency Map** as:

- 🔹 A **core standalone pattern**
- 🔹 A **building block** used inside many other patterns

### Used **independently** in:

- Frequency counting
- Existence checks
- De-duplication
- Pair / complement problems

### Used **inside other patterns**:

- Sliding Window (counts in window)
- Prefix Sum + HashMap
- Two Sum variants
- Graphs (visited map)
- Greedy + Map
- Heap + Map

📌 **Interview mindset**

If the problem says:

- “count”
- “frequency”
- “how many times”
- “exists / seen before”
- “pair / complement”

👉 **HashMap should instantly come to mind**

---

### 2️⃣ When to Use Hashing (Recognition Signals)

Look for these keywords 👀

| Keyword in Problem | Meaning |
| --- | --- |
| frequency / count | Map |
| unique / duplicate | Set / Map |
| pair sum / difference | Map |
| anagram | Frequency Map |
| first non-repeating | Map |
| subarray sum | Prefix Sum + Map |
|  |  |

---

### Set vs Map — One-Line Interview Answer 🧠

> “Set is used when I only need uniqueness or existence checks.
> 
> 
> Map is used when I need to **associate data or counts** with keys.”
> 

### What You Can Do With Set (and What You Can’t)

### ✅ Allowed / Intended

```jsx
set.add(5);
set.has(5);
set.delete(5);
set.size;

```

### ❌ Not Supported

```jsx
set.get(5);// ❌
set[0];// ❌

```

---

### Interview Rule of Thumb (VERY IMPORTANT)

### Ask yourself:

> “Do I need to count or store extra data?”
> 
- Yes → **Map**
- No, only existence → **Set**

### 3️⃣ Core Time & Space Complexity

| Operation | Complexity |
| --- | --- |
| Insert / Lookup | `O(1)` average |
| Traverse array once | `O(n)` |
| Space | `O(n)` |

📌 **Trade-off**

Use **extra memory** to reduce **time complexity**

---

### 4️⃣ Core Templates (VERY IMPORTANT)

### 🔹 Template 1: Frequency Count

```jsx
const freq =new Map();

for (let num of nums) {
  freq.set(num, (freq.get(num) ||0) +1);
}

```

🧠 Used in:

- Majority Element
- Count occurrences
- Mode problems

---

### 🔹 Template 2: Seen / Exists Check

```jsx
const seen =new Set();

for (let num of nums) {
if (seen.has(num))return true;
  seen.add(num);
}

```

🧠 Used in:

- Duplicate detection
- Cycle detection (non-Floyd)
- Unique checks

---

### 🔹 Template 3: Complement Pattern (Two Sum)

```jsx
const map =new Map();

for (let i =0; i < nums.length; i++) {
const need = target - nums[i];
if (map.has(need))return [map.get(need), i];
  map.set(nums[i], i);
}

```

🧠 Used in:

- Two Sum
- Pair problems
- Difference problems

---

### 🔹 Template 4: Prefix Sum + HashMap (Advanced but Common)

```jsx
const map =new Map();
map.set(0,1);

let sum =0;
let count =0;

for (let num of nums) {
  sum += num;
if (map.has(sum - k)) {
    count += map.get(sum - k);
  }
  map.set(sum, (map.get(sum) ||0) +1);
}

```

🧠 Used in:

- Subarray sum equals K
- Count subarrays
- Zero sum problems

---

### 5️⃣ Must-Do LeetCode Problems (Interview Priority)

### ⭐ Beginner (Must know)

1. **1. Two Sum**
2. **217. Contains Duplicate**
3. **242. Valid Anagram**
4. **169. Majority Element**

---

### ⭐⭐ Medium (Very common)

1. **560. Subarray Sum Equals K**
2. **49. Group Anagrams**
3. **347. Top K Frequent Elements**
4. **525. Contiguous Array**

---

### ⭐⭐⭐ Advanced

1. **128. Longest Consecutive Sequence**
2. **438. Find All Anagrams in a String**
