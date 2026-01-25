![[Pasted image 20260119013709.png]] ![[Pasted image 20260119013838.png]]![[Pasted image 20260119013858.png]]![[Pasted image 20260119013920.png]]![[Pasted image 20260119013941.png]]## 1. Element selector

### What it does

Targets **all HTML elements of a given type**.

### Example

`p {   color: blue; }`

### HTML

`<p>Hello</p> <p>World</p>`

➡️ **ALL `<p>` elements become blue**
---

## 2. Class selector

### What it does

Targets elements with a **specific class**.

### Syntax

`.class-name { }`

### HTML

`<p class="highlight">Important</p> <p>Normal</p>`

### CSS

`.highlight {   color: red; }`

➡️ Only elements with `class="highlight"` turn red

---

## 3. ID selector

### What it does

Targets **ONE unique element** with a specific ID.

### Syntax

`#id-name { }`

### HTML

`<h1 id="main-title">Welcome</h1>`

### CSS

`#main-title {   font-size: 40px; }`
---

## 4. Attribute selector

### What it does

Targets elements based on **attributes and values**.

### Example

`[type="text"] {   border: 2px solid green; }`

### HTML

`<input type="text"> <input type="password">`![[Pasted image 20260119014307.png]]

|**Feature**|**Pseudo-class (:)**|**Pseudo-element (::)**|
|---|---|---|
|**Purpose**|Styles the _whole element_ based on **behavior/state**.|Styles a _sub-part_ of the element based on **location**.|
|**Symbol**|Single Colon (`:`)|Double Colon (`::`)|
|**Analogy**|Like a light that turns on when you flip a switch.|Like using a highlighter on just the first word of a sentence.|
### 1. The Generic Selector (Element Selector)

CSS

```
li {
    color: brown;
}
```

- **What it does:** This targets **every single** list item (`<li>`) on the entire page.
    
- **The Result:** Whether the list item is in a navigation menu, a footer, or a recipe list, it will turn brown.
    
- **When to use:** When you want a global default style for all lists.
    

### 2. The Descendant Selector (Context Selector)

CSS

```
ol li {
    color: brown;
}
```

- **What it does:** This targets list items (`<li>`), but **only** if they are inside an Ordered List (`<ol>`).
    
- **The Logic:** The space between `ol` and `li` is the key. In CSS, a space means "inside of" (descendant of).
    
- **The Result:** Numbered lists (`<ol>`) will be brown. Bulleted lists (`<ul>`) will be ignored and remain their default color.
    

### 3. The Class Descendant Selector

CSS

```
.content li {
    color: brown;
}
```

- **What it does:** This targets list items (`<li>`), but **only** if they are inside an element with the class `content`.
    
- **The Logic:** This is very specific to a section of your page. You might have a `<div class="content">` for your main article.
    
- **The Result:** Lists inside your main content area turn brown, but lists in your sidebar, header, or footer (which don't have the `.content` class) are unaffected.
![[Pasted image 20260119014837.png]]

|**Scenario**|**Conflict**|**Winner Decision Based On**|**Result**|
|---|---|---|---|
|**Left Box**|`p.greeting` vs `p`|**Specificity** (Class > Tag)|**Yellow**|
|**Right Box**|`p` vs `p`|**Order** (Last one listed)|**Green**|
![[Pasted image 20260119015147.png]]
![[Pasted image 20260119015303.png]]**1. Backgrounds Do Not Inherit** The `body` has a yellow background. The `h1` and `h2` elements do **not** inherit this property.

- **h1:** It looks yellow only because its default background is `transparent`. You are seeing the `body` background _through_ the `h1`.
    
- **h2:** It is green because the specific rule (`background: green`) paints over the transparent default.
    

**2. What actually Inherits?** In CSS, usually only **text properties** (like `color`, `font-family`, `font-size`) inherit.

- If you added `color: blue` to the `body`, the `h2` would turn blue (inheritance).
    
- The `h1` would stay red because its specific rule (`color: red`) overrides inheritance.
- 
- ![[Pasted image 20260119015310.png]]![[Pasted image 20260119015651.png]]![[Pasted image 20260119015827.png]]![[Pasted image 20260119015833.png]]![[Pasted image 20260119015908.png]]![[Pasted image 20260119015918.png]]![[Pasted image 20260119015933.png]]![[Pasted image 20260119020009.png]]![[Pasted image 20260119020024.png]]![[Pasted image 20260119020129.png]]![[Pasted image 20260119020152.png]]![[Pasted image 20260119020201.png]]![[Pasted image 20260119020245.png]]