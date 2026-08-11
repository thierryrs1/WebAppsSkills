---
name: SAP BEAS Data and State Management (SAPUI5 Classic)
description: Guidelines for managing data fetching, JSON Models, and SAPUI5 routing in BEAS/SAP WebApps.
---

## API Integration, State, and Routing

When dealing with SAP B1 or BEAS Manufacturing REST/OData APIs within the WebApp portal, you must strictly follow these rules to ensure stability, especially on factory floor devices.

### 1. Data Binding and Models
- **SAPUI5 Models**: State management should be handled natively using SAPUI5's Model-View-Controller paradigm. 
- **JSONModel**: For REST APIs or local state, instantiate a `sap.ui.model.json.JSONModel` and set it to the core or the specific view (`app.setModel(myModel)`). Bind UI controls (like `sap.m.List` or `sap.m.Input`) directly to the model properties.

### 2. Error Handling and Loading Feedback
- **Prevent Freezing:** Never allow the interface to freeze without providing feedback to the user during API calls.
- **Busy Indicators**: Use `sap.ui.core.BusyIndicator.show()` and `.hide()` or the `setBusy(true/false)` method on specific `sap.m` controls during data fetching.
- **Exception Handling**: If the ERP API returns an error (Timeout, Error 500, etc.), handle it immediately by displaying a user-friendly `sap.m.MessageBox`. Silent failures (only logging to the console) are strictly prohibited.

### 3. Navigation and Routing
- **App and Pages**: Screen navigation should be controlled using a `sap.m.App` container holding multiple `sap.m.Page` controls.
- **Routing**: You can switch pages programmatically using `myApp.to("pageId")` or set up the native `sap.m.routing.Router` for complex applications. Avoid writing raw DOM replacement logic.
- **Memory Management**: Ensure that pages or complex controls are properly managed or destroyed if they are generated dynamically, to prevent memory leaks on factory tablets.
