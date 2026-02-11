![[Pasted image 20260211193337.png]]

|**Feature**|**Express.js**|**Axios**|
|---|---|---|
|**Role**|Web Application Framework|HTTP Client Library|
|**Main Job**|**Receives** requests and sends responses.|**Sends** requests and receives responses.|
|**Environment**|Server-side (Node.js).|Client-side (Browser) & Server-side.|
|**Key Capability**|Routing, Middleware, Server Logic.|Data fetching, API calls, Interceptors.|
|**Analogy**|The **Waiter** who takes your order and brings food.|The **Customer** who places the order.|
![[Pasted image 20260211193539.png]]![[Pasted image 20260211193549.png]]![[Pasted image 20260211193705.png]]
### `app.get('/', (req, res) => { ... })`

- **`app.get`**: This tells the server to watch for an **HTTP GET request**. This is the standard request a browser sends when you type a URL into the address bar.
    
- **`'/'`**: This is the **path** (the "root" or home page). It means this code will only trigger when someone visits the base URL of your server (e.g., `http://127.0.0.1:3000/`).
    
- **`(req, res)`**: These are two objects provided by Express:
    
    - `req` (Request): Contains information about the incoming call from the user.
        
    - `res` (Response): Contains the tools you use to send something back to the user.
        

### `res.end('Hello, World!\n')`

- **The Action**: This line actually sends the text **"Hello, World!"** back to the user's browser or tool (like Axios).
    
- **Closing the Connection**: The `.end()` method tells the server that the response is complete and it can "hang up" the connection.

![[Pasted image 20260211193838.png]]

|**Feature**|**/ (The Root)**|**/question (The Sub-path)**|
|---|---|---|
|**Common Name**|The Home or Index route.|A specific functional route.|
|**Triggered by**|`http://127.0.0.1:3000/`|`http://127.0.0.1:3000/question`|
|**Logic**|Simple: It just sends back "Hello, World!".|Complex: It looks for extra data in the URL (parameters).|
|**Visual Ref**|Seen in Line 14 of both images.|Seen in Line 18 of the second image.|


``` JAvaSCript
// 1. IMPORTING THE MODULE
// Load the express module so we can use its functions
const express = require('express');

// 2. SERVER SETTINGS
// Define where the server will live (your own computer) and on which 'port'
const hostname = '127.0.0.1';
const port = 3000;

// 3. INITIALIZATION
// Create an instance of an Express application
const app = express();

// 4. START THE SERVER
// Tell the app to start 'listening' for visitors at the specified address and port
app.listen(port, hostname, () => {
    console.log(`Server running at http://${hostname}:${port}/`);
});

// 5. THE HOME ROUTE ('/')
// This handles basic requests to the main page
app.get('/', (req, res) => {
    // Simply send back a plain text greeting and end the response
    res.end('Hello, World!\n');
});

// 6. THE QUESTION ROUTE ('/question')
// This route is more advanced; it looks for data sent by the user
app.get('/question', (req, res) => {
    // Create a URL object to easily parse information from the request
    const requestUrl = new URL(req.url, `http://${req.headers.host}`);
    
    // Look for a specific piece of data in the URL called 'q' (e.g., /question?q=something)
    const nameValue = requestUrl.searchParams.get('q');

    // Check if the user actually provided a value for 'q'
    if (nameValue != null) {
        console.log('Info-> ' + nameValue); // Log what they typed to the server console

        // Logic: Respond based on how long the user's input is
        if (nameValue.length < 10) {
            // If it's short, encourage them to type more
            res.end('Keep on typing\n');
        } else {
            // If it's 10 characters or longer, tell them to stop
            res.end('That\'s enough stop!!!!\n');
        }
    } else {
        // If they visited /question but didn't provide 'q', just say hello
        res.end('Hello, World!\n');
    }
});
```

![[Pasted image 20260211194454.png]]![[Pasted image 20260211194512.png]]![[Pasted image 20260211194626.png]]
### . Solving the "CORS" Problem (Slide 35)

This is a critical step for when you start using **Axios**.

- **The Problem**: Browsers have a security feature called **Cross-Origin Resource Sharing (CORS)**. By default, a browser will block a website (like a local file or another domain) from talking to your Express server for security reasons.
    
- **The Solution**: You can "tell" your server to allow these connections by adding the `cors` package.
    
- **How to add it**:
    
    1. Import it: `const cors = require('cors');`.
        
    2. Apply it to your app: `app.use(cors());`.