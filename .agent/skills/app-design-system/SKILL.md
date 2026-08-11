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

### 2. SAP Fiori Visual Style & BEAS Identity
The design MUST be identical to the standard **SAP Fiori** experience, aligning specifically with how BEAS portals are structured.
- **BEAS Portal Layouts**: The app content is usually rendered inside a white container over the portal's light blue background. Use `sap.m.IconTabBar` horizontally to separate logical sections (e.g., "Ordens", "Cabeçalho", "Linhas"). For forms and header details, strictly use `sap.ui.layout.form.SimpleForm` to create perfectly aligned, multi-column Fiori Object Page layouts.
- **Data Lists (Dense/Compact)**: When listing orders or operations, use `sap.m.List` with `sap.m.CustomListItem`. Lists in BEAS portals often present a lot of data; apply the `sapUiSizeCompact` density class to list containers so items fit tightly on the screen (often with dashed separators).
- **Inputs and Validation**: Search bars and form inputs typically span the full width of their white panels. Use `valueState="Error"` (red borders) for mandatory/invalid fields, and utilize inner icons (like a key `sap-icon://key`) to denote primary keys or lookups.
- **UI Elements**: Make extensive use of `sap.m.ObjectStatus` to add semantic colors (e.g., Warning, Success) to text statuses like "Depósito" or "DESCONGELAR".

### 3. Theme Restrictions (Mandatory: Light Mode)
- **Recommended Themes**: You MUST enforce the modern **SAP Horizon** (`sap_horizon`) theme for a brighter, more rounded, and contemporary look. Avoid the older `sap_belize` theme which looks dated.
- **PROHIBITION OF DARK MODE**: It is strictly forbidden to create, suggest, or enable any Dark Mode functionality. 

### 4. Usability (Manufacturing and ERP UX)
- **Shop Floor Accessibility (BEAS)**: Interfaces designed for BEAS Manufacturing are often used on industrial tablets. Ensure controls have `sapUiSizeCozy` or touch-friendly sizes.
- **Visual Feedback**: Provide instant indicators using native components: `sap.m.MessageToast` for brief successes, and `sap.m.MessageBox` for ERP alerts and errors.

### 5. Layout Constraints (BEAS Portal)
- **NO NAVBAR/SHELLBAR**: Do not create or include a global navigation bar, shell bar, or top-level app header (`sap.f.ShellBar`, `sap.tnt.ToolHeader`, etc.) in your UI code (`app.js`). The BEAS Portal environment already provides the outer shell and navigation menu natively. Your application should strictly render only the inner page content (e.g., the `sap.m.Page` or `sap.f.DynamicPage` without the global shell).