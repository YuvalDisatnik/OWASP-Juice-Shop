# OWASP Juice Shop Walkthrough: Login Admin Challenge

This guide documents the solution to the **"Login Admin"** challenge in OWASP Juice Shop. The objective is to exploit an SQL Injection vulnerability to bypass the login process and gain admin access.

---

## Challenge: Login Admin

The goal is to log in as the admin user by exploiting an SQL Injection vulnerability on the login page.

---

### Walkthrough

#### 1. **Setup Burp Suite and Proxy**
   - Open **Burp Suite** and configure your browser to route traffic through the **Proxy** (e.g., using an extension like **FoxyProxy**).
   - Ensure interception is enabled to capture HTTP requests.

#### 2. **Navigate to the Login Page**
   - Go to the Juice Shop login page.
   - Enter arbitrary credentials, such as:
     ```
     Email: admin
     Password: 123
     ```
   - Submit the form and capture the **POST request** containing the credentials.

#### 3. **Send the Request to Repeater**
   - In Burp Suite, forward the captured POST request to the **Repeater** tab.
   - Resend the request to see the server's response. Initially, the response will return:
     ```
     Invalid email or password
     ```

#### 4. **Analyze the SQL Query Structure**
   - To test for SQL Injection, modify the email input to include a single quote (`'`) after the admin username:
     ```
     admin'
     ```
   - Resend the request and observe the server's response. The response returns an error:
     ```
     500 Internal Server Error
     ```
   - The error message indicates an **SQLITE_ERROR**, revealing the SQL query structure used by the server:
     ```sql
     SELECT * FROM Users WHERE email='admin'' AND password='202cb96ac59075b964b07152d234b70' AND deletedAt IS NULL
     ```

#### 5. **Craft the Injection Payload**
   - Based on the exposed SQL query structure, craft a payload that bypasses the login checks:
     ```
     'admin' OR 1=1; --'
     ```
   - This payload manipulates the query logic as follows:
     - `OR 1=1` always evaluates to `true`.
     - `;` ends the query.
     - `--` comments out the rest of the query, bypassing the password check.

#### 6. **Execute the Injection**
   - Enter the crafted payload in the email field:
     ```
     Email: 'admin' OR 1=1; --'
     ```
   - Use any arbitrary value for the password field.
   - Submit the form to log in successfully as the admin user.

---

### Insights and Takeaways

- This challenge demonstrates a classic **SQL Injection** vulnerability caused by unsanitized user input.
- By exposing the database query structure in error messages, the application provides attackers with valuable information for crafting payloads.
- Proper input validation, parameterized queries, and error message obfuscation are critical for preventing SQL Injection.

---

### Tools Used

- **Burp Suite** (for intercepting and modifying HTTP requests)
- **ProxyFoxy** (or any proxy configuration tool)
