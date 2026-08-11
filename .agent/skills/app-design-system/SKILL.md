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

### 2. SAP Fiori Visual Style (Premium & Dynamic)
The design MUST be identical to the standard and premium **SAP Fiori** experience, avoiding "flat" or "lifeless" interfaces.
- **Rich Layouts**: Instead of plain pages, use rich containers like `sap.f.DynamicPage` or `sap.uxap.ObjectPageLayout`.
- **UI Elements (Fiori)**: Make extensive use of `sap.m.ObjectHeader` (for highlighted records), `sap.m.ObjectStatus` (to add semantic colors like Success/Warning/Error to text), and `sap.m.InfoLabel`. 
- **Spacing and Margins**: Liberally use SAPUI5 CSS margin and padding classes (e.g., `sapUiSmallMargin`, `sapUiResponsivePadding--header`) to give the UI breathing room. Don't let elements feel cramped.
- **Typography and Icons**: Icons should be loaded using the `sap-icon://` protocol native to SAPUI5. Use icons on buttons and headers to make the UI more vibrant.

### 3. Theme Restrictions (Mandatory: Light Mode)
- **Recommended Themes**: You MUST enforce the modern **SAP Horizon** (`sap_horizon`) theme for a brighter, more rounded, and contemporary look. Avoid the older `sap_belize` theme which looks dated.
- **PROHIBITION OF DARK MODE**: It is strictly forbidden to create, suggest, or enable any Dark Mode functionality. 

### 4. Usability (Manufacturing and ERP UX)
- **Shop Floor Accessibility (BEAS)**: Interfaces designed for BEAS Manufacturing are often used on industrial tablets. Ensure controls have `sapUiSizeCozy` or touch-friendly sizes.
- **Visual Feedback**: Provide instant indicators using native components: `sap.m.MessageToast` for brief successes, and `sap.m.MessageBox` for ERP alerts and errors.