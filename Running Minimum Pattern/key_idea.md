Given an array:

```
prices = [7,1,5,3,6,4]
```

You may buy **one** stock and sell **one** stock later.

Return the maximum profit.

Output:

```
5
```

because:

```
Buy at 1
Sell at 6

Profit = 5
```

If no profit is possible:

```
return 0
```

Example:

```
prices = [7,6,4,3,1]

Output:
0
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

### Hint

Ask yourself:

```
Should I remember the minimum price seen so far?
```

### My Answer -
```
Pattern:  Array traverse 
Why:  just need to traverse array 
Brute Force Complexity: 0(n^2) 
Optimal Data Structure:  N/A 
Optimal Approach:  Array traverse and keep minimum values and keep calculating profit using minimum values and get max profit 
Time Complexity: 0(n) 
Space Complexity: 0(1)
```
### Review

call it:

```
One Pass Array Traversal
```

or

```
Running Minimum Pattern
```

This isn't an official named pattern like Kadane or Two Pointers, but it's a very common interview technique.

```
Need to know the minimum price seen so far to calculate the maximum profit at each day.
```

That's the key insight.

### Brute Force

```
O(n²)
```

✅ Correct.

```
forevery buy day
forevery sell day
calculate profit
```

---

### Optimal Approach

You wrote:

```
keep minimum values and keep calculating profit
```

✅ Perfect.

That's exactly what the optimal solution does.

---

## Dry Run

```
prices= [7,1,5,3,6,4]
```

Start

```
minPrice = 7
maxProfit = 0
```

---

Day 2

```
price = 1

minPrice = 1
```

---

Day 3

```
price = 5

profit = 5 - 1 = 4

maxProfit = 4
```

---

Day 4

```
price = 3

profit = 3 - 1 = 2

maxProfit = 4
```

---

Day 5

```
price = 6

profit = 6 - 1 = 5

maxProfit = 5
```

---

Day 6

```
price = 4

profit = 4 - 1 = 3

maxProfit = 5
```

Return

```
5
```

---

# Pattern Recognition Note

Add this to your notebook:

```
Best Time to Buy and Sell Stock

Pattern:
Running Minimum (One Pass Array Traversal)

Recognition Clues:
- Buy once
- Sell once
- Maximum profit
- Need smallest value before current element

Maintain:
minPrice
maxProfit

At every element:
profit = currentPrice - minPrice

Update:
minPrice = min(minPrice, currentPrice)
maxProfit = max(maxProfit, profit)

Time:
O(n)

Space:
O(1)
```

---

## One Small Improvement

You wrote:

```
Optimal Data Structure: N/A
```

✅ That's actually the correct answer.

Sometimes the best solution doesn't need a special data structure.

It just needs **two variables**:

```
minPrice
maxProfit
```

Here is the optimal **O(n)** solution.

```jsx
function maxProfit(prices) {

let minPrice=prices[0];
let maxProfit=0;

for (let i=1;i<prices.length;i++) {

// Update minimum buying price
minPrice = Math.min(minPrice,prices[i]);

// Calculate profit if sold today
const profit = prices[i]-minPrice;

// Update maximum profit
maxProfit = Math.max(maxProfit,profit);
    }

return maxProfit;
}

console.log(maxProfit([7,1,5,3,6,4]));// 5
console.log(maxProfit([7,6,4,3,1]));// 0
```

---

## Dry Run

```
prices= [7,1,5,3,6,4]
```

| Price | minPrice | Profit | maxProfit |
| --- | --- | --- | --- |
| 7 | 7 | 0 | 0 |
| 1 | 1 | 0 | 0 |
| 5 | 1 | 4 | 4 |
| 3 | 1 | 2 | 4 |
| 6 | 1 | 5 | 5 |
| 4 | 1 | 3 | 5 |

Return:

```
5
```

## Even Cleaner Version

```jsx
function maxProfit(prices) {
  let minPrice = Infinity;
  let maxProfit = 0;

  for (const price of prices) {
    minPrice = Math.min(minPrice, price);
    maxProfit = Math.max(maxProfit, price - minPrice);
  }

  return maxProfit;
}
```

I personally prefer this version because:

- No special handling for the first element.
- Cleaner code.
- Easy to remember in interviews.
