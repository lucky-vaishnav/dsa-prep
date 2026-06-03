**When to use:**

Linked list cycle detection, middle element, palindrome LL.

**Common problems:**

- Detect cycle
- Find cycle start
- Find middle of LL

**Key idea:**

Slow moves 1 step, fast moves 2.

it’s better to treat **Fast & Slow Pointers (Floyd’s pattern)** as a **separate pattern** from **general Two Pointers** in interview prep.

### Core Template (for notes / revision)

### Cycle Detection Template

```jsx
let slow = head;
let fast = head;

while (fast && fast.next) {
  slow = slow.next;
  fast = fast.next.next;

if (slow === fast) {
// cycle detected
returntrue;
  }
}
returnfalse;

```

---

### Find Middle of Linked List
```javascript
let slow = head;
let fast = head;

while (fast && fast.next) {
  slow = slow.next;
  fast = fast.next.next;
}
return slow;// middle
```
