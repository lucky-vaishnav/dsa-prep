## Problem: Koko Eating Bananas (LeetCode 875)
Koko loves to eat bananas. There are n piles of bananas, the ith pile has piles[i] bananas. The guards have gone and will come back in h hours.

Koko can decide her bananas-per-hour eating speed of k. Each hour, she chooses some pile of bananas and eats k bananas from that pile. If the pile has less than k bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return the minimum integer k such that she can eat all the bananas within h hours.
```text
piles = [3,6,7,11]
h = 8

Output:
4
```

Tell me:

* Pattern
* Why
* Brute Force Complexity
* Optimal Data Structure
* Optimal Approach
* Time Complexity
* Space Complexity

💡 Hint:
This is **not** searching in an array. Think:

> **Binary Search on the answer.**

---
# My Thought -
So for question number one, Cocoa eating banana. So yeah, for the approach will be like that. First, the brute force complexity will be O of n or O of 2n because we will need a two for loop for the brute force. First, we'll be calculating the sum of all the elements, sum of all the elements, and we will calculate the average as well per hour using the hour value. And then we will find the value which is max value within that piles which is greater than that average. And if not, then that average will be the answer. And while calculating the average, we will round off the value to maximum, like math.ceil. So brute force complexity will be O of 2n or O of 2n plus k. And for optimal approach, so what we can do is that we can calculate the total sum and sort the piles array both, and then we will calculate the total average using math.ceil. And then we will find a maximum element which is greater than that average. So it will be around, time complexity will be O of 2n plus k around, and space complexity will be O of 1. And yeah, the major thing, second part is that how to find the maximum element. So for that, we can use binary search as well. And we can use multiple approaches to find maximum. So you can guide me for that. And yeah, share the brute force code as well and the best optimal approach code as well.

---
You're thinking in the right direction that we need to **find a speed**, but the sum/average approach doesn't work here.(minimum banana per hour we need to find)

### Complexity

**Brute force:**

```text
O(max(piles) × n)
```

**Optimal:**

```text
O(n log(max(piles)))
```

Space:

```text
O(1)
```

### Why average doesn't work

For:

```text
[3, 6, 7, 11], h = 8
```

Average is `27 / 8 = 3.375 → 4`.

Here `4` happens to be the answer, but that's not guaranteed. The distribution of bananas among piles matters because **each pile takes a separate hour chunk**, and Koko cannot combine leftovers between piles.

### Brute Force

```javascript
function minEatingSpeed(piles, h) {
    const maxSpeed = Math.max(...piles);

    for (let speed = 1; speed <= maxSpeed; speed++) {

        let hours = 0;

        for (const pile of piles) {
            hours += Math.ceil(pile / speed);
        }

        if (hours <= h) {
            return speed;
        }
    }
}
```

### Optimal — Binary Search on Answer

```javascript
function minEatingSpeed(piles, h) {

    let left = 1;
    let right = Math.max(...piles);

    while (left < right) {

        const speed = Math.floor((left + right) / 2);

        let hours = 0;

        for (const pile of piles) {
            hours += Math.ceil(pile / speed);
        }

        if (hours <= h) {
            right = speed;
        } else {
            left = speed + 1;
        }
    }

    return left;
}
```

### ⭐ Notebook key idea

```text
Binary Search on Answer

Search space = possible answer values
1 → max(piles)

For each candidate:
    check if it satisfies the condition

Works → move left
Doesn't work → move right

Goal → find minimum valid answer
```

And importantly, **we don't need to sort the array**. We only need `max(piles)` to establish the search range.

