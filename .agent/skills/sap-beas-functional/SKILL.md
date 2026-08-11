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

### 6. No Build Tools & Native JavaScript (Crucial Constraint)
- **NO JSX and NO VITE/WEBPACK**: Since the BEAS portal runs the module directly and we must avoid complex build steps, DO NOT use JSX syntax (`<App />`). You MUST write standard ECMAScript using `React.createElement` (e.g., `const e = React.createElement;`) so the browser doesn't throw Syntax Errors.
- **NO CSS Imports**: Do not use `import './style.css'` in the JS code. Native browsers enforce strict MIME checking for ES modules and will throw an error. Rely exclusively on dynamic DOM injection (`document.createElement('link')`) as specified in rule 4.
- **Local Testing**: To test the UI locally without bundlers, developers must manually create an `index.html` (for local dev only) with an `<script type="importmap">` mapping `react`, `react-dom`, and `@ui5/webcomponents-react` to a CDN like `https://esm.sh/`. The file must be served via a local HTTP server (like `npx serve`), never via `file://`.
