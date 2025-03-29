# Tampering

This example demonstrates information disclosure by injecting malicious query objects to a NoSQL database.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?username[$ne]=
    ```

4. Do you see user information being displayed despite the malicious request not having a valid username in the request?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
   - NoSQL Injection Risk: The username from req.query is directly used in `User.findOne()`.

2. Briefly explain how a malicious attacker can exploit them.
   - Attackers can manipulate queries using MongoDB query operators like `username[$ne]=` which could transform the query into something like `{ "username": { "$ne": "" } }`. This would match any document where the `username` is not equal to an empty string, which could potentially return any users in the database or bypass authentication 

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?
   - The username parameter from the query is checked to ensure it is a string, and the input is sanitized by removing non-alphanumeric characters: prevents characters that could be interpreted as MongoDB operators (`e.g., $ne, $gt, $in`) from being used in the query, mitigating the risk of NoSQL injection.