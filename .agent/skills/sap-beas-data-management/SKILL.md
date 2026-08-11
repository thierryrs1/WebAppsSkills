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
- **Tab Navigation (UX Flow)**: When a user performs a search (e.g., typing an OP and pressing enter), the application should automatically switch to the results tab using `sap.ui.getCore().byId("tabBarId").setSelectedKey("resultsKey")`.
- **Search Triggers**: Use the `submit` and `valueHelpRequest` events on `sap.m.Input` controls to trigger API searches natively. Do not rely exclusively on detached "Search" buttons if an input field is the primary driver.
- **Routing**: You can switch pages programmatically using `myApp.to("pageId")` or set up the native `sap.m.routing.Router`. Avoid writing raw DOM replacement logic.

### 4. Mock Data Rules (Strict Security)
- **NO CLIENT DATA**: When creating mock data or static examples, it is STRICTLY PROHIBITED to use real or suspected client data (e.g., real OP numbers, exact part numbers, client names).
- **Generic Manufacturing Data**: Always invent highly generic dummy data (e.g., "OP-99201", "PRD-001 Motor Elétrico", "Rolamento de Esferas").
