# Middleware - The server's security checkpoint 
- Think of middleware as everything that happens between the user and the server when a request is made.
    - When someone makes a request to your server is goes something like this:
    > Client --> Middleware --> Route Handler --> Response
    - If middleware blocks it, the request never reaches your server.

# Why middleware exists
- Without middleware:
    - Malformed request can crash your server.
    - An attacker can:
        - Send hugh payloads
        - Send invalid JSON
        - Spam endpoints
        - Probe for weaknesses 
- Middleware allows you to:
    - Inspect
    - Validate
    - Reject early 

# Simple Middleware Example 
- let's say you want to log who is making a request to your server:
````
    app.use((req, res, next) =>{
        console.log(req.ip);
        next();
    })
```` 

- Whats happening?
    - req --> incoming request
    - res --> response object 
    - next() --> "this request is allowed to continue"
- if you dont call **next()** --> request is stopped

---
- Now that we know the ip address of the user we can decide if we block it or allow it to continue
Let's block the IP

````
    app.use((req, res, next) =>{
        if(req.ip === '192.168.1.50'){
            return res.status(403).send('Blocked');
        };
        next();
    });
```` 
- Why something like this is important?
    - This is __Basic Intrusion Prevention__ attacks or bots might reuse the same ip address to scan repeatedly, with this we can check if the given ip address has made too much request to your server, 
    if it has, we can simply block it.

---
# Middleware Vs Routes

1. Route Handler:
````
    app.get('/data', (req, res) =>{
        res.send("Hello");
    });
```` 
- This will only run for the __/data__ route

2. Middleware:
````
    app.use((req, res, next) =>{
        //code here
    });
```` 
- This will run for every request regardless of the route, this is perfect because it help us with:
    - security
    - Logging
    - Validation 
    - Rate limiting

# Real-World Security Stack
- In a production server you might have middleware that checks for:
    1. Request size limiter
    2. JSON Validation
    3. Authentication Check 
    4. Rate limiter
    5. IP Reputation Filter
    6. Error Handler
- Each of these layer will reduce the risk of your server crashing.
