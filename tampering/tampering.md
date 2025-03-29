# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies

    `npm install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. In the browser, type a potentially malicious script in the name field of the form

    ```
        <script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
    ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
    - Cross-Site Scripting (XSS): The name input in the `/register` route is stored in the session without sanitization, allowing an attacker to inject malicious HTML or JavaScript.
2. Briefly explain how a malicious attacker can exploit them.
   - A user could enter a script `<script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>` as their name, and when the session is used in the response, the script will execute in the victim's browser, and the victim will be potentially redirect to other malicious website.
3. Briefly explain why **secure.ts** does not have the same vulnerabilties?
   - The `escapeHTML` function sanitizes user input before storing it, preventing malicious scripts from being injected.