The **Array Reversal Pattern** looks simple, but interviewers love it because it teaches:

```
Two Pointers
In-place modification
Space optimization
Array manipulation
String manipulation
Linked List reversal foundation
```

Many advanced problems are just variations of reversal.

---

# 1. Core Idea

Given:

```
[1,2,3,4,5]
```

Need:

```
[5,4,3,2,1]
```

---

Most beginners think:

```
Create another array
```

But interviewers usually want:

```
In-place reversal
```

Meaning:

```
No extra array
```

---

# 2. Pattern Recognition

Think reversal pattern when you see:

```
Reverse array
Reverse string
Rotate array
Palindrome
Swap from ends
Two pointers moving inward
```

---

# 3. Brute Force

Create new array.

```
function reverse(nums){
let result= [];

for(let i=nums.length-1;i>=0;i--){
result.push(nums[i]);
    }

return result;
}
```

---

Complexity

```
Time  : O(n)

Space : O(n)
```

---

Usually not preferred.

---

# 4. Optimal Pattern (Two Pointers)

This is the actual Array Reversal Pattern.

---

Initial:

```
[1,2,3,4,5]

 L       R
```

---

Swap

```
[5,2,3,4,1]

   L   R
```

---

Swap

```
[5,4,3,2,1]

     LR
```

Done.

---

# Template

```
function reverse(nums){

let left=0;
let right=nums.length-1;

while(left < right){

        [nums[left],nums[right]]
         =
        [nums[right],nums[left]];

left++;
right--;
    }

return nums;
}
```

---

Complexity

```
Time  : O(n)

Space : O(1)
```

Best possible.

---

# 5. Why Does This Work?

You asked this earlier.

---

This line:

```
[nums[left],nums[right]]
=
[nums[right],nums[left]];
```

works because:

JavaScript evaluates:

```
[nums[right],nums[left]]
```

FIRST.

---

Example:

```
left=0
right=4

nums= [1,2,3,4,5]
```

JS first stores:

```
[5,1]
```

temporarily.

Then assigns:

```
nums[0]=5
nums[4]=1
```

---

No value is lost.

---

Equivalent to:

```
let temp=nums[left];

nums[left]=nums[right];

nums[right]=temp;
```

---

# 6. Template to Memorize

This is the generic reversal template.

```
let left=0;
let right=arr.length-1;

while(left < right){

swap(left,right);

left++;
right--;
}
```

---

You'll reuse this everywhere.

---

# 7. Palindrome Problems

Example:

```
racecar
```

---

Use same pattern.

```
while(left<right){

if(s[left]!==s[right])
return false;

left++;
right--;
}
```

---

This is why palindrome is considered a reversal variation.

---

# 8. Reverse String

LeetCode 344

```
function reverseString(s){

let left=0;
let right=s.length-1;

while(left < right){

        [s[left],s[right]]
         =
        [s[right],s[left]];

left++;
right--;
    }
}
```

---

# 9. Reverse Only Part Of Array

Example:

```
Reverse indexes 2 to 5
```

---

Template becomes:

```
function reverse(arr,start,end){

while(start<end){

        [arr[start],arr[end]]
=
        [arr[end],arr[start]];

start++;
end--;
    }
}
```

Very important.

Used in:

```
Rotate Array
Next Permutation
Reverse Words
```

---

# 10. Rotate Array (Major Interview Question)

LeetCode 189

Example:

```
[1,2,3,4,5,6,7]

k = 3
```

Result:

```
[5,6,7,1,2,3,4]
```

---

Magic solution:

Reverse whole array.

```
7 6 5 4 3 2 1
```

Reverse first k.

```
5 6 7 4 3 2 1
```

Reverse remaining.

```
5 6 7 1 2 3 4
```

Done.

---

Interview favorite.

---

# 11. Reverse Words In String

Example:

```
"I love coding"
```

Output:

```
"coding love I"
```

Uses reversal repeatedly.

### Approach 1 (Easy)

Split and reverse:

```
s.split(" ").reverse().join(" ");
```

This doesn't really use the Array Reversal Pattern directly.

### Approach 2 (Interview Style - In-place Reversal)

#### Step 1: Reverse entire string

```
I love coding

↓

gnidoc evol I
```

---

#### Step 2: Reverse each word individually

Reverse:

```
gnidoc → coding
```

String becomes:

```
coding evol I
```

Reverse:

```
evol → love
```

String becomes:

```
coding love I
```

Reverse:

```
I → I
```

Final:

```
coding love I
```

Example code:

```jsx
function reverse(arr,start,end) {
while (start<end) {
        [arr[start],arr[end]]=
        [arr[end],arr[start]];

start++;
end--;
    }
}

function reverseWords(str) {

let arr=str.split('');

// reverse entire string
reverse(arr,0,arr.length-1);

let start=0;

for (let end=0;end<=arr.length;end++) {

if (end===arr.length||arr[end]===' ') {

reverse(arr,start,end-1);

start=end+1;
        }
    }

return arr.join('');
}

console.log(reverseWords("I love coding"));
```

### Senior Developer Perspective

If interviewer asks:

```
Reverse words in a string
```

I'd answer in this order:

#### Approach 1

```
s.split(" ").reverse().join(" ");
```

Mention:

```
Simple
Readable
Production-friendly
O(n) space
```

---

#### Approach 2

Then say:

```
If interviewer wants optimal space,
we can use in-place reversal.
```

and write the reversal solution.

---

# 12. Linked List Reversal

The famous:

LeetCode 206

---

Array reversal teaches:

```
left
right
swap
move inward
```

---

Linked list reversal teaches:

```
prev
curr
next
```

Same idea.

---

# 13. Recognition Pattern

Think Array Reversal when:

```
Reverse
Swap ends
Palindrome
Rotate
Reverse words
Two pointers inward
```

---

# Must Practice Problems

## Easy

```
344 Reverse String
125 Valid Palindrome
```

---

## Medium

```
189 Rotate Array
151 Reverse Words in a String
680 Valid Palindrome II
```

---

## Foundation for Future

```
206 Reverse Linked List
92 Reverse Linked List II
```

---

# Interview Notes

```
Array Reversal Pattern

Core Idea:
Swap from both ends.

Pattern:
left = 0
right = n - 1

while(left < right)
{
   swap
   left++
   right--
}

Time:
O(n)

Space:
O(1)

Recognition:
Reverse
Palindrome
Rotate Array
Reverse String
Swap Ends

Most Important Problems:
344 Reverse String
125 Valid Palindrome
189 Rotate Array
151 Reverse Words
```

---

### Connection To Other Patterns

This pattern leads directly into:

```
Two Pointer Pattern
```

because array reversal is actually the simplest and most fundamental Two Pointer problem. Understanding reversal deeply makes palindrome, container-with-most-water, 3Sum, and many other interview problems much easier.
