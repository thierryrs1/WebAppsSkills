---
name: SAP BEAS Data and State Management
description: Detailed guidelines for managing data fetching, API error handling, loading states (progress indicators), and lightweight routing in BEAS/SAP WebApps.
---

## API Integration, State, and Routing

When dealing with SAP B1 or BEAS Manufacturing REST/OData APIs within the WebApp portal, you must strictly follow these rules to ensure stability, especially on factory floor devices.

### 1. Error Handling and Loading Feedback (Mandatory)
- **Prevent Freezing:** Never allow the interface to freeze without providing feedback to the user during API calls.
- **Multiple Requests (Progress Indicator):** Whenever the application needs to trigger multiple batch requests (e.g., saving dozens of samples and measurements simultaneously), it is MANDATORY to implement a Loading Screen displaying the **percentage (%)** of the completed process. This is vital so the operator knows the system has not crashed.
- **Simple Requests:** For fast, single queries, use the `BusyIndicator` component from the SAP Fiori standard.
- **Exception Handling:** If the ERP API returns an error (Timeout, Error 500, etc.), handle it immediately by displaying a user-friendly `MessageBox`. Silent failures (only logging to the console) are strictly prohibited.

### 2. Lightweight Navigation Management (Routing)
- **State-Based Navigation:** Since we cannot use modern routing libraries that depend on bundlers (such as `react-router-dom`), all screen navigation must be controlled via State Management in the root component (`app.js`).
- **Implementation:** Use simple states (e.g., `const [currentScreen, setCurrentScreen] = useState('LIST')` or mapping the selected entity `const [selectedOrder, setSelectedOrder] = useState(null)`) to toggle which components should be rendered.
- **Memory Management:** Ensure that the previous component is properly unmounted when switching screens to prevent memory leaks on factory tablets.
