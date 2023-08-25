# 0.4: New note diagram

```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server

    note right of browser: Redirect response with url for browser to follow, releoading new_note html

    server-->>browser: 302 redirect https://studies.cs.helsinki.fi/exampleapp/new_note
    deactivate server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server
    server-->>browser: 304 not modified HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: 304 not modified css
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: 304 not modified css
    deactivate server

    note right of browser: Browser starts running js to retrieve json from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: 200 retrieve updated json payload
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes
```