# OWASP Juice Shop Walkthrough: Error Handling Challenge

This guide documents the solution to the **"Error Handling"** challenge in OWASP Juice Shop. The objective is to trigger a server error and expose sensitive error details.

---

## Challenge: Error Handling

The goal is to exploit a vulnerability that reveals technical details about the server, such as stack traces or database query structures, via improper error handling.

---

### Relevant Steps

#### 1. **Trigger the Error**
   - During the **"Login Admin"** challenge, we submitted the following email input:
     ```
     admin'
     ```
   - This caused the server to return a **500 Internal Server Error**.

#### 2. **Examine the Error Message**
   - The error message revealed critical information, including:
     - The type of database used: `SQLite`.
     - The SQL query structure:
       ```sql
       SELECT * FROM Users WHERE email='admin'' AND password='202cb96ac59075b964b07152d234b70' AND deletedAt IS NULL
       ```

#### 3. **Complete the Challenge**
   - The challenge was marked as complete because the error message displayed sensitive details due to improper error handling.

---

### Insights and Takeaways

- Proper error handling is essential to avoid exposing sensitive server-side details to attackers.
- Best practices include:
  - Using generic error messages for end users.
  - Logging detailed error messages only on the server side for debugging purposes.
  - Avoiding direct exposure of stack traces or query structures.

---

### Tools Used

- **Burp Suite** (for intercepting and modifying HTTP requests)
- **OWASP Juice Shop** login page
