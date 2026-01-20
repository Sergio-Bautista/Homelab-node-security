In this part we are going to create a server file to understand how it listens and how responds to different requests

- Before we start we need to install express, before we can install it we need to install npm (Node Package Manager) which like the name implies, is a package manager for javascript running on Node.
Learn more about npm [here](https://www.npmjs.com/): 


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

- STEP 2 
    - Run the **server.js**