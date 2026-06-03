**When to use:**

Sorted arrays, or problems involving pair/triplet, merging, removing duplicates.

**Key idea:**

Left/right pointers move toward each other or in same direction.

Two pointers is one of the **highest-frequency** DSA patterns because of efficiency:

**O(n)** instead of **O(n²)**.

# When to immediately think of Two Pointers

👉 If the question involves:

### **Arrays / Strings**

- Searching pairs / triplets
- Sorting + scanning
- Moving from both ends
- Removing elements in place
- Comparing sequences

### **Strings**

- Palindrome check
- Reverse words
- Skip characters

### **Linked Lists**

- Slow & fast pointer (Floyd's algorithm)
- Middle of linked list
- Detect cycle

### **Geometry / Math**

- Container With Most Water
- Two-sum variant

👉 Keywords that trigger this pattern:

- **pair / triplet**
- **sorted array**
- **closest sum**
- **minimum difference**
- **left / right**
- **merge / compare**
- **is palindrome?**

# Types of Two Pointers

## **1. Opposite-direction pointers (left→right & right→left)**

Used when scanning from both ends.

✔ Sorted array

✔ Palindrome

✔ Trapping rain water

✔ Container with most water

### Template

```jsx
let left = 0;
let right = arr.length - 1;

while (left < right) {
    // process
    if (condition) left++;
    else right--;
}

```

---

## **2. Same-direction pointers (fast/slow)**

Used when one pointer “catches up”.

✔ Removing duplicates

✔ Move zeros

✔ Partitioning arrays

✔ Sliding window alternative

✔ Linked list cycle detection

### Template

```jsx
let slow = 0;
for (let fast = 0; fast < arr.length; fast++) {
    if (valid(arr[fast])) {
        arr[slow] = arr[fast];
        slow++;
    }
}

```

---

