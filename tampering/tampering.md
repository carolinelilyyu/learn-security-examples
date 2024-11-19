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
An attacker change or tamper with the applicatino's inputs to cause unintentionally behavior. We don't sanitize the inputs. We're not rejecting code as input. 

- Input expects strings and now code can be injected into server. 
- Failure to block malicious file uploads. 
- Using inputs in database queries without validation. 
- Allow attackers to tamper with the cookies.

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
It's not checking the input. We're accepting inputs that should be plain strings but javascript code could also be injected as a string. Some javascript gets injected and a link called `Gotcha` is displayed on top. 

2. Briefly explain how a malicious attacker can exploit them.
The script could have code to delete everything on the server. They can inject any code they want.

3. Briefly explain why **secure.ts** does not have the same vulnerabilties?
`escapeHTML` will replace and sanitize input to prevent XSS attacks. This replaces any special characters with their string equivalence. 