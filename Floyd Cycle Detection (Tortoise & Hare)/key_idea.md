**Floyd Cycle Detection (Tortoise & Hare)** is a completely separate DSA pattern.

I would put it under:

```
Fast & Slow Pointer Pattern
```

This pattern is extremely common in Linked Lists and sometimes Arrays.

---

# Floyd Cycle Detection (Tortoise & Hare)

## Why does it exist?

To detect:

```
Cycle / Loop
```

without using:

```
HashSet
Extra Memory
```

---

# Core Idea

Use two pointers:

```
Slow = moves 1 step

Fast = moves 2 steps
```

---

# Visual

Linked List

```
1 → 2 → 3 → 4 → 5
          ↑     ↓
          ← ← ←
```

Cycle exists.

---

Start:

```
Slow = 1

Fast = 1
```

Move:

```
Slow -> 2

Fast -> 3
```

Move:

```
Slow -> 3

Fast -> 5
```

Move:

```
Slow -> 4

Fast -> 4
```

Both meet.

Cycle detected.

---

# Why Does It Work?

Imagine race track:

```
Slow speed = 1

Fast speed = 2
```

If track is circular:

```
Fast eventually laps Slow
```

and catches it.

Exactly same idea.

---

# Recognition Pattern

If problem mentions:

```
Cycle
Loop
Repeated traversal
Linked List cycle
Duplicate number
Middle node
Happy Number
```

Think:

```
Fast & Slow Pointer
```

---

# Template 1

## Detect Cycle

LeetCode 141

```
functionhasCycle(head) {

letslow=head;
letfast=head;

while (fast&&fast.next) {

slow=slow.next;

fast=fast.next.next;

if (slow===fast) {
returntrue;
        }
    }

returnfalse;
}
```

---

Complexity

```
Time: O(n)

Space: O(1)
```

---

# Pattern 2

## Find Cycle Start

LeetCode 142

Harder and very famous.

---

Step 1

Find meeting point.

```
Slow == Fast
```

---

Step 2

Move:

```
Pointer1 = head

Pointer2 = meeting point
```

---

Both move:

```
1 step
```

until they meet.

Meeting point:

```
Cycle Start
```

---

Code

```
functiondetectCycle(head) {

letslow=head;
letfast=head;

while (fast&&fast.next) {

slow=slow.next;
fast=fast.next.next;

if (slow===fast) {

letp1=head;
letp2=slow;

while (p1!==p2) {

p1=p1.next;
p2=p2.next;
            }

returnp1;
        }
    }

returnnull;
}
```

---

# Interview Question

Why does this work?

Answer:

```
Distance from head to cycle start
=
Distance from meeting point to cycle start
```

Mathematical proof exists.

Interviewers rarely ask proof.

Just know:

```
Reset one pointer to head.
Move both one step.
Meeting point = cycle start.
```

---

# Pattern 3

## Find Middle Node

LeetCode 876

---

Example

```
1 → 2 → 3 → 4 → 5
```

Answer:

```
3
```

---

Use:

```
Slow = 1 step

Fast = 2 steps
```

When:

```
Fast reaches end
```

Slow is at:

```
Middle
```

---

Code

```
functionmiddleNode(head) {

letslow=head;
letfast=head;

while (fast&&fast.next) {

slow=slow.next;
fast=fast.next.next;
    }

returnslow;
}
```

---

Recognition

```
Find middle
Single pass
Linked List
```

Think:

```
Fast Slow
```

---

# Pattern 4

## Happy Number

LeetCode 202

Not Linked List.

---

Example

```
19

1² + 9² = 82

8² + 2² = 68

6² + 8² = 100

1
```

Happy.

---

Observation

Sequence eventually:

```
Reaches 1
OR

Forms cycle
```

---

Use Floyd Cycle Detection.

---

Recognition

```
Repeated transformation
Repeated state
May enter loop
```

Think:

```
Floyd
```

---

# Pattern 5

## Find Duplicate Number

LeetCode 287

One of the most famous uses.

---

Input

```
[1,3,4,2,2]
```

Output

```
2
```

---

Amazing trick.

Treat array as linked list.

Example:

```
Index -> Value

0 -> 1
1 -> 3
3 -> 2
2 -> 4
4 -> 2
```

Forms cycle.

Apply Floyd.

---

Recognition

```
Numbers 1..n
One duplicate
Cannot modify array
O(1) space
```

Think:

```
Floyd
```

---

# Fast & Slow Pattern Recognition

If problem says:

```
Cycle
Loop
Repeated state
```

Think:

```
Floyd Cycle Detection
```

---

If problem says:

```
Middle Node
```

Think:

```
Fast Slow
```

---

If problem says:

```
Nth from end
```

Think:

```
Two Pointers
```

(related pattern)

---

# Important LeetCode Questions

### Easy

```
141. Linked List Cycle
202. Happy Number
876. Middle of Linked List
```

---

### Medium

```
142. Linked List Cycle II
287. Find Duplicate Number
```

---

### Hard

```
457. Circular Array Loop
```

---

# Interview Cheat Sheet

```
Fast & Slow Pointer Pattern

Cycle Detection:
slow = 1 step
fast = 2 steps

if slow == fast
cycle exists

Find Cycle Start:
1. Detect meeting point
2. Move one pointer to head
3. Move both 1 step
4. Meeting point = cycle start

Find Middle:
Fast reaches end
Slow reaches middle

Complexity:
Time O(n)
Space O(1)
```

---

# Notes Summary

```
Floyd Cycle Detection (Tortoise & Hare)

Pattern:
Fast & Slow Pointer

Recognition:
- Cycle detection
- Loop detection
- Repeated state
- Middle node
- Duplicate number
- Happy number

Core Logic:
slow += 1 step
fast += 2 steps

If cycle exists:
slow == fast

Important Problems:
LC 141
LC 142
LC 202
LC 287
LC 876

Complexity:
Time O(n)
Space O(1)
```

This is one of those patterns that interviewers expect you to recognize immediately once you see words like:

```
Cycle
Loop
Repeated State
Find Middle
```

and it's usually considered a Top 15 DSA pattern for interviews.
