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
Information Disclosure refers to the unauthorized exposure of leakage of sensitive info, such as personal data or system details, to unintended parties.

Few reasons are:
- Lack of encrypting sensitive data in transit and storage
- Leaking sensitive data in the code or logs
- Lack of access control on sensitive data

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
The attacker can input a NoSQL or SQL injections into the username query. Then they can get the password. There is unauthorized exposure of leakage of sensitive info, such as personal data or system details, to unintended parties.

Few reasons are:
- Lack of encrypting sensitive data in transit and storage
- Leaking sensitive data in the code or logs
- Lack of access control on sensitive data

2. Briefly explain how a malicious attacker can exploit them.
Tampering the inputs to get into the system. You can type in `http://localhost:3000/userinfo?username[$ne]=`, which is { username: { $ne: "" } } in mongodb. This would fetch all records where the username is not an empty string. In the backend, you can inject SQL like this too: SELECT * FROM users WHERE username != '';

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?
You can encrypt the password returned. You can input validation to see if the typeof username is a string. You can replace any non word character (^ means not , `\w` non word character) with empty characters; this is so you don't allow % and special characters. This is similar to escapeHTML. If the username is not of type string then it'll return 400 invalid username.