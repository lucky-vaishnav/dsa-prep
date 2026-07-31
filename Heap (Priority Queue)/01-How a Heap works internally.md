If you understand **how a Heap works internally**, you'll never have to memorize Heap problems.

We'll do it in this order:

```
Part 2.1  Binary Tree representation
Part 2.2  Heap Properties
Part 2.3  Array Representation ⭐
Part 2.4  Insert (Heapify Up)
Part 2.5  Remove Top (Heapify Down)
Part 2.6  Build Complete Heap Class
Part 2.7  Dry Run
Part 2.8  Interview Template
```

---

# Part 2.1 - What actually is a Heap?

Most people think Heap is some magical data structure.

It isn't.

It is simply a **Complete Binary Tree**.

Example:

```
        90
      /    \
    70      60
   /  \    /  \
 40   30  20  10
```

Nothing magical.

Just a binary tree.

---

## What makes it different?

Only ONE rule.

### Max Heap

Every parent

```
>=
```

its children.

```
        90
      /    \
    70      60
   /  \    /  \
 40   30  20  10
```

90 > 70

90 > 60

70 > 40

70 > 30

Everything satisfies.

---

### Min Heap

Exactly opposite.

Parent is always smaller.

```
        10
      /    \
    20      30
   /  \    /  \
 40   50  60  70
```

---

# Part 2.2 - Complete Binary Tree

This is VERY important.

Heap MUST be complete.

Means

```
Level 1
        X

Level 2
      X   X

Level 3
    X X X X
```

Every level is full except maybe the last.

Last level fills

```
LEFT → RIGHT
```

Only.

Valid

```
      5
    /   \
   7     8
  /
 9
```

Invalid

```
      5
    /   \
   7     8
        /
       9
```

Gap exists.

Not complete.

---

# ⭐ Why Complete Tree?

Because then we never need pointers.

Instead of

```javascript
class Node{
 left
 right
}
```

We simply store

```javascript
[90,70,60,40,30,20,10]
```

That's Heap.

---

# Part 2.3 - Array Representation ⭐⭐⭐⭐⭐

This is the MOST important concept.

Binary Tree

```
        90
      /    \
    70      60
   /  \    /  \
 40   30  20  10
```

Array

```
Index

0   1   2   3   4   5   6

90  70  60  40  30  20  10
```

Nothing else.

Just an array.

---

## Magic Formula ⭐⭐⭐⭐⭐

Suppose current node index is

```
i
```

Left Child

```
2*i + 1
```

Right Child

```
2*i + 2
```

Parent

```
Math.floor((i-1)/2)
```

---

Example

Current index

```
1
```

Value

```
70
```

Left child

```
2*1+1 =3
```

Array

```
Index

0 1 2 3 4 5 6

90 70 60 40 30 20 10
```

Index 3

```
40
```

Correct.

Right child

```
2*1+2=4
```

Value

```
30
```

Correct.

Parent

```
floor((1-1)/2)

0
```

Value

```
90
```

Correct.

---

# ⭐⭐⭐ Interview Memory

```
Left

2*i+1

------------------

Right

2*i+2

------------------

Parent

floor((i-1)/2)
```

**Memorize these three formulas.** They are used in **every Heap implementation**.

---

# Why are these formulas so important?

Because every Heap operation is just:

1. Find parent.
2. Compare.
3. Swap if needed.

OR

1. Find children.
2. Compare.
3. Swap if needed.

That's literally the whole Heap algorithm.

---

# Let's verify another example

Array

```
Index

0 1 2 3 4 5 6 7

90 70 60 40 30 20 10 5
```

Take

```
i = 2
```

Value

```
60
```

Left

```
2*2+1

5
```

Value

```
20
```

Right

```
2*2+2

6
```

Value

```
10
```

Parent

```
floor((2-1)/2)

0
```

Value

```
90
```

Everything matches.

---

# 📝 Notes for your notebook

```
HEAP

Heap = Complete Binary Tree

Types:
1. Min Heap
2. Max Heap

Complete Binary Tree:
- Every level full except last
- Last level fills left to right

Stored as Array

Formulas:

Left Child
2*i + 1

Right Child
2*i + 2

Parent
floor((i-1)/2)

These three formulas are the foundation of every Heap operation.
```

---

