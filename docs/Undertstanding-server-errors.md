# Server Internal Error

- What is an internal error?
    - An internal server error or also commonly known as a __500__ error. This code means that the server encounters an unexpected condition that prvented the request to be fullfiled. In simple words, you know that there is an error, but you dont know where or why.
    
----

- Lets update the **server.js** to get an error when we make a request

````const express = require('express');
    const app = express();

    const PORT = 8000;
    const IP = '0.0.0.0';

    app.get('/', (req, res) => {
        console.log("IP:", req.ip)
        console.log("Method:", req.method)
        console.log("URL:", req.url)

        console.log(user.name);

        res.send("Hello from my server")
    })

    app.listen(PORT, IP, () => {
        console.log(`Server is runing on port ${PORT}`);
    });
````
- On this new code we added a new line that logs __user.name__ variable to the console, here this variable does not exist, therefore the server will thorw an error when you make a request.

    - Run the new file and make a request using the terminal or a web browser

    - You should see something like this in the console
        > ReferenceError: user is not defined
    after this the server will stop.

- In a nutshell, this is what happened:
    1 - Someone made a request 
    2 - Your server ran the code
    3 - JavaSvript hit something it didn't understand 
    4 - Node crashed
    5 - The server stopped responding
    This is considered an __Internal Server Error__ 

- Why Understanding how a server crashes is important?
    - Errors can expose different functionallity and files paths in the server, also, it could expose the logic of the code the server is running, 
        - if you make a request and see that the server crashes you can infer the behavior of the server code.
    - Errors can be useful to an attacker because, they can learn how the system works, this can lead to potentially causing a Denial-of-Service attack. Attackers can also craft better and targeted attacks to the server based on how it behaves with requests.

- Update the **server.js** file to be able to catch errors instead of crashing the server.
````const express = require('express');
    const app = express();

    const PORT = 8000;
    const IP = '0.0.0.0';

    app.get('/', (req, res) => {
        try{
            console.log("IP:", req.ip)
            console.log("Method:", req.method)
            console.log("URL:", req.url)
        
            console.log(user.name);
        
            res.send("Hello from my server")
        }
        catch(error){
            console.log('Something went wrong:', error.message);
            res.status(500).send("Internal Server Error")
        }
    });

    app.listen(PORT, IP, () => {
        console.log(`Server is runing on port ${PORT}`);
    });
````
In this code we added a __try__ and __catch__ statements to be able to catch the error, now instead of crashing the server we will get the message of **Something went wrong: user is not defined** becuase the user variable we use to cause the error is not defined, if you have a different error in your server it will display a different error message. When a user makes a reques, the user will see the message __Internal Server Error__, this is much better becuae it will not crash the server and it will not leak any information about the server.

## What this we learned?
- With this information we learned the critical rule of logging details internally, and showing generic errors externally.

- Why this is important?
    - This is important because for one side, users dont need to learn any technical details about the server. on the other hand, Attackers should not learn anything about how the server code works, this will make it harder for the attacker to understan the logic of the server.

