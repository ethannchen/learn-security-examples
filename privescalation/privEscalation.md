# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

    ```
        http://localhost:3000/send-form
    ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
   - The application does not authenticate the user making the request. It simply checks the `userId` field in the request body, which can be manipulated by any attacker to impersonate another user and potentially change their role.
   
2. Briefly explain how a malicious attacker can exploit them.
   - The attacker can enumerate `userId` and try to change its role to user and the real admin will eventually lose their administrative rights.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?
   - Session-Based and Role-Based Authentication: The secure.ts uses session management which ensures that each request is associated with a specific logged-in user. This helps prevent unauthorized users from accessing sensitive routes, like `/update-role`. It also checks whether the logged-in user has an admin role before allowing the user to update another user’s role. 