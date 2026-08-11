---
name: App Design System
description: Detailed design and UI guidelines for creating webapps in the SAP Business One and BEAS Manufacturing ecosystem.
---

## Visual and Technological Overview

When designing the user interface (UI) for SAP Business One and BEAS Manufacturing applications, strictly apply the following guidelines to ensure full compliance with the SAP corporate ecosystem.

### 1. Core Technologies (Front-end)
- **Main Framework**: Use **React** as the primary library.
- **Official Components**: It is MANDATORY to use components that comply with the SAP UI5 standard. The primary recommendation is to use the **UI5 Web Components for React** library (`@ui5/webcomponents-react`).
- Avoid building components from scratch (custom buttons, manually built tables). Use what the UI5 ecosystem provides to ensure scalability and compatibility.

### 2. SAP Fiori Visual Style
The design MUST be identical to the standard and premium **SAP Fiori** experience.
- **Structural Layouts**: Organize pages using standard structures such as *Dynamic Page*, *Object Page*, or *Worklist / Master-Detail Layouts*.
- **UI Elements (Fiori)**: Make extensive use of *Cards* for dashboards, complex tables for listing data (e.g., production orders), *Object Headers* for item headers, and fixed *Action Bars*.
- **Typography and Icons**: Use the official SAP font ("72") and the corporate icons from the `@ui5/webcomponents-icons` library.

### 3. Theme Restrictions (Mandatory: Light Mode)
- **Recommended Themes**: Use only the light and modern SAP themes, such as **SAP Horizon** (`sap_horizon`), **SAP Quartz Light** (`sap_fiori_3`), or **SAP Belize**.
- **PROHIBITION OF DARK MODE**: It is strictly forbidden to create, suggest, or enable any Dark Mode functionality. Corporate applications in this manufacturing/ERP environment must remain exclusively in light mode to maintain contrast, standardization, and avoid discrepancies with the host portal.

### 4. Usability (Manufacturing and ERP UX)
- **Shop Floor Accessibility (BEAS)**: Interfaces designed for BEAS Manufacturing are often used on industrial tablets. Buttons and touch areas must have generous sizing, prioritizing visibility and click speed.
- **Visual Feedback**: Provide instant indicators using native components: *Message Toast* modals for brief successes, and *Message Box* or *Popover* for ERP alerts and errors.