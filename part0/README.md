# Part 0: Fundamentals of Web Apps

This section focuses on the communication patterns between the browser and the server, specifically comparing traditional multi-page applications (MPA) with modern single-page applications (SPA).

---

### Exercise 0.4: New Note Diagram (Traditional Web App)
When a user saves a note in a traditional app, the browser sends a `POST` request, the server responds with a `302 Redirect`, and the browser performs a full page reload.

```mermaid
sequenceDiagram
    participant browser
    participant server

    Note over browser: User writes a note and clicks Save

    browser->>server: POST [https://studies.cs.helsinki.fi/exampleapp/new_note](https://studies.cs.helsinki.fi/exampleapp/new_note)
    activate server
    Note left of server: Server saves the note to the database
    server-->>browser: HTTP 302 Redirect to /notes
    deactivate server

    browser->>server: GET [https://studies.cs.helsinki.fi/exampleapp/notes](https://studies.cs.helsinki.fi/exampleapp/notes)
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET [https://studies.cs.helsinki.fi/exampleapp/main.css](https://studies.cs.helsinki.fi/exampleapp/main.css)
    activate server
    server-->>browser: main.css
    deactivate server

    browser->>server: GET [https://studies.cs.helsinki.fi/exampleapp/main.js](https://studies.cs.helsinki.fi/exampleapp/main.js)
    activate server
    server-->>browser: main.js
    deactivate server

    Note over browser: Browser executes JS to fetch JSON data

    browser->>server: GET [https://studies.cs.helsinki.fi/exampleapp/data.json](https://studies.cs.helsinki.fi/exampleapp/data.json)
    activate server
    server-->>browser: Updated JSON data [{ "content": "New Note", ... }, ...]
    deactivate server

    Note over browser: Browser renders the notes




Exercise 0.5

sequenceDiagram
    participant browser
    participant server

    browser->>server: GET [https://studies.cs.helsinki.fi/exampleapp/spa](https://studies.cs.helsinki.fi/exampleapp/spa)
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET [https://studies.cs.helsinki.fi/exampleapp/main.css](https://studies.cs.helsinki.fi/exampleapp/main.css)
    activate server
    server-->>browser: main.css
    deactivate server

    browser->>server: GET [https://studies.cs.helsinki.fi/exampleapp/spa.js](https://studies.cs.helsinki.fi/exampleapp/spa.js)
    activate server
    server-->>browser: spa.js
    deactivate server

    Note over browser: Browser executes spa.js and fetches JSON

    browser->>server: GET [https://studies.cs.helsinki.fi/exampleapp/data.json](https://studies.cs.helsinki.fi/exampleapp/data.json)
    activate server
    server-->>browser: [{ "content": "SPA Load", "date": "2025-12-31" }, ... ]
    deactivate server

    Note over browser: JS renders the notes to the page




Exercise 0.6

sequenceDiagram
    participant browser
    participant server

    Note over browser: User clicks Save
    Note over browser: JS appends note to local list and redraws UI

    browser->>server: POST [https://studies.cs.helsinki.fi/exampleapp/new_note_spa](https://studies.cs.helsinki.fi/exampleapp/new_note_spa)
    activate server
    Note right of browser: JSON: { "content": "SPA Save", "date": "2025-12-31" }
    server-->>browser: 201 Created
    deactivate server

    Note over browser: No page reload or redirect occurs
