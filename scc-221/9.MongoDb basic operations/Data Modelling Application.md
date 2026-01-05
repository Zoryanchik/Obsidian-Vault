![[Pasted image 20260105185846.png]]![[Pasted image 20260105185919.png]]![[Pasted image 20260105185932.png]]In SQL, you write a command to create a constraint. In NoSQL (like MongoDB), the constraint itself is just another JSON object. You are essentially using JSON to police your JSON.

![[Pasted image 20260105190139.png]]
![[Pasted image 20260105190155.png]]![[Pasted image 20260105190342.png]]### 2. The Relationships (The Lines)

The lines connecting the boxes tell the "story" of how the data interacts. The symbols at the ends of the lines (Crow's feet, bars, circles) define the rules (constraints).

**User Interactions**

- **User creates Playlist:** A single **User** can create many **Playlists**, but each Playlist belongs to exactly one User.
    
- **User logs Play:** A **User** generates many **Play** records (listening history). Each Play record belongs to one User.
    

**Music Structure**

- **Artist releases Album:** An **Artist** can release many **Albums**. An Album belongs to one Artist.
    
- **Artist writes Song:** An **Artist** writes many **Songs**.
    
- **Album contains Song:** An **Album** contains many **Songs**, but a Song typically belongs to one Album (based on this specific diagram's notation).
    

**Song Connections**

- **Playlist contains Song:** This is a **Many-to-Many** relationship. A **Playlist** can have many **Songs**, and a single **Song** can appear in many different Playlists.
    
- **Play of Song:** Each **Play** log corresponds to exactly one **Song**. (e.g., "User X listened to Song Y at 12:00 PM").
    
- **Song has Lyrics:** This is a **One-to-One** (or optional one) relationship. A **Song** has one set of **Lyrics**.
    

### Summary of the Flow


![[Pasted image 20260105190544.png]]![[Pasted image 20260105190610.png]]![[Pasted image 20260105190629.png]]![[Pasted image 20260105190643.png]]![[Pasted image 20260105190853.png]]![[Pasted image 20260105191007.png]]![[Pasted image 20260105191153.png]]![[Pasted image 20260105191220.png]]![[Pasted image 20260105191410.png]]![[Pasted image 20260105191541.png]]![[Pasted image 20260105191740.png]]![[Pasted image 20260105191835.png]]