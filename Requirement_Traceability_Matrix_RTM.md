# Requirement Traceability Matrix (RTM) - Myntra E-Commerce Website Testing

An RTM is a critical QA artifact that maps Functional Requirements (FR) to the corresponding Test Cases (TC). This matrix ensures that 100% of the project specifications are tested and helps trace test coverage.

## Traceability Summary
*   **Total Functional Requirements (FRs)**: 34
*   **Total Test Cases Created**: 50
*   **Coverage Status**: 100% (Every functional requirement has at least one associated test case)

---

## 🔗 Traceability Matrix Table

| Requirement ID | Module Name | Functional Requirement Description | Associated Test Case ID(s) | Status (Covered / Not Covered) |
| :--- | :--- | :--- | :--- | :---: |
| **FR_AUTH_01** | Authentication | User registration via valid Indian mobile number and OTP. | `TC_MYN_AUTH_001` | Covered |
| **FR_AUTH_02** | Authentication | Login using registered mobile number and OTP verification. | `TC_MYN_AUTH_002`, `TC_MYN_AUTH_003` | Covered |
| **FR_AUTH_03** | Authentication | Protect OTP requests with resend timers and attempt limits. | `TC_MYN_AUTH_004` | Covered |
| **FR_AUTH_04** | Authentication | Social Sign-in integration using Google/Facebook login. | `TC_MYN_AUTH_005` | Covered |
| **FR_AUTH_05** | Authentication | Session timeout enforcement after designated period of inactivity. | `TC_MYN_AUTH_006` | Covered |
| **FR_SRCH_01** | Search & Navigation | Auto-suggest search keywords based on partial user input. | `TC_MYN_SRCH_001` | Covered |
| **FR_SRCH_02** | Search & Navigation | Search lookup for exact Product ID (PID) redirecting to PDP. | `TC_MYN_SRCH_002` | Covered |
| **FR_SRCH_03** | Search & Navigation | Fuzzy search/spell check search engine logic. | `TC_MYN_SRCH_003` | Covered |
| **FR_SRCH_04** | Search & Navigation | Multi-select filters for Gender, Category, and Brand. | `TC_MYN_SRCH_004`, `TC_MYN_SRCH_005` | Covered |
| **FR_SRCH_05** | Search & Navigation | Discount-based filtering on product list page. | `TC_MYN_SRCH_005` | Covered |
| **FR_SRCH_06** | Search & Navigation | Product list sorting (Price, Rating, Popularity). | `TC_MYN_SRCH_006`, `TC_MYN_SRCH_007` | Covered |
| **FR_SRCH_07** | Search & Navigation | Zero search results handling and recommendations. | `TC_MYN_SRCH_008` | Covered |
| **FR_PDP_01** | Product Details Page | Zoom feature on hover and video playback of product. | `TC_MYN_PDP_001` | Covered |
| **FR_PDP_02** | Product Details Page | Correct calculation and display of Selling Price and discounts. | `TC_MYN_PDP_002` | Covered |
| **FR_PDP_03** | Product Details Page | Dynamic visibility of size buttons (active, out-of-stock, notified). | `TC_MYN_PDP_003` | Covered |
| **FR_PDP_04** | Product Details Page | Interactive size chart modal with unit toggle (Inches/Cm). | `TC_MYN_PDP_004` | Covered |
| **FR_PDP_05** | Product Details Page | "Fit Finder" size recommendations based on user profiles. | `TC_MYN_PDP_005` | Covered |
| **FR_PDP_06** | Product Details Page | Pincode estimator for delivery dates and COD serviceability. | `TC_MYN_PDP_006` | Covered |
| **FR_CART_01** | Shopping Bag | Add items to shopping bag with selected color/size. | `TC_MYN_CART_001` | Covered |
| **FR_CART_02** | Shopping Bag | Modify quantity of items in bag and update price components. | `TC_MYN_CART_002` | Covered |
| **FR_CART_03** | Shopping Bag | Delete items from the shopping bag. | `TC_MYN_CART_003` | Covered |
| **FR_CART_04** | Shopping Bag | Move items from Bag to Wishlist folder and vice-versa. | `TC_MYN_CART_004` | Covered |
| **FR_CART_05** | Shopping Bag | Apply promo coupons at cart based on eligibility/min purchase. | `TC_MYN_CART_005`, `TC_MYN_CART_006`, `TC_MYN_CART_007` | Covered |
| **FR_CHK_01** | Checkout | Add/Edit shipping addresses with city/state auto-population. | `TC_MYN_CHK_001`, `TC_MYN_CHK_002` | Covered |
| **FR_CHK_02** | Checkout | Choose default delivery address from multiple saved addresses. | `TC_MYN_CHK_003` | Covered |
| **FR_CHK_03** | Checkout | Pincode-level shipping block for unserviceable locations. | `TC_MYN_CHK_004` | Covered |
| **FR_CHK_04** | Checkout | Invoice price summary validation (Bag total, taxes, discounts). | `TC_MYN_CHK_005` | Covered |
| **FR_PAY_01** | Payments | Process credit/debit card transactions securely via gateway. | `TC_MYN_PAY_001`, `TC_MYN_PAY_002` | Covered |
| **FR_PAY_02** | Payments | UPI transaction collection and verification flow. | `TC_MYN_PAY_003`, `TC_MYN_PAY_004` | Covered |
| **FR_PAY_03** | Payments | CAPTCHA authentication for Cash on Delivery (COD) orders. | `TC_MYN_PAY_005` | Covered |
| **FR_PAY_04** | Payments | Split payments using Myntra Credit wallets and credit card. | `TC_MYN_PAY_006` | Covered |
| **FR_PAY_05** | Payments | Handle payment timeouts and server-side payment failures. | `TC_MYN_PAY_007`, `TC_MYN_PAY_008` | Covered |
| **FR_ORD_01** | Order & Tracking | Print/Download invoice PDF of placed orders. | `TC_MYN_ORD_001` | Covered |
| **FR_ORD_02** | Order & Tracking | Order cancellation prior to dispatch. | `TC_MYN_ORD_002`, `TC_MYN_ORD_003` | Covered |
| **FR_ORD_03** | Order & Tracking | Live shipment tracking stages integration. | `TC_MYN_ORD_004` | Covered |
| **FR_ORD_04** | Order & Tracking | Process return requests and specify refund destinations. | `TC_MYN_ORD_005`, `TC_MYN_ORD_007` | Covered |
| **FR_ORD_05** | Order & Tracking | Size/Color exchange flow for apparel and footwear. | `TC_MYN_ORD_006` | Covered |
| **FR_INSD_01** | Loyalty Program | Accumulate loyalty points based on delivered order values. | `TC_MYN_INSD_001` | Covered |
| **FR_INSD_02** | Loyalty Program | Redeem Insider points for merchant gift coupons. | `TC_MYN_INSD_002` | Covered |
| **FR_INSD_03** | Loyalty Program | Automate user tier upgrade (Select/Elite) on point milestones. | `TC_MYN_INSD_003` | Covered |
