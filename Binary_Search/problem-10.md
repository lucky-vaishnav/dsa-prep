### **Minimum Number of Days to Make m Bouquets**

```text
bloomDay = [1,10,3,10,2]
m = 3
k = 1

Output:
3
```

Meaning:

* Need to make **3 bouquets**
* Each bouquet needs **1 adjacent flower**
* `bloomDay[i]` tells us when that flower blooms.

Think about:

* Pattern
* Why?
* Search space
* How would you validate a candidate day?
* Time complexity
* Space complexity

**Hint:** Same **Binary Search on Answer** pattern as Koko, Shipping, and Split Array.

---
### My Thought-
Yeah, so for question number one, minimum number of days to make a bouquet, so we will be using the binary search on the answer pattern because it is similar to the problem we have already worked on, the coconut banana and the split array. And we will be calculating the left and right pointer. So right pointer will be the maximum number of bouquet we can make. So, and we can assume that one flower flower will be enough for that. So it will be the length of the array, the maximum bouquet, the right value. And left will be the zero on the start. And then we will loop through the array, and if the total flower is greater than or equal to k, which means that one bouquet is ready, greater or equal to k, then one bouquet is ready, and we will be incrementing the number of bouquet. And after that, we will be checking that if number of bouquet is greater than or equal to the number m, which is required for the problem, then we will be resetting the right value to mid minus one, and else the left will be mid plus one. And at the end, the answer will be the left, so we will return the left. So the problem will be time complexity will be O of n log n, and space complexity will be O of 1.

---
You're **mostly correct — 8.5/10**. The pattern and overall binary-search structure are right, but there are two important corrections.

### 1. Search range

You said:

> `left = 0`, `right = nums.length`

❌ Not quite.

The search space is **days**, so:

```text
left = minimum bloom day
right = maximum bloom day
```

For:

```text
bloomDay = [1, 10, 3, 10, 2]
```

we search:

```text
1 → 10
```

Not `0 → 5`.

### 2. Checking bouquets

Your idea is correct, but the flowers must be **adjacent**.

For a candidate day, we traverse the array:

```text
flower bloomed by candidate day?
    ↓
yes → consecutiveFlowers++

no  → consecutiveFlowers = 0
```

Whenever:

```text
consecutiveFlowers === k
```

we have one bouquet.

Then reset:

```text
consecutiveFlowers = 0
```

because those flowers are consumed by that bouquet.

### Complexity

If `n = bloomDay.length` and `D = max(bloomDay)`:

```text
Time:  O(n log D)
Space: O(1)
```

So not strictly `O(n log n)` unless the value range `D` happens to be related to `n`.

### Key pattern

```text
Candidate day
     ↓
Can we make ≥ m bouquets?
     ↓
YES → try earlier day
NO  → try later day
```

Your recognition of **Binary Search on Answer** is absolutely right.

### Brute Force — O(n × D)

```javascript
function minDays(bloomDay, m, k) {
    const n = bloomDay.length;

    if (m * k > n) {
        return -1;
    }

    const maxDay = Math.max(...bloomDay);

    for (let day = 1; day <= maxDay; day++) {

        let bouquets = 0;
        let consecutive = 0;

        for (const bloom of bloomDay) {

            if (bloom <= day) {
                consecutive++;

                if (consecutive === k) {
                    bouquets++;
                    consecutive = 0;
                }
            } else {
                consecutive = 0;
            }
        }

        if (bouquets >= m) {
            return day;
        }
    }

    return -1;
}
```

### Optimal — Binary Search on Answer

```javascript
function minDays(bloomDay, m, k) {

    const n = bloomDay.length;

    if (m * k > n) {
        return -1;
    }

    let left = Math.min(...bloomDay);
    let right = Math.max(...bloomDay);

    while (left < right) {

        const day = Math.floor((left + right) / 2);

        let bouquets = 0;
        let consecutive = 0;

        for (const bloom of bloomDay) {

            if (bloom <= day) {
                consecutive++;

                if (consecutive === k) {
                    bouquets++;
                    consecutive = 0;
                }
            } else {
                consecutive = 0;
            }
        }

        if (bouquets >= m) {
            // This day works → try earlier
            right = day;
        } else {
            // Not enough bouquets → need more days
            left = day + 1;
        }
    }

    return left;
}
```

### Notes

```text
Pattern:
Binary Search on Answer

Search space:
min(bloomDay) → max(bloomDay)

Validation:
Can we make m bouquets by this day?

YES → move left
NO  → move right

Time:
O(n log D)

Space:
O(1)
```

The **`consecutive = 0` after making a bouquet** is important because those `k` adjacent flowers have already been used.

