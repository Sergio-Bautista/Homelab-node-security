# Attack simulation
- We will perfom a controlled, local only attack simulation that will help us understand the mechanics of what we are learning

# !!IMPORTANT!!
     - WE ARE ATTACKING OUR OWN SERVER, ON LOCALHOST, NOTHING HERE IS DESTRUCTIVE AND SHOULD NOT BE USE TO DO SO

----

## Goal of this excercise
    - See how a server crashes or how it gets errors
    - Understand what caused it 
    - See what attackers look for 
    - Learn why defenses exist 

---

## Real-World Scenarion
- You deploy a Node.js server with:
    - No input validation 
    - No error handling
    - Open network binding 

- Most attacks come from:
    - Bots
    - Scripts 
    - Scanners
- They will:
    - Scan IP ranges 
    - Probe common ports
    - Send malformed requests

# PART 1 
- We saw before how our server crashed when there was an error with a request made
- Why is this important?
    - In the real world your server might handle:
        - Logins 
        - APIs
        - Monitoring 
        - Metrics
    - A crash means:
        - No service
        - No response
        - Possible data loss
This is called **Denial of Service**
- Not hacking
- Not stealing
- Just making something unusable
