**When to use:**

Sorted input OR answer lies in a monotonic search space.

**Common problems:**

- Search in rotated array
- First/last occurrence
- Peak element
- Allocate books / painters partition (binary search on answer)

**Key idea:**

Search mid, eliminate half of the search space.

## When to THINK Binary Search (Interview Trigger)

Use Binary Search when you see:

✅ **Sorted data** (array, implicit range, answers space)

✅ **Monotonic behavior**

- true → false
- false → true
- increasing / decreasing
    
    ✅ **“Minimum / Maximum such that condition holds”**
    
    ✅ **Search space is numeric**
    
- index
- value
- time
- speed
- capacity

📌 Interview keyword triggers:

> “first”, “last”, “minimum”, “maximum”, “at least”, “at most”,

## MASTER Binary Search Template 
```javascript
while (low <= high) {
const mid =Math.floor((low + high) /2);

if (arr[mid] === target) {
return mid;
    }elseif (arr[mid] < target) {
        low = mid +1;
    }else {
        high = mid -1;
    }
}
return -1;
```

> 
> “smallest possible”, “largest possible”
>
