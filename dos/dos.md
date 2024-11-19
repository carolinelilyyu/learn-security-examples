# Denial-of-Service (DoS)

This example demonstrates DoS vulnerabilities and how they can be exploited.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Ignore if you have already done this once. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?id[$ne]=
    ```

4. Do you see the server crashing?

## For you to do
Attackers can prevent access to a service by overwhelming it with requests or by exploiting a vulnerability to crash it. 

Few reasons: 
- Unnecessary exposure of services.
- Lack of rate limiting.
- Failure to use a Content Delivery Network (CDN) to handle high traffic loads. 
Also:
- No firewall to block IPs or geoIPs.

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts** that can lead to a DoS attack.
Server isn't able to catch exceptions. It comes from the id. 

2. Briefly explain how a malicious attacker can exploit them.
If the attacker were to craft an id that takes a long time, they could crash the server. `http://localhost:3000/userinfo?id[$ne]=` crashed the server, because we passed a string and mongodb is looking for a specific format. The programmer wasn't able to handle this specific format on the server side for server crashed. 

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?
Handle the error so we don't crash unexpectedly. try catch on the database if an exception handles. We should also sanitize the inputs to be a 24 character alphanumeric string. Configure a rate limiter (ideally in a different file) so that every IP can send one request every X minutes.