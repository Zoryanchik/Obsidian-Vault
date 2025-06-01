![[Pasted image 20250325181129.png]]![[Pasted image 20250325181329.png]]![[Pasted image 20250325181704.png]]![[Pasted image 20250325182013.png]]
The `target` attribute specifies where to open the linked document. `target="_blank"` opens the linked document in a new tab or window
a target="_blank" href="https://freecatphotoapp.com">cat photos</a>
# Step 17

In previous steps you used an anchor element to turn text into a link. Other types of content can also be turned into a link by wrapping it in anchor tags.

Here is an example of turning an image into a link:

Example Code

```html
<a href="example-link">
  <img src="image-link.jpg" alt="A photo of a cat.">
</a>
```

Turn the image into a link by surrounding it with necessary element tags. Use `https://freecatphotoapp.com` as the anchor's `href` attribute value.
Before adding any new content, you should make use of a `section` element to separate the cat photos content from the future content.

The `section` element is used to define sections in a document, such as chapters, headers, footers, or any other sections of the document. It is a semantic element that helps with SEO and accessibility.

Example Code

```html
<section>
  <h2>Section Title</h2>
  <p>Section content...</p>
</section>
```

Take your `h2`, `p`, and anchor (`a`) elements and nest them in a `section` element.

Submit and go to next challenge (Ctrl + Enter)

Congratulations, your code passes. Submit your code to continue.

"You're a wizard, Harry!"

25% complete

---

Learn HTML by Building a Cat Photo App

25% complete

---

Reset

Navigated to Step 18
![[Pasted image 20250325185228.png]]
The `<a>` tag is used to create hyperlinks, meaning it is typically used to link to other web pages or resources. In **Step 24**, you're only required to display an image, not make it a clickable link.
![[Pasted image 20250325190308.png]]
Use a <figure> element to mark up a photo in a document, and a <figcaption> element to define a caption for the photo:

<figure>  
  <img src="pic_trulli.jpg" alt="Trulli" style="width:100%">  
  <figcaption>Fig.1 - Trulli, Puglia, Italy.</figcaption>  
</figure>

figure is the things taht holds phot document etc

The code for an ordered list (`ol`) is similar to an unordered list, but list items in an ordered list are numbered when displayed.

