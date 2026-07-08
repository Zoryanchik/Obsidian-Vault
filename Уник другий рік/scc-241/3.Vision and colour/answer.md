### **1️⃣ Why are desktop monitors usually set up so they don’t extend over more than ~40° of the user’s visual field?**

**Reason:**  
Our **visual acuity** (ability to see fine detail) drops off rapidly outside the central ~20° of our visual field.  
Beyond ~40°, **peripheral vision** becomes:

- Less sensitive to detail,
    
- Less effective at color discrimination,
    
- More sensitive to motion than to shape or text.
    

So if a monitor spans too wide an angle:

- You can’t comfortably see or focus on everything at once.
    
- You’d need to move your head or eyes constantly, increasing fatigue.
    
- Text and UI elements on the edges become harder to read.
    

✅ **In short:**  
Monitors are limited to about 40° so that all displayed information stays within the part of the visual field where human vision is sharp and comfortable.

---

### **2️⃣ Early WWW hyperlinks were blue — was that a good choice? What are limitations of blue text?**

**Why it seemed good initially:**

- Blue stands out from black body text (high contrast).
    
- It was rarely used in print, so it clearly indicated “this is a link.”
    

**Limitations of blue for highlighting text:**

- The human eye has **fewer blue-sensitive cones (S-cones)** — only about 5–10% of all cones.
    
- S-cones are concentrated **away from the fovea** (the very center of vision).  
    → So when reading small blue text, our eyes literally have trouble focusing on it clearly.
    
- Blue text also has **lower luminance contrast** on white backgrounds.
    
- On some screens, blue appears darker and thinner than other colors.
    

✅ **In short:**  
Blue links are recognizable but not ideal for readability — small blue text is hard to focus on, especially for people with vision deficiencies or older eyes.

---

### **3️⃣ Do we have better color vision in the fovea or in the periphery?**

**Answer:**  
👉 **Better color vision in the fovea.**

**Why:**

- The **fovea** (center of the retina) is densely packed with **cone cells** (red, green, blue sensitive).
    
- The **periphery** has mostly **rod cells**, which are great for motion and dim light, but **color-blind**.
    

✅ **In short:**  
Color discrimination and fine detail are best in the **fovea**; the **periphery** is mostly for motion detection and brightness, not color.

---

### **4️⃣ What color is at the center of an RGB cube?**

The RGB color cube represents all possible colors by mixing **Red, Green, and Blue** (each 0–255).

At the **center**, all three colors are equal:  
👉 **R = G = B = 0.5 (or 128, 128, 128)**

That produces **neutral gray** — halfway between black and white.

✅ **In short:**  
**The center of the RGB cube = gray** (equal red, green, and blue).

---

### **5️⃣ How can we ensure that people with color vision deficiency can discriminate map regions?**

**Strategies:**

1. **Don’t rely on color alone** — use:
    
    - Patterns (stripes, dots)
        
    - Texture
        
    - Shape or boundaries
        
2. **Use color palettes tested for color blindness**, e.g.:
    
    - **ColorBrewer** palettes (“ColorBrewer2.org”)
        
    - Avoid confusing combinations like **red–green** or **blue–purple**.
        
3. **Ensure luminance contrast** (lightness differences), not just hue differences.
    
    - Even in grayscale, regions should still be distinguishable.
        
4. **Test designs** using color-blindness simulators (e.g., for protanopia, deuteranopia).
    

✅ **In short:**  
Use redundant visual cues (shape + brightness + tested colors) to make maps readable for everyone, including those with color vision deficiencies.