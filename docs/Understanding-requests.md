# Understanding Express Requests

- Right now, your server reponds, but it doesn't know anything about who is talking to it. In the next section we're going to modify the **server.js** file to be able to see who is making request to the server and do different things with the infomratino we get.

 ----

 - STEP 1:
    - When someone talks to your sever, they send a request. 
    The request contains:
        - Where they come from (IP address)
        - What they want (URL)
        - What action they ask to perform (GET, POST, DELETE, PUT)
    Your sever can see all of this.

    - Modify the **server.js** file, right now the file should look like this: 
    ````
        const express = require('express');
        const app = express();

        const PORT = 8000;
        const IP = '0.0.0.0';

        app.get('/', (req, res) => {
            res.send("Hello from my server")
        })

        app.listen(PORT, IP, () => {
            console.log(`Server is runing on port ${PORT}`);
        });
    ```` 
    add the following line to your GET request
    ````
            console.log("Someone made a request");
    ````


    Your **server.js** file shold look like this now
    ````
        const express = require('express');
        const app = express();

        const PORT = 8000;
        const IP = '0.0.0.0';

        app.get('/', (req, res) => {
            console.log("Someone made a request");

            res.send("Hello from my server")
        })

        app.listen(PORT, IP, () => {
            console.log(`Server is runing on port ${PORT}`);
        });
    ```` 

    - Run your sever with the new code, use the terminal or a web browser to make a request, when you do, you should see **Someone made a request** on the console
----
    ##What we learned with this?
     - This is logging, blocking, and alerts work in, when someone makes a request with an unknown IP address or other parameters, you can block it, allow it and log it, trigger an alert.
     Your code now knows in a simple way when someone contacts and makes a request. Something to have in mind, Every request can trigger code 

---- 

- STEP 2 
    ##Who is talking to my server?

    - Now lets modify the file again to add one line of code that will let us see the ip address of who is making a request to our server.
    Add the followinf like to your get path on your file.
    ```` app.get('/', (req, res) => {
            console.log("Request from IP:", req.ip);

            res.send("Hello from my server")
        })
    ```` 
    This line will allow us to see the IP address of the device that made a request to our server.
    Run your server with the new code, use the terminal or a web browser to make a request to the server, you should see the IP address from the device that make the request.

    - ### Something important to know
        - Attackers or users can change their IP addresses, this will allow them to __hide__ their original IP address. Some of the methods they use are: 

        1 - **Proxies**: An attacker will make the request to a proxy server first, then the proxy server will forward that request to the server, this will log the proxy's IP address instead of the original user that made the request.

        2 - **VPNs (Virtual Private Network)**: Similar to proxy servers, a VPN creates an ecrypted tunnel to a remote server. All the traffic the user generates will originate from a different location

        3 - **IP Spoofing**: In a more sophisticated network-level attacks like DDOS. attackers can forge the __Source IP__ in the IP packet header.

        4 - **HTTP Header Manipulation**: If the server is behind a load balancer or a proxy server, attackers can sometimes __fake__ thier IP by sending custom headers.

    - Your server can know at a simple level identify where traffic comes from and decide what to do, wheather trust or block it.
    In essence, this is the foundation for 
        - Firewalls
        - Intrusion Detection/Prevention
        - Rate Limiting
----
- STEP 3
    - Let's add more code to our server file to get some more information about the request, modify your server file to look like this: 
    ````const express = require('express');
        const app = express();

        app.get('/', (req, res) => {
            console.log('IP:', req.ip);
            console.log('Method:', req.method);
            console.log('URL:', req.url);

            res.send('Hello from my server');
        });

        app.listen(3000, () => {
            console.log('Server running on port 3000');
        });
    ````
    - Run your server again and make a request, in the console you should see the IP address of the device who made the request, the __method__ they use (GET, POST, PUT, DELETE), and the __URL__ of the request. When you make a request you should see something like this: 
    ````Server is runing on port 8000
        IP: 192.168.0.18
        Method: GET
        URL: /
    ````
----
    ##What we learned with this?
    - Now with our new modify file, we can see:
        - Who is talking to the server
        - What method they are using to talk to your server
        - What are they requesting from the server
    this allows us to, depending on the request method do diffrent stuff as the name suggests, we can request information from the server (GET), create new information in the server (POST), update existing information in the server (PUT), and delete information in the server (DELETE). Also depending on who is making the request, we can decide to block it or allow it into our network or server.  

    - You should now understand the sentence:
        > "A request contains an IP, a method, and a URL, and my server can see all of that.
    