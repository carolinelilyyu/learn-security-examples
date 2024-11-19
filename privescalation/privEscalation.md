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
Unauthorized elevation of priveleges, granting access to resources or actions beyond the intended level of authorization. 
Few reasons:
- Implmentation weakness
- Absence of authorization
- Exposing services which don't need to be

1. Briefly explain the potential vulnerabilities in **insecure.ts**
userid and new role is read from the request body. The user can control updates. 

2. Briefly explain how a malicious attacker can exploit them.
The user can control the updates and is able to update the user to non-admin or admin. 

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?
The cookie should be programatically inaccessible. Set to strict so the client and server is on the same domain to prevent cross site scripting attack. Don't want to hardcode our secret. The secret should be set in a config file, read separately from the source code. Then we can trust this user's req session. Then we go ahead to update the user.