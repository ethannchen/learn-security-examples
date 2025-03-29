# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.
   - No Logging: which means the system cannot track who performs actions like sending messages or retrieving messages. This creates a lack of accountability.
   - No Authentication: Any users can retrieve sensitive system messages without any form of authentication. This exposes the application to unauthorized access without restriction.
2. Briefly explain why the vulnerability is addressed in __secure.ts__.
   - Logging: In secure.ts, logging has been introduced. Every incoming request is logged with detailed information. 
   - Authentication: simulates an authentication mechanism for retrieving messages. The authentication ensures that only authorized users can access sensitive data like the stored messages.
3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
   - Chain of responsibility. 
   - The `secure.ts` uses middleware functions to handle tasks like logging, error handling, and potentially authentication. 
   - For logging, the middleware intercepts incoming requests and writes logs before allowing the request to proceed to the route handler.
   - The error handling middleware catches any errors in the application and logs them appropriately.