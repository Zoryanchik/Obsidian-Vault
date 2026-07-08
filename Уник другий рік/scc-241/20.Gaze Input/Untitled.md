![[Pasted image 20251223131833.png]]![[Pasted image 20251223131846.png]]![[Pasted image 20251223131904.png]]### 1. Gaze as an Input Device (CMR Matrix Context)

While a standard mouse measures **Displacement (dP)**, gaze is a complex input type that traditionally attempts to track **Position (P)** to determine exactly where a user is looking.

- **Gaze Pointing vs. Mouse Pointing:** Gaze is faster and requires less effort than using a mouse, but it lacks a built-in "click" mechanism.
    
- **The "Midas Touch" Problem:** A major challenge in gaze input where every object the user looks at is accidentally triggered. Designers must use specific spatial or temporal conditions (like a "dwell time") to confirm a selection.
    
- **Accuracy vs. Precision:** Eye tracking is often imprecise due to natural eye jitter (fixations aren't perfect points).
### 2. Multi-Modal Interaction: "Eye-Hand Symbiosis"

Modern HCI research (including work done at **Lancaster University**) focuses on combining gaze with other inputs to use their relative strengths66666666:

|**Input Type**|**Role in Interaction**|**Key Benefit**|
|---|---|---|
|**Gaze**|**Selection & Pre-selection** 7777|Speed and reach8.|
|**Hands/Touch**|**Manipulation** 9999|Accuracy and expressivity10101010.|

- **Gaze-Touch:** Zooming occurs at the specific point where you are looking11.
    
- **Gaze-Pinch:** Used in systems like **Apple's Vision Pro**, where gaze selects a target and a hand pinch executes the action12. This allows for seamless interaction from close-up objects to those far away13.

### 3. Advanced Gaze Movement Types

Beyond simple pointing (fixations), there are three critical types of natural eye movements that HCI researchers use to solve problems like motion artifacts:

1. **Smooth Pursuit Eye Movement (SPEM):** Enables us to focus on moving objects.
    
    - **"Pursuits" Selection:** A technique where an object is selected because the eye's movement path matches the object's movement path. This requires **no calibration**.
        
2. **Vergence:** Enables focusing on objects at different depths.
    
3. **Vestibulo-Ocular Reflex (VOR):** Stabilizes the eyes when the head or body moves.
    

---

### 4. Head and Eye Coordination

In Virtual Reality (VR) or Head-Mounted Displays (HMDs), gaze is the combination of eye, head, and body direction.

- **Comfortable Range:** Most natural eye-in-head rotation is limited to approximately **20 degrees** from the center.
    
- **Gaze Shifts:** When looking at a target far away, the eye reaches the target first, and the head begins to follow shortly after. The head usually does not follow the entire way, leaving the eyes slightly off-center.