# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do
Non-repudiation refers to the ability of systems to hold people accountable to their actions. e.g.
- Malicious user deletes sensitive information, but the system cannot track down the user.

Few ways of non-repudiation:
- Insufficient logging
- Logs vulnerable to tampering.
- Lack of audit policies.

1. Briefly explain the vulnerability.
If something were to go wrong, there is no way to investigate or track that problem.

2. Briefly explain why the vulnerability is addressed in __secure.ts__.
Creates middleware functions for logging. Have a server.logfile and keep writing to the log file. The middleware function takes three arguments and the next endpoint/function to call. With every request, find the current timestamp, the request method and the ip address and write it to the log file. If there's an error, then it'll go to the error handling middleware and log the entry and the send the response back. You can manually review it or have a script to look through the log files. If you don't have this tracking, you don't have repudiation. 

3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
Middleware pattern that are linked together like chains. Each function does a trask before passing control to the next middleware or endpoint. The Middleware Pattern centralizes logging, ensuring every request and error is uniformly captured. The modularity of middleware functions allows for separation of concerns, making it easier to maintain and enhance. Logs written to a secure file provide a reliable audit trail, supporting non-repudiation and accountability.