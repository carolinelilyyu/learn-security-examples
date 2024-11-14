# Spoofing

This example demonstrates spoofind through two ways -- Stealing cookies programmatically and cross site request forgery (CSRF).

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
A spoofing attack happens when an attacker successfully identifies as noather falsifying or stealing data to gain unathorized access. Not obscuring credentials during entry, insecure storage of credentials, reliance on single factor auth, insecure session config and management.

1. Briefly explain the spoofing vulnerability in **insecure.ts**.
uses the express session middleware to generate a session id and sets it as a bookie in the browser when the client sents a request from the browser. The session ID is sent with every subsequent request.

2. Briefly explain different ways in which vulnerability can be exploited.
Security vulerabilities in the code that could result in spoofing:
    - session hijacking
    - cross-site request forgery (CSRF)

The user can take a leaked token and get access to the priveleged part of the server. They can programtically read the cookie. They could also fool the user to send a fake request. Either way, the cookie gets passed.

In insecure.ts the cookie has been set when we logged in and received the token. When the link to steal cookies has been clicked, this cookie is exposed in the session.

CSRF, attacker is not on same domain. Forged the request, no access to token but the cookie has been set. When link is clicked, session gets sent to server and executes piece of code.

3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.

We should only accept a cookie from a one specific source/site. Block access to the cookie so no one can read or write to it. When configuring the cookie, the `httpOnly` needs to be set to true so no one can read the cookie programatically. The user can change it themselves on the site, but that wouldn't do anything. `sameSite` must be true. Default behavior is to take in every request. This is to avoid CSRF. The cookie gets set but in mal-csrf, the cookie has not been set because the origin is different. 