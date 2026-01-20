In this part we are going to create a server file to understand how it listens and how responds to different requests

- Before we start we need to install express, before we can install it we need to install npm (Node Package Manager) which like the name implies, is a package manager for javascript running on Node.
Learn more about npm [here](https://www.npmjs.com/): 

-------

- STEP 1
    - Create one file named **server.js**, open it and paste this code below: 
    ```text
    1 -  const express = require('express');
    2 -  const app = express();

    3 - const PORT = 8000;
    4 - const IP = '0.0.0.0';

    5 - app.listen(PORT, IP, () => {
    6 -   console.log(`Server is running on port ${PORT}`)
        });

- What does this means?

    - line 1: we "import" express to our file
    - line 2: we create an instance of express to create our server (app)
    - line 3: we define the port we want our server to listen on.
    - line 4: we define which ip address can make request to our server, 0.0.0.0 means any ip can request, you can change it to any ip you want.
    - line 5: we make our server (app) run and listen to any request from any ip address, when we run the server we will see **Server is running on port 8000** in the console 

-------

- STEP 2 
    - Run the **server.js** file 

    ```` 
        node server.js
- At this point your computer is acting like a server, listening for requests on port 8000. its doing nothing else

-------

- STEP 3
    - Talk to the server to make sure everything is running as expected.
    - On your terminal or your broswer navegate to the local host on port 8000

    ````
        curl http://localhost:8000    
        
- At this point you should see somethign like **Cannot GET** that fine we haven't told the server to respond if there are any requests made.

- NOTE: 
    - At this point we have a server running WITHOUT any instructions on what to do if a request is made, in the next step we will set up the server to respond when a request us made.

-------

- STEP 4
    -Make the server respond to requests
    - Modify your **server.js** file and add the following:
    ````
        app.get('/', (req, res) =>{
            res.send('Hello from my server!!')
        });
- Now your **server.js** file shoudl look like this
    ````
        const express = require('express');
        const app = express();

        // When someone visits /
    1 - app.get('/', (req, res) => {
            res.send('Hello from my server');
        });

        app.listen(3000, () => {
            console.log('Server running on port 3000');
        });
- line 1: On this line we added a GET route, when the user visits your server homepage is the same as visiting '/' route, when they make the request to the server they will get a responds back.

- NOTE: we use **(req, res)** this is short for **(request, response)**

 - use CTRL-C to stop the server and run it again
 - you should now see:
    ```` 
        Hello from my server

- In a nutshell:
    - When you did
    ````
        curl http://localhost:8000

- This happened:
    ````
        You → Port 3000 → Express → app.get('/') → Response

- This is the entire backend lifecycle simplified.

