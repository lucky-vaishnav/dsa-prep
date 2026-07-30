## Problem: Group Anagrams

Given an array of strings `strs`, group the anagrams together.

Two strings are anagrams if they contain the **same characters with the same frequencies**, only the order differs.

### Example

```
Input:
["eat","tea","tan","ate","nat","bat"]

Output:
[
  ["eat","tea","ate"],
  ["tan","nat"],
  ["bat"]
]
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

### My Answer-

So for question number one, group anagrams, so for that pattern we can use hashmap, so that we can count and store the string which are anagrams. And for that, time complexity will be O of n, space complexity will be O of n. Brute force approach, in short, the time complexity will be O of n square. And while storing to the hashmap, we can create a unique key so that we know that the next string is anagram. So for that, there can be multiple approaches, like we can sort that particular string and then use it as a key. And there are multiple ways to do that to get the unique key. So you can share the code for it, and also share the code for brute force approach.

You're now thinking beyond just the pattern—you identified the **key challenge**:

> **Generate the same key for all anagrams.**
> 

That's exactly the heart of the problem.

The only small correction:

- The overall time complexity is **not always O(n)**.
- It depends on how you generate the key.

---

# Review

### Pattern

```
HashMap
```

✅ Correct.

---

### Why

You wrote:

> Store strings using a unique key.
> 

✅ Correct.

---

### Brute Force

```
O(n²)
```

✅ Acceptable.

---

### Optimal Data Structure

```
HashMap
```

✅ Correct.

---

### Optimal Approach

You wrote:

> Sort the string and use it as the key.
> 

✅ This is the most common interview solution.

Example:

```
eat  -> aet
tea  -> aet
ate  -> aet
```

All map to the same key.

---

### Time Complexity

If there are:

- `n` strings
- each string length = `m`

Sorting each string costs:

```
O(m log m)
```

Overall:

```
O(n × m log m)
```

---

### Space Complexity

```
O(n)
```

(or more precisely `O(n × m)` because we store all strings)

---

## Brute Force (Compare Every Pair)

```jsx
function groupAnagrams(strs) {

    const visited = new Array(strs.length).fill(false);
    const result = [];

    for (let i = 0; i < strs.length; i++) {

        if (visited[i]) continue;

        const group = [strs[i]];
        visited[i] = true;

        const sorted1 = strs[i].split('').sort().join('');

        for (let j = i + 1; j < strs.length; j++) {

            if (visited[j]) continue;

            const sorted2 = strs[j].split('').sort().join('');

            if (sorted1 === sorted2) {
                group.push(strs[j]);
                visited[j] = true;
            }
        }

        result.push(group);
    }

    return result;
}
```

---

## Optimal (HashMap + Sorted Key)

```jsx
function groupAnagrams(strs) {

    const map = new Map();

    for (const str of strs) {

        const key = str
            .split('')
            .sort()
            .join('');

        if (!map.has(key)) {
            map.set(key, []);
        }

        map.get(key).push(str);
    }

    return [...map.values()];
}
```

---

# ⭐ Another Optimal Approach (Without Sorting)

Instead of sorting, count the frequency of all 26 characters.

Example:

```
eat

a -> 1
e -> 1
t -> 1
```

Key:

```
1#0#0#0#1#0#0#...#1...
```

Then:

```jsx
const count = new Array(26).fill(0);

for (const ch of str) {
    count[ch.charCodeAt(0) - 97]++;
}

const key = count.join('#');
```

Overall complexity:

```
O(n × m)
```

because counting characters is linear.

---

```jsx
function groupAnagrams(strs) {

    const map = new Map();

    for (const str of strs) {

        const count = new Array(26).fill(0);

        for (const ch of str) {
            count[ch.charCodeAt(0) - 'a'.charCodeAt(0)]++;
        }

        const key = count.join('#');

        if (!map.has(key)) {
            map.set(key, []);
        }

        map.get(key).push(str);
    }

    return [...map.values()];
}

console.log(groupAnagrams(["eat","tea","tan","ate","nat","bat"]));
```

### Example Key Generation

```
eat

a -> 1
b -> 0
c -> 0
d -> 0
e -> 1
...
t -> 1
...

Key:
1#0#0#0#1#0#0#0#...#1#...
```

For:

```
tea
ate
```

the generated key is **exactly the same**, so they end up in the same HashMap entry.

### Complexity

- **Time:** `O(n × m)`
- **Space:** `O(n × m)`

> **Interview Note:** This approach is considered better than sorting because generating the frequency array is **O(m)**, while sorting each string takes **O(m log m)**.
> 

---

## ⭐ One Interview Tip

When you hear:

> **"Group strings"**
> 

your first thought should be:

> **HashMap**
> 

Then ask yourself:

> **"What can be the unique key?"**
> 

That "find the key" step is the main trick in many HashMap interview problems (Group Anagrams, Isomorphic Strings, Word Pattern, etc.). Once you identify the correct key, the rest of the solution is usually straightforward.
