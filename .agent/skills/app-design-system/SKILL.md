---
name: App Design System (SAPUI5 Classic)
description: Detailed design and UI guidelines for creating classic SAPUI5 webapps in the SAP Business One and BEAS Manufacturing ecosystem.
---

## Visual and Technological Overview

When designing the user interface (UI) for SAP Business One and BEAS Manufacturing applications, strictly apply the following guidelines to ensure full compliance with the SAP corporate ecosystem.

### 1. Core Technologies (SAPUI5 Classic)
- **Main Framework**: Use the **Classic SAPUI5 Framework** (OpenUI5) loaded via the official bootstrap script (`sap-ui-core.js`). Do not use React or Vanilla Web Components.
- **Official Components**: Utilize the native controls provided by the `sap.m` (Mobile/Main) and `sap.tnt` libraries (e.g., `sap.m.Button`, `sap.m.Page`, `sap.m.Table`).
- **Implementation**: Instantiate components programmatically via JavaScript (e.g., `new sap.m.Button({...})`) or using XML Views if instructed, relying on the global `sap` object loaded by the bootstrap.

### 2. SAP Fiori Visual Style
The design MUST be identical to the standard and premium **SAP Fiori** experience.
- **Structural Layouts**: Organize pages using standard SAPUI5 containers like `sap.m.App`, `sap.m.Page`, and `sap.f.DynamicPage`.
- **UI Elements (Fiori)**: Make extensive use of `sap.m.Panel`, `sap.m.Table`, and `sap.m.ObjectHeader`.
- **Typography and Icons**: Icons should be loaded using the `sap-icon://` protocol native to SAPUI5.

### 3. Theme Restrictions (Mandatory: Light Mode)
- **Recommended Themes**: The SAPUI5 bootstrap should enforce a clear, modern light theme like **SAP Belize** (`sap_belize`) or **SAP Horizon** (`sap_horizon`).
- **PROHIBITION OF DARK MODE**: It is strictly forbidden to create, suggest, or enable any Dark Mode functionality. 

### 4. Usability (Manufacturing and ERP UX)
- **Shop Floor Accessibility (BEAS)**: Interfaces designed for BEAS Manufacturing are often used on industrial tablets. Ensure controls have `sapUiSizeCozy` or touch-friendly sizes.
- **Visual Feedback**: Provide instant indicators using native components: `sap.m.MessageToast` for brief successes, and `sap.m.MessageBox` for ERP alerts and errors.