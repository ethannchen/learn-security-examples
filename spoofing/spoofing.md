# Spoofing

This example demonstrates spoofing through two ways -- Stealing cookies programmatically and cross site request forgery (CSRF).

## Steps to reproduce the vulnerability

1. Install dependencies

    `$ npx install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. Start the malicious server **mal.ts**

    `npx ts-node mal.ts`

4. Open __http://localhost:8000__ in a browser, type a name and Submit.

5. Open the __Application__ tab in the Browser's inspect pane. Find the __Cookies__ under __Storage__. You should see a __connect.sid__ cookie being set.

6. Open the HTML file __mal-steal-cookie.html__ file in the same browser (different tab). Open inspect and view the console.

7. Click the link in the HTML file. Do you see the cookie being stolen in the console?

8. Open the HTML file __mal-csrf.html__ file in the same browser (different tab). What do you see if the user has not logged out of **insecure.ts**? What do you see if the user has logged out? 


## For you to answer

1. Briefly explain the spoofing vulnerability in **insecure.ts**.
   - Session hijacking
   - Cross-site Request Forgery (CSRF)

2. Briefly explain different ways in which vulnerability can be exploited.
    - `httpOnly: false` in the session cookie: meaning hackers can use malicious scripts (XSS attacks) to steal cookies.
    - Weak hardcoded secret key ("SOMESECRET"): If a hacker figures out the secret key, they can create fake session cookies and log in as any user.
    - If an admin is logged in and visits a hacker’s website, the hacker can secretly send a request to real website `/sensitive` and do bad things.
    - No `sameSite` protection: Cookies are sent even on requests from other websites, allowing attackers to use tricks like hidden forms to perform actions.
   
3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.
    - Uses `httpOnly: true`: Stops JavaScript from stealing cookies.
    - Uses a customizable secret key `process.argv[2]`: Makes it harder for hackers to guess
    - Uses `sameSite: true`: Stops cookies from being used in cross-site attacks.
