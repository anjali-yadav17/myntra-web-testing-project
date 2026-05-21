# TEST PLAN: Myntra E-Commerce Website Testing

---

## 1. Test Plan Identification

| Field | Details |
| :--- | :--- |
| **Test Plan ID** | TP_MYN_ECOM_001 |
| **Project Name** | Myntra E-Commerce Web Application Testing |
| **Application Under Test (AUT)** | Myntra Web Application (Staging Environment) |
| **Document Version** | 1.0 |
| **Prepared By** | Anjali Yadav (QA Test Engineer) |
| **Reviewed By** | Senior QA Lead |
| **Approved By** | QA Manager |
| **Date** | 21/05/2026 |

---

## 2. Introduction

### Objective
The objective of this test plan is to define the testing strategy, scope, resources, environment, and deliverables for verifying the functionality, usability, compatibility, security, and reliability of the Myntra E-Commerce web application. The primary goal is to ensure a high-quality, bug-free online fashion shopping experience, covering critical user journeys from registration to checkout, order management, and return/exchange cycles.

### Scope
This test plan covers the testing of the following primary modules of the Myntra Web Application:
*   **User Registration & Login**: Phone number, social sign-in, and OTP authentication.
*   **Product Search & Advanced Catalogue**: Search bar, category landing pages, fashion-specific filtering (gender, brand, discount, fabric, size, price), and sorting.
*   **Product Details Page (PDP)**: Product media, description, specifications, size charts, fit recommendations, pin-code serviceability, reviews, and ratings.
*   **Shopping Cart & Wishlist**: Adding/removing items, updating quantities, moving items to wishlist, and applying coupons.
*   **Checkout Process**: Multi-step checkout, address management, shipping options, and price breakdowns (GST, delivery fees, coupon discounts).
*   **Payment Gateway Integration**: UPI, Debit/Credit Card, Net Banking, Myntra Wallet, and Cash on Delivery (COD).
*   **Order Management**: Order placement, confirmation, SMS/Email notifications, invoice downloading, and order cancellation.
*   **Order Tracking**: Live tracking of courier stages (Dispatched, Out for Delivery, Delivered).
*   **Returns & Exchanges**: Size/color exchanges, return requests, pickup validation, and refund processing.
*   **Myntra Insider (Loyalty Program)**: Points accumulation, tier advancement, and reward/coupon redemption.
*   **User Profile Management**: Managing saved cards, addresses, wishlist, and profile information.

---

## 3. Test Items

| Item | Description |
| :--- | :--- |
| **Application Under Test** | Myntra Web Application |
| **Platform** | Responsive Web Application (optimized for Desktop, Mobile Web, and Tablet Web) |
| **Browser Support** | Google Chrome (v110+), Mozilla Firefox (v108+), Microsoft Edge (v109+), Apple Safari (v15+) |
| **Devices** | Desktop (Windows, macOS), Laptop, Tablets (iPad), Mobile Phones (iOS, Android) |
| **Modules to be Tested** | Authentication, Search, PDP, Cart, Wishlist, Checkout, Payments, Orders, Returns/Exchanges, Myntra Insider |
| **Type of Testing** | Functional, Regression, Integration, System, Usability, Compatibility, Security, Performance |

---

## 4. Features to be Tested

### Authentication Module
*   **Registration & Login**: User registration via mobile number with OTP. Support for Google and Facebook OAuth logins.
*   **OTP Verification**: OTP expiry, resend option, throttling (maximum retries), and validation of incorrect OTPs.
*   **Session Management**: Session persistence, auto-logout after inactivity, and secure login cookie handling.

### Product Search & Catalogue
*   **Search Functionality**: Auto-suggest keywords, handling of spelling typos, search by product name/brand/category/PID (Product ID).
*   **Fashion-Specific Filters**: Multi-select filters for Gender (Men, Women, Kids), Brand, Color, Price, Discount, Size, Occasion, and Fabric.
*   **Sorting**: Sort by Relevance, Popularity, Customer Rating, Discount, Price (Low to High), and Price (High to Low).

### Product Details Page (PDP)
*   **Visual Assets**: Multi-image carousel, zoom functionality, and product video playability.
*   **Fashion Size Matrix**: Size selector buttons, dynamic visual indicators for out-of-stock sizes.
*   **Size Chart & Fit Guide**: Interactivity of Size Chart modal, unit toggling (Inches vs. Centimeters), and "Fit Finder" recommendation algorithm based on user height/weight.
*   **Delivery Check**: Pincode checker interface to show estimated delivery date (EDD) and Cash on Delivery availability.

### Cart & Wishlist
*   **Wishlist**: Adding items from search results or PDP, moving items from wishlist to cart, and maintaining items list post-logout.
*   **Cart Actions**: Adding multiple sizes/colors, updating quantities, deleting items, and preserving cart items on session timeout.
*   **Coupon Application**: Automated discount calculation, error messages for invalid coupon codes, and terms/expiry conditions.

### Checkout & Address Module
*   **Address Management**: Add new shipping address, auto-detect location, edit existing address, and delete address.
*   **Pricing Engine**: Validating correct calculation of MRP, Discount, Coupon Discount, Convenience/Delivery Fees, GST, and Net Payable Amount.

### Payment Module
*   **Redirection & Security**: Seamless transition to payment gateway. Masking card details, CVV validation, 3D secure (OTP) routing.
*   **Payment Channels**: Card payments, UPI (redirect & collect flows), Net Banking, Myntra Credit Wallet, and Cash on Delivery.
*   **Failure Recovery**: Proper messaging for failed transactions and rollback of debited money/restoring cart contents.

### Order Tracking & Cancellation
*   **Confirmation**: Generation of unique Order ID, receipt of Email/SMS confirmation.
*   **Live Tracking**: Visual stepper tracking order states (Order Placed -> Shipped -> Out for Delivery -> Delivered).
*   **Cancellation**: Cancellation before dispatch, refund initiation, and updating product inventory stock counts.

### Returns & Exchanges
*   **Return Process**: Return request creation window (e.g., within 14 days of delivery), selecting reason for return, and choosing refund method (Original source vs. Myntra Credit).
*   **Fashion Exchange**: Selecting alternative sizes or colors of the same product, checking stock availability for exchange, and creating reverse pickup.

---

## 5. Features Not to be Tested

*   **Third-Party Payment Gateway Internals**: Internal processing, validation of actual bank-side servers, and merchant settlement systems (Mocked interfaces will be used).
*   **Third-Party Logistics Vendors**: External warehouse management, courier dispatch software, and GPS transit maps of delivery partners.
*   **Core Server Infrastructure**: Hard rebooting of AWS/GCP servers, CDN performance, and DNS configuration.
*   **Internal Admin / Merchant Portals**: Seller product listing portals, admin dashboard metrics, and inventory upload panels.

---

## 6. Test Approach

Testing will combine Manual and Automation testing to maximize coverage and release velocity.

### Manual Testing
*   **Exploratory Testing**: Performed on the staging environment to uncover edge cases in fashion workflows (e.g., applying contradictory discount coupons).
*   **UI/UX & Usability Testing**: Validating layouts, alignment, typography, and accessibility features of the checkout pages.
*   **Ad-Hoc / Monkey Testing**: Entering random strings and payloads into search inputs and pincode checkers to test application resilience.

### Automation Testing
*   **Smoke Testing**: Automated scripts triggered on every deployment to verify critical paths (Login, Add to Cart, Checkout).
*   **Regression Testing**: Running automated end-to-end tests after bug fixes to ensure core components remain functional.
*   **Cross-Browser Testing**: Running tests concurrently on Chrome, Firefox, and Edge via cloud grid execution.

---

## 7. Test Environment

The test environment represents a replica of the production environment with mock configurations for external integrations:

| Component | Configuration |
| :--- | :--- |
| **Operating System** | Windows 11, macOS Sequoia, Android 13, iOS 16 |
| **Browsers** | Chrome (v112), Firefox (v110), Safari (v16), Edge (v111) |
| **Test Database** | MySQL Staging Database (populated with dummy customer and inventory data) |
| **API testing client** | Postman |
| **Test URL** | `https://staging-myntra-test.co.in` |
| **Mock services** | Razorpay mock gateway, SMS OTP mock service, Delhivery courier API sandbox |

---

## 8. Entry Criteria

Testing will commence only when:
*   Product Requirement Documents (PRDs) and wireframes are finalized.
*   Staging test environment is active and configured.
*   Test Plan and Test Cases are reviewed and approved.
*   The build under test is deployed successfully to the staging server.
*   Smoke test execution passes with 100% success rate.

---

## 9. Exit Criteria

Testing will be considered complete when:
*   All planned 50+ test cases have been executed.
*   The overall test case execution status is **95% or higher**.
*   All Blockers and Critical (P1) defects are fixed, verified, and closed.
*   No Major (P2) defects are left open without documented workarounds or deferrals approved by stakeholders.
*   The final Defect Report and Test Summary Report are published.

---

## 10. Test Deliverables

During the Software Testing Life Cycle (STLC), the following documents will be produced and maintained:
*   **Master Test Plan** (This document)
*   **Test Scenarios & Detailed Test Cases**
*   **Requirement Traceability Matrix (RTM)**
*   **Defect Log & Incident Reports**
*   **Daily QA Status Reports**
*   **Test Summary Report**

---

## 11. Roles and Responsibilities

| Role | Responsibility |
| :--- | :--- |
| **QA Lead** | Drafting Test Plan, defining testing strategies, assigning tasks, coordinating with stakeholders, and publishing reports. |
| **Test Engineer (Manual)** | Identifying scenarios, writing test cases, preparing test data, manual execution, logging bugs, and executing retests. |
| **Automation Engineer** | Writing, maintaining, and running Selenium test automation scripts for regression suites. |
| **Developers** | Deploying builds, resolving defects logged by the QA team, and participating in root-cause analysis. |
| **Business Analyst** | Clarifying business requirements, reviewing test cases, and signing off on changes. |

---

## 12. Test Schedule

| Activity | Start Date | End Date |
| :--- | :--- | :--- |
| **Test Planning & Requirements Review** | 22/05/2026 | 24/05/2026 |
| **Test Scenario & Case Preparation** | 25/05/2026 | 28/05/2026 |
| **Environment Setup & Sanity Testing** | 29/05/2026 | 30/05/2026 |
| **Test Execution (Cycle 1)** | 31/05/2026 | 06/06/2026 |
| **Defect Logging & Retesting** | 07/06/2026 | 10/06/2026 |
| **Regression Testing (Cycle 2)** | 11/06/2026 | 14/06/2026 |
| **Test Closure & Summary Reporting** | 15/06/2026 | 16/06/2026 |

---

## 13. Defect Management Process

Defects discovered during testing will be tracked using Jira.

### Defect Lifecycle
```text
[New] ──> [Assigned] ──> [Open] ──> [Fixed] ──> [Retest] ──> [Closed]
                             │                        ▲
                             └───> [Reopened] ────────┘
```
1.  **New**: The tester logs a bug in Jira.
2.  **Assigned**: Lead reviews and assigns the bug to the respective developer.
3.  **Open**: Developer reviews and starts working on a fix.
4.  **Fixed**: Developer deploys code fix to the staging environment.
5.  **Retest**: Tester runs the test case again to verify the fix.
6.  **Closed**: If verification succeeds, the bug status is updated to Closed.
7.  **Reopened**: If the bug is still reproducible, it is sent back with comments.

---

## 14. Risks and Mitigation

| Risk | Impact | Mitigation Strategy |
| :--- | :--- | :--- |
| **Unstable Test Environment** | High delay in execution | Maintain a backup environment or work on offline localized mock servers until staging is restored. |
| **Scope Creep / Mid-cycle Requirements Changes** | Testing deadline missed | Perform Impact Analysis immediately. Update the RTM and reprioritize test cases. |
| **Payment Gateway Downtime** | Blocked checkout/payment flows | Utilize mock payment gateways (such as Razorpay sandbox mode) with pre-defined mock success/failure card numbers. |
| **Lack of Test Data** | Poor functional coverage | Prepare a pre-populated test data sheet containing various pincodes, cards, login credentials, and expired coupons before execution. |

---

## 15. Tools Used

*   **Test Management & Tracking**: Jira, MS Excel
*   **Automation Testing**: Selenium Webdriver, Java, TestNG
*   **API Testing**: Postman (validation of search, login, and order endpoints)
*   **Performance Testing**: Apache JMeter (for load testing Cart and Checkout page API calls)
*   **Documentation**: Microsoft Word, Markdown

---

## 16. Approval Section

| Prepared By | Reviewed By | Approved By |
| :---: | :---: | :---: |
| Anjali Yadav | QA Lead | QA Manager |
| **Signature:** _Anjali_ | **Signature:** ________ | **Signature:** ________ |
| **Date:** 21/05/2026 | **Date:** ________ | **Date:** ________ |
