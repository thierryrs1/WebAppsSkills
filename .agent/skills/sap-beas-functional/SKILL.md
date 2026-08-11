---
name: SAP and BEAS Functionality
description: Detailed guidelines on file structure, initialization, and dynamic loading for BEAS Manufacturing and SAP Business One web applications.
---

## Initialization Architecture and Functional Logic

When developing the logic and structure for BEAS and SAP Business One applications, you must strictly follow these detailed rules:

### 1. No HTML Files Allowed
- **Strict Prohibition**: Never create `.html` files (such as `index.html`).
- **Context**: The platform (BEAS portal or SAP B1 host) already provides the main page structure, rendering container, and initial DOM.

### 2. Single Entry Point (`app.js`)
- The application must be initialized **exclusively** through a single file named `app.js`.
- This file acts as the application's "maestro" and is responsible for all initial setup and bootstrapping.

### 3. Module System (type="module")
- The `app.js` file is executed as an ES6 module (loaded via `<script type="module">` by the host system).
- **Isolation and Organization**: Use `import` and `export` to separate your code into logical modules (e.g., `api.js`, `utils.js`, `router.js`).
- Do not pollute the global scope (`window`) unless strictly required for legacy integration with BEAS APIs.

### 4. Dynamic Resource Loading (CSS and JS)
- **CSS Injection**: Since there is no HTML file to declare `<link>` tags, all external styling must be injected via JavaScript. The `app.js` file should import the CSS or, if necessary, create a `<link rel="stylesheet">` element and append it to `document.head`.
- **Script Importing**: Other libraries or dependencies must be orchestrated from `app.js` using native ES6 imports, ensuring execution order is respected.

### 5. BEAS Portal Integration
- If the development is specifically for the **BEAS Portal**:
  - All network request logic (fetching ERP data), authentication, session maintenance, and initial portal rendering must be triggered from `app.js`.
  - Centralize state management and API calls at the beginning of the `app.js` lifecycle before mounting the graphical interface.
