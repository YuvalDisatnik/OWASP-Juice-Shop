# OWASP Juice Shop Walkthrough: Finding the Hidden Scoreboard

This guide documents the solution to the **"Find the hidden scoreboard"** challenge in OWASP Juice Shop. Below, you'll find a detailed walkthrough of how this challenge was approached, solved, and verified.

---

## Challenge: Find the Hidden Scoreboard

The objective is to locate the scoreboard of OWASP Juice Shop, which is not directly accessible via the website's navigation.

---

### Walkthrough

#### 1. **Open Developer Tools**
   - Access the **Developer Tools** by pressing `F12` (or right-clicking the page and selecting **Inspect**).
   - Navigate to the **Debugger** or **Sources** tab to explore the site's JavaScript files.

#### 2. **Search for Clues in `main.js`**
   - Locate and open the `main.js` file, which typically contains core functionality for the site.
   - Use the **Search** feature (`Ctrl+F` or `Cmd+F`) to look for the keyword `/score`.

#### 3. **Identify the Scoreboard Path**
   - Upon searching for `/score`, you will find it referenced under the `sidenavtoggle` function:
     ```javascript
     "/score-board"
     ```
   - This indicates that the scoreboard is located at `/score-board`, even though it is not linked directly in the navigation menu.

#### 4. **Access the Scoreboard**
   - Manually navigate to the hidden scoreboard by entering the URL in your browser's address bar:
     ```
     http://<Juice-Shop-URL>/score-board
     ```
   - Replace `<Juice-Shop-URL>` with the address where your Juice Shop instance is hosted (e.g., `http://localhost:3000/score-board` for local installations).

#### 5. **Verify Completion**
   - After accessing the scoreboard, the challenge will be marked as solved in your progress tracker.

---

### Insights and Takeaways

- This challenge highlights the importance of inspecting and analyzing client-side JavaScript for potential clues. 
- Tools like browser Developer Tools can reveal hidden endpoints and resources that are not directly exposed in the user interface.
- The `/score-board` endpoint is part of Juice Shop’s design to teach about poorly-hidden functionality.

---

### Tools Used

- Browser Developer Tools (e.g., Chrome/Firefox)
- Juice Shop running locally or on a hosted server

---
