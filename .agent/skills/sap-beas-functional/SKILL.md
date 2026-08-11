---
name: SAP and BEAS Functionality (SAPUI5 Classic)
description: Detailed guidelines on file structure, initialization, and application entry points using the classic SAPUI5 bootstrap.
---

## Initialization Architecture and Functional Logic

When developing the logic and structure for BEAS and SAP Business One applications, you must strictly follow these detailed rules:

### 1. Mandatory HTML File and SAPUI5 Bootstrap
- **`index.html` Required**: ALWAYS create an `index.html` file. 
- **Bootstrap Script**: The `index.html` MUST include the SAPUI5 bootstrap script in the `<head>` exactly as follows (or similar based on specific versions/themes):
  ```html
  <script id="sap-ui-bootstrap" src="https://sapui5.hana.ondemand.com/1.150.0/resources/sap-ui-core.js"
      data-sap-ui-async="true" data-sap-ui-preload="async" data-sap-ui-libs="sap.m, sap.tnt"
      data-sap-ui-theme="sap_belize" data-sap-ui-compatVersion="edge"
      data-sap-ui-resourceroots='{"sps.wms": "./front/"}'></script>
  ```
- **Module Entry**: Below the bootstrap, the `index.html` MUST include the application entry point as an ES module: `<script type="module" src="app.js"></script>`.

### 2. Application Entry Point (`app.js`)
- The `app.js` file acts as the application's starting point.
- Because the SAPUI5 bootstrap is asynchronous (`data-sap-ui-async="true"`), your `app.js` must wait for the SAPUI5 core to be initialized before rendering UI components.
- Use `sap.ui.getCore().attachInit(function() { ... })` inside `app.js` to ensure the framework is fully loaded before instantiating your `sap.m` controls and placing them in the DOM (e.g., `app.placeAt("content")`).

### 3. No Build Tools (Crucial Constraint)
- **NO VITE/WEBPACK/REACT**: Do not use React or build tools. You must write standard JavaScript that executes directly in the browser, relying on the `sap` global namespace provided by the bootstrap.
- **CSS**: UI styling is handled natively by the SAPUI5 theme engine. If custom CSS is absolutely needed, link it standardly in the `index.html` `<head>`, but avoid overriding standard Fiori styles.

### 4. BEAS Portal Integration
- All network request logic (fetching ERP data) and authentication must be handled within the SAPUI5 lifecycle in `app.js` or its associated JS/XML views.
