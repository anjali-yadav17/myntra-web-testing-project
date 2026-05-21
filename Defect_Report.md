# Defect Report (Jira Bug Log) - Myntra E-Commerce Website Testing

This document logs the defects identified during the execution of the Myntra E-Commerce Test Suite. Logging defects with clear, actionable steps is a core competency of professional QA Engineers. The defects below simulate real-world **Jira tickets**.

---

## 📊 Defect Metrics Dashboard

*   **Total Defects Logged**: 5
*   **Defect Distribution by Severity**:
    *   🔴 **Critical (P1)**: 1
    *   🟠 **Major (P2)**: 3
    *   🟡 **Minor (P3)**: 1
*   **Defect Distribution by Status**:
    *   **Open / To Do**: 3
    *   **In Progress**: 1
    *   **Fixed & Verified**: 1 (Regression Verified)

---

## 🐞 Detailed Defect Logs

### 1. BUG_MYN_001: Brand and Discount filter combination displaying non-selected brand products
*   **Status**: 🔴 Open
*   **Priority**: High (P1)
*   **Severity**: Major
*   **Component**: Product Listing Page (PLP) - Search & Filter Module
*   **Environment**: Staging v1.0.4, Windows 11, Google Chrome (v112.0)
*   **Associated Test Case**: `TC_MYN_SRCH_005`

#### Summary:
When filtering product search results by combining a specific brand (e.g., **Puma**) and a discount range (e.g., **30% and above**), the catalog list page displays products from unrelated brands (like HRX, Roadster) that match the discount filter, violating the brand selection constraint.

#### Steps to Reproduce:
1. Navigate to the Myntra Staging Home page.
2. In the Search Bar, enter `"Sneakers"` and press Enter.
3. On the left filter panel, select the check box for Brand: **Puma**.
4. In the Discount filter section, select the check box for **"30% and above"**.
5. Scroll through the product grid and observe the brand names of the displayed shoes.

#### Expected Result:
The product listing should strictly display Puma sneakers that have a discount of 30% or more.

#### Actual Result:
The listing displays Puma sneakers with discounts, but also displays **HRX** and **Roadster** sneakers that have a 30% or above discount. The brand filter is ignored when a discount filter is added.

#### Screenshots / Logs Simulation:
```json
// Console Log showing wrong query parameters sent to search API
Request URL: https://staging-api.myntra.co.in/search/products?q=sneakers&brand=Puma&discount=30-100
Response Payload: Contains "brand": "HRX" and "brand": "Roadster" alongside Puma products.
```

---

### 2. BUG_MYN_002: Fit Finder tool crashes with 500 error on specific height and weight boundaries
*   **Status**: 🟠 In Progress
*   **Priority**: Medium (P2)
*   **Severity**: Major
*   **Component**: Product Details Page (PDP) - Fit Finder Widget
*   **Environment**: Staging v1.0.4, macOS Sequoia, Safari v16.2
*   **Associated Test Case**: `TC_MYN_PDP_005`

#### Summary:
The "Fit Finder" recommendation algorithm crashes and displays a blank screen inside the modal when inputting exact boundary weight values (e.g., less than 35 kg or greater than 150 kg).

#### Steps to Reproduce:
1. Open any apparel PDP (e.g., Roadster Casual Shirt).
2. Click on the `"Find your size"` link next to the size options.
3. In the Fit Finder modal, set height to `160 cm`.
4. Enter weight as `30 kg` (extreme lower boundary) or `160 kg` (extreme upper boundary).
5. Click `"Next"`.

#### Expected Result:
The tool should display a validation error: `"Please enter a weight between 35 kg and 150 kg."` or recommend sizes based on closest available bounds.

#### Actual Result:
The modal goes completely blank (White Screen). The console displays an unhandled `NullPointerException` from the microservice.

#### Error Logs:
```text
TypeError: Cannot read properties of null (reading 'size_matrix_weight')
    at FitFinder.calculateSize (FitFinderWidget.js:142:38)
    at HTMLButtonElement.onSubmit (FitFinderWidget.js:89:12)
```

---

### 3. BUG_MYN_003: App crashes (White Screen of Death) when payment gateway returns HTTP 500
*   **Status**: 🔴 Open
*   **Priority**: High (P1)
*   **Severity**: Critical
*   **Component**: Checkout & Payments Module
*   **Environment**: Staging v1.0.4, Windows 11, Edge (v111.0)
*   **Associated Test Case**: `TC_MYN_PAY_008`

#### Summary:
If a bank server or payment gateway returns a 500 Server Error during redirect, the Myntra application crashes to a blank white screen with no error boundary or navigation recovery options, forcing the user to close the browser.

#### Steps to Reproduce:
1. Add any item to the bag and proceed to the Payment section.
2. Select **Net Banking** and choose **SBI** (configured to simulate mock gateway 500 error).
3. Click "Pay Now".
4. The mock payment server responds with `HTTP 500 Internal Server Error`.
5. Observe the browser behavior.

#### Expected Result:
The payment gateway redirection should fail gracefully. Myntra should display a friendly error page: *"Payment failed due to technical issues at the bank. Your money is safe, and your cart is saved."* with a "Retry Payment" button.

#### Actual Result:
The entire web page blanks out. No headers, footers, or error notifications are rendered.

#### Console Errors:
```text
GET https://staging-api.myntra.co.in/checkout/payment-verify 500 (Internal Server Error)
Uncaught (in promise) Error: Gateway failure: Cannot parse response of undefined.
    at PaymentVerifyPage.componentDidMount (PaymentVerify.js:48:19)
```

---

### 4. BUG_MYN_004: "Exchange Size" button throws Out of Stock error for available sizes
*   **Status**: 🟢 Fixed & Verified
*   **Priority**: High (P1)
*   **Severity**: Major
*   **Component**: Orders & Post-Purchase Modules
*   **Environment**: Staging v1.0.4, Mobile Web (Android Chrome)
*   **Associated Test Case**: `TC_MYN_ORD_006`

#### Summary:
Users cannot exchange clothing items for alternative sizes because the "Exchange" submission portal states the size is out of stock, even though the main Product Details Page (PDP) lists the size as active and available for fresh purchases.

#### Steps to Reproduce:
1. Navigate to "My Orders" and select a delivered order (e.g., Wrogn Jeans, Size 32).
2. Click `"Exchange"`.
3. Choose Size **34** (which shows as "Available" in the list).
4. Click `"Confirm Exchange"`.

#### Expected Result:
The exchange request should process successfully, schedule the reverse pickup, and reserve the size 34 item.

#### Actual Result:
An error banner pops up: `"Selected size is out of stock. Cannot process exchange."` despite the size being fully active and purchaseable on the live product page.

#### Resolution Details:
*   **Fix**: Developer identified that the Exchange API was querying a stale caching layer for inventory check, whereas the PDP was querying the live inventory database. Cache-invalidation hook added on order checkout.
*   **Verification**: Verified on Build v1.0.5. Exchange for Size 34 processed successfully. (Status closed).

---

### 5. BUG_MYN_005: Pincode API timeout blocks Checkout Flow (Boundary check)
*   **Status**: 🔴 Open
*   **Priority**: High (P1)
*   **Severity**: Major (Blocks execution of tests)
*   **Component**: Address / Checkout Pincode Serviceability
*   **Environment**: Staging v1.0.4, Android 13, Chrome Mobile
*   **Associated Test Case**: `TC_MYN_CHK_004`

#### Summary:
Entering specific boundary/remote pincodes causes the serviceability checker API to timeout (taking over 15 seconds) and freeze the Checkout "Place Order" button indefinitely without showing an error message.

#### Steps to Reproduce:
1. Proceed to the address details screen during checkout.
2. Enter remote pincode `790001` (Tawang, Arunachal Pradesh).
3. Click "Save Address".
4. The button shows a spinner. Wait 30 seconds.

#### Expected Result:
The checker should complete within 3 seconds. If there's a timeout, it should fail gracefully: *"Connection timed out. We are unable to verify this pincode at the moment. Please save the address, and we will verify it shortly."*

#### Actual Result:
The spinner rotates indefinitely. No error is thrown. User cannot click other UI elements.
