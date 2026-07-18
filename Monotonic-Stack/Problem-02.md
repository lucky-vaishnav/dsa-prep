## Problem: Valid Parentheses

Given a string containing only:

```
( ) { } [ ]
```

Determine if the string is valid.

A string is valid if:

- Every opening bracket has a matching closing bracket.
- Brackets close in the correct order.

### Example 1

```
Input:
"()[]{}"

Output:
true
```

### Example 2

```
Input:
"(]"

Output:
false
```

### Example 3

```
Input:
"([)]"

Output:
false
```

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

💡 **Hint:** This is one of the classic Stack problems.

### My Answer-

So for question number one, we will be using a stack where we will be storing the indexes of the string and whatever last element of the stack. And according to that, when we put a value in the stack, we will check that according to the last value, the closing bracket should be there. If already there, then we will add a new element and check for the closing element for that. If whenever there is mismatch, then we will return false. If this works properly, then we will return true. The pattern will be modeled in stack and that, why? Because we need to track the last bracket of the string, that is why we are using stack. Time force will be O of n square, output data structure model in stack. And complexity of that will be O of n, and space complexity will be O of n as well. I am thinking about that how we will matching the closing brackets. So I think according to me, we can have a closing brackets temporary array, constant array, by which we can see that what are the closing brackets. That I am still thinking. But yeah, that will be the approach. Share the code as well for that. And if there is any other approach, that also tell me. Share the code without the explanation.

---

# Review

## Pattern

```
Stack
```

✅ Correct.

---

## Why

You wrote:

> Need to track the last bracket.
> 

✅ Exactly.

A stack follows **LIFO (Last In, First Out)**, which perfectly matches nested brackets.

---

## Brute Force

You wrote:

```
O(n²)
```

🟡 There isn't really a meaningful brute force solution that's used for this problem. In interviews, we usually only discuss the stack solution because it's the natural approach.

---

## Optimal Data Structure

```
Stack
```

✅ Correct.

---

## Optimal Approach

You wrote:

> According to the last value, the closing bracket should be there.
> 

Almost.

A slightly better wording is:

> Push opening brackets onto the stack. When a closing bracket is found, it must match the opening bracket at the top of the stack. If it doesn't, return `false`. At the end, if the stack is empty, return `true`.
> 

---

## Time Complexity

```
O(n)
```

✅ Correct.

---

## Space Complexity

```
O(n)
```

✅ Correct.

Worst case:

```
((((((((
```

Everything gets pushed.

---

# Code (Map Approach - Most Common)

```jsx
function isValid(s) {
  const stack = [];
  const map = {
    ")": "(",
    "]": "[",
    "}": "{",
  };
  for (const ch of s) {
    if (ch === "(" || ch === "[" || ch === "{") {
      stack.push(ch);
    } else {
      if (stack.length === 0 || stack.pop() !== map[ch]) {
        return false;
      }
    }
  }
  return stack.length === 0;
}
console.log(isValid("()[]{}"));
```

---

# Alternative Code (Without Map)

```jsx
function isValid(s) {
  const stack = [];
  for (const ch of s) {
    if (ch === "(" || ch === "[" || ch === "{") {
      stack.push(ch);
    } else {
      const top = stack.pop();
      if (
        (ch === ")" && top !== "(") ||
        (ch === "]" && top !== "[") ||
        (ch === "}" && top !== "{")
      ) {
        return false;
      }
    }
  }
  return stack.length === 0;
}
```

---

# Which one is better?

✅ **Map approach** is generally preferred because:

- Easier to read
- Easier to extend
- Less repetitive

---

## ⭐ One Interview Tip

You mentioned storing **indexes** in the stack.

For this problem, we **don't need indices**.

We only need the brackets themselves:

```
stack.push('(');stack.push('{');stack.push('[');
```

Unlike **Daily Temperatures** or **Sliding Window Maximum**, we never calculate distances or positions, so storing indices doesn't provide any benefit.

This is a good distinction to remember:

- **Need distance/index calculations?** → Store **indices**.
- **Need only values?** → Store **values** (like brackets here).

That's the only correction I'd make. Otherwise, your reasoning is solid.
