```
let arrTypes = [0, 1, -1, "hello", "", null, undefined, [], {}];

const truthyOrFalsy = function (val) {
  return val ? "T" : "F";
};

let str = arrTypes.map((v) => truthyOrFalsy(v)).join("");
console.log("Str:", str);

```

### 🔍 Step 1: The array

`arrTypes` contains a mix of different types and values:

`[0, 1, -1, "hello", "", null, undefined, [], {}]`

condition ? valueIfTrue : valueIfFalse

### 🧩 2. How it works in your function

In your function:

`const truthyOrFalsy = function (val) {   return val ? "T" : "F"; };`

Here’s what happens step by step:

1. JavaScript looks at the **condition** → `val`
    
2. It evaluates whether `val` is **truthy** or **falsy**.
    
3. If `val` is **truthy**, it returns the **first value** after the question mark → `"T"`
    
4. If `val` is **falsy**, it returns the **second value** after the colon → `"F"`


### 🧮 3. The long form (if–else equivalent)

You could write the same logic like this:

`const truthyOrFalsy = function (val) {
if (val) { 
return "T";   }
else {    
return "F";   } };`

The ternary operator just makes this shorter and cleaner.

### 🧠 1. How JavaScript actually reads `if (val)`

When you write:

`if (val) {   // do something }`

JavaScript **automatically converts** whatever `val` is into a **Boolean** behind the scenes — as if it did this:

`if (Boolean(val) === true)`

So when you say “we’re not actually saying `equals true`,” that’s true in _syntax_, but JavaScript is _doing it internally_ for you.

## 🔍 Step-by-step explanation

### **1️⃣ `arrTypes.map(...)`**

- The `.map()` method **loops over every element** in the array `arrTypes`.
    
- For each element `v`, it calls the function `(v) => truthyOrFalsy(v)`  
    → meaning it passes each value into `truthyOrFalsy`.
let str = arrTypes.map((v) => truthyOrFalsy(v)).join("");
console.log("Str:", str);
### **2️⃣ `.join("")`**

- `.join("")` takes all elements of the array and **concatenates them into one string**.
    
- The `""` (empty string) means “don’t put anything between them.”
'

another example 
let numbers = [1, 2, 3];

let doubled = numbers.map((num) => num * 2);

console.log(doubled);
'