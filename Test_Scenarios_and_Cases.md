# Myntra E-Commerce Web Application - Test Scenarios & Detailed Test Cases

This document details the test scenarios and test cases designed for validating the core functionalities of the Myntra E-commerce web application. 

The test cases are grouped by functional modules, and each test case represents real-world user workflows, including boundary cases, negative paths, and device responsiveness.

---

## Module 1: User Authentication & Session Management

### Module Summary
Validates user registration, OTP verification, third-party logins, and session timeouts.

| Test Case ID | Test Scenario | Pre-requisites | Test Steps | Test Data | Expected Result | Severity | Priority | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: |
| **TC_MYN_AUTH_001** | Register new user via Valid Mobile Number and OTP | 1. User is on login page.<br>2. Mobile number is unregistered. | 1. Click "Sign Up".<br>2. Enter a 10-digit mobile number.<br>3. Click "Continue".<br>4. Enter the received 6-digit OTP.<br>5. Click "Submit". | Mobile: `9876543210`<br>OTP: `123456` | User is registered successfully, redirected to home page, and profile icon shows initials. | Critical | High | Pass |
| **TC_MYN_AUTH_002** | Validate login with registered mobile number and valid OTP | User account already exists. | 1. Click "Login".<br>2. Enter registered mobile number.<br>3. Enter valid OTP received.<br>4. Click "Verify". | Mobile: `9999888877`<br>OTP: `888888` | User is logged in successfully and redirected to the page they were previously viewing. | Critical | High | Pass |
| **TC_MYN_AUTH_003** | Attempt login with invalid OTP | User has requested OTP. | 1. Enter registered mobile number.<br>2. Wait for OTP screen.<br>3. Enter incorrect OTP.<br>4. Click "Submit". | Mobile: `9999888877`<br>OTP: `111111` | Error message displayed: "Invalid OTP. Please try again." User is not logged in. | Major | High | Pass |
| **TC_MYN_AUTH_004** | Verify OTP resend throttling and timeout | OTP screen is active. | 1. Click login and send OTP.<br>2. Observe OTP timer (30s countdown).<br>3. Verify "Resend OTP" link is disabled during timer.<br>4. Once timer hits 0:00, click "Resend OTP".<br>5. Trigger OTP 3 consecutive times. | Mobile: `9111222333` | 1. "Resend OTP" link is disabled during countdown.<br>2. Triggering OTP > 3 times shows error: "Too many attempts. Try after 15 mins." | Major | Medium | Pass |
| **TC_MYN_AUTH_005** | Login via Google Social Sign-in OAuth | Stable internet. | 1. Click "Login".<br>2. Click "Continue with Google".<br>3. Enter valid Google credentials in OAuth pop-up.<br>4. Authorize application. | Google ID: `qa.test@gmail.com`<br>Pass: `Test@123` | Social authentication completes; Myntra session starts and registers user profile automatically. | Critical | High | Pass |
| **TC_MYN_AUTH_006** | Verify Session Timeout and Auto-Logout | User is logged in. | 1. Open Myntra.<br>2. Leave session inactive for 24 hours (simulated via cookie expiration changes).<br>3. Refresh the page. | Session cookie: `Expires/Max-Age` set to past | Session is terminated, user is redirected to public homepage, and profile shows "Login". | Minor | Low | Pass |

---

## Module 2: Product Search, Navigation & Advanced Filters

### Module Summary
Validates search accuracy, auto-suggest, sorting algorithms, and fashion-specific multi-select filters.

| Test Case ID | Test Scenario | Pre-requisites | Test Steps | Test Data | Expected Result | Severity | Priority | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: |
| **TC_MYN_SRCH_001** | Search by product name and verify auto-suggestions | On homepage. | 1. Type "nike" in search bar.<br>2. Verify auto-suggest dropdown list. | Search Query: `nike` | A dropdown appears displaying relevant tags (e.g., "nike shoes", "nike t-shirt"). | Major | High | Pass |
| **TC_MYN_SRCH_002** | Search by specific Product ID (PID) | Product exists in DB. | 1. Enter exact Product ID in search bar.<br>2. Press Enter. | PID: `2345192` (Roadster Jacket) | Direct redirection to the Product Details Page (PDP) of that specific Roadster Jacket. | Major | Medium | Pass |
| **TC_MYN_SRCH_003** | Execute search with typographical errors (Fuzzy search) | On homepage. | 1. Enter misspelled product name.<br>2. Press Enter. | Query: `adidad shoes` | Search system corrects spelling and displays Adidas shoes with text: "Showing results for **adidas shoes**". | Minor | Medium | Pass |
| **TC_MYN_SRCH_004** | Verify Search filters: Gender and Category | On search results page. | 1. Search for "T-shirts".<br>2. Under Gender filter, select "Men".<br>3. Under Category, select "Polo T-shirts". | Query: `T-shirts`<br>Gender: `Men` | Product grid updates dynamically. All products shown are Men's Polo T-shirts. | Critical | High | Pass |
| **TC_MYN_SRCH_005** | Verify Advanced Filters: Brand and Discount range | On product list page. | 1. Navigate to "Men's Sneakers".<br>2. Check "Puma" filter.<br>3. Select "30% and above" discount. | Brand: `Puma`<br>Discount: `30% and above` | All displayed items are Puma sneakers with a discount tag of at least 30%. | Major | High | Fail |
| **TC_MYN_SRCH_006** | Test Sorting: Price (Low to High) | On search listing. | 1. Search "Jeans".<br>2. Select sort option: "Price: Low to High". | Sort: `Price: Low to High` | Product listing displays jeans in ascending price order. Price labels are validated programmatically. | Major | High | Pass |
| **TC_MYN_SRCH_007** | Test Sorting: Customer Rating | On search listing. | 1. Search "Kurtas".<br>2. Select sort: "Customer Rating". | Sort: `Customer Rating` | Listing displays items from 5-star to 1-star ratings. Unrated products are pushed to the bottom. | Minor | Medium | Pass |
| **TC_MYN_SRCH_008** | Verify Search for nonexistent items | On homepage. | 1. Type random alphanumeric/gibberish text.<br>2. Press Enter. | Query: `xyz123abc456` | "No results found" page is displayed along with recommendations for popular items. | Minor | Low | Pass |

---

## Module 3: Product Details Page (PDP) & Size Guide

### Module Summary
Validates image zooming, price displays, sizing widgets, and fit guides.

| Test Case ID | Test Scenario | Pre-requisites | Test Steps | Test Data | Expected Result | Severity | Priority | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: |
| **TC_MYN_PDP_001** | Verify image carousel zoom and video playability | On PDP. | 1. Hover mouse over main product image.<br>2. Click on the 2nd thumbnail (video).<br>3. Click Play. | Product: `Wrogn Casual Shirt` | 1. Image zooms in dynamically showing fabric detail.<br>2. Video plays smoothly with audio controls. | Minor | Medium | Pass |
| **TC_MYN_PDP_002** | Validate dynamic pricing and discount calculation | Product has discounts. | 1. Fetch MRP on PDP.<br>2. Fetch Selling Price.<br>3. Calculate discount % manually and match. | MRP: `₹1999`<br>Discount: `40%`<br>Selling Price: `₹1199` | The printed selling price matches the mathematical calculation: `1999 - (0.40 * 1999) = ₹1199` (rounded). | Critical | High | Pass |
| **TC_MYN_PDP_003** | Verify size availability and out-of-stock overlay | Item has limited sizes. | 1. Navigate to a product with sold-out sizes.<br>2. Check display of sold-out size buttons.<br>3. Click a sold-out size. | Size: `S` (Out of Stock) | 1. Out of stock size button is greyed out and struck-through.<br>2. Clicking it triggers: "Get notified when back in stock" widget. | Major | High | Pass |
| **TC_MYN_PDP_004** | Verify interactive Size Chart and units conversion | On PDP. | 1. Click "Size Chart" link.<br>2. Toggle units from "In" (Inches) to "Cm" (Centimeters).<br>3. Compare values. | Unit: `Inches` vs `Cm` | 1. Size chart modal opens with a chest/waist matrix.<br>2. Toggling to "Cm" multiplies inch values by 2.54 correctly. | Major | Medium | Pass |
| **TC_MYN_PDP_005** | Verify "Fit Finder" Recommendations | User is logged in. | 1. Click "Find your size / Fit Finder".<br>2. Input height, weight, and preferred fit.<br>3. View recommended size. | Height: `180 cm`<br>Weight: `75 kg`<br>Fit: `Regular` | System recommends size "L" with text: "85% of users with your measurements bought size L". | Minor | Medium | Fail |
| **TC_MYN_PDP_006** | Verify delivery estimation pincode checker | Valid & invalid pincodes. | 1. Enter invalid pin code.<br>2. Enter valid, serviceable pin code. | Pincodes: `000000` (Invalid), `560001` (Bangalore) | 1. Invalid code shows: "Pincode is unserviceable".<br>2. Valid code shows: "Delivered by Tuesday, May 26" and COD option. | Critical | High | Pass |

---

## Module 4: Shopping Cart & Wishlist

### Module Summary
Validates adding, deleting, quantity modifications, wishlist integrations, and coupon validations.

| Test Case ID | Test Scenario | Pre-requisites | Test Steps | Test Data | Expected Result | Severity | Priority | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: |
| **TC_MYN_CART_001** | Add product to bag from PDP | Product selected. | 1. Select size (e.g., "M").<br>2. Click "Add to Bag".<br>3. Check cart badge count. | Size: `M` | 1. Cart badge count increments by 1.<br>2. Floating success notification: "Added to Bag". | Critical | High | Pass |
| **TC_MYN_CART_002** | Increase product quantity in cart | Cart has 1 item. | 1. Navigate to bag.<br>2. Click on Quantity dropdown.<br>3. Select "3".<br>4. Observe cart value update. | Quantity: `3` | 1. Quantity updates to 3.<br>2. Total price and tax recalculate instantly without reload. | Major | High | Pass |
| **TC_MYN_CART_003** | Remove item from cart | Cart has items. | 1. Navigate to Bag.<br>2. Click "Remove" button.<br>3. Confirm in popup. | Action: `Remove` | Item is removed from the bag. Cart badge count decrements. Message shows: "Bag is empty". | Major | Medium | Pass |
| **TC_MYN_CART_004** | Move item from Bag to Wishlist | Cart has items. | 1. Navigate to Bag.<br>2. Click "Move to Wishlist" link. | Action: `Move to Wishlist` | Item is removed from the cart and successfully appears in the user's Wishlist folder. | Major | Medium | Pass |
| **TC_MYN_CART_005** | Apply valid discount coupon | Cart value > threshold. | 1. Click "Apply Coupon".<br>2. Enter valid active coupon code.<br>3. Click "Apply". | Coupon: `MYNTRA200` (Min purchase: ₹1000) | Coupon discount (₹200) is deducted from order value. "Coupon applied successfully" displayed. | Critical | High | Pass |
| **TC_MYN_CART_006** | Apply coupon without meeting minimum purchase threshold | Cart value below threshold. | 1. Add item worth ₹500 to cart.<br>2. Attempt to apply coupon requiring ₹1000 min purchase. | Coupon: `MYNTRA200`<br>Cart: `₹500` | Error message: "Add items worth ₹500 more to apply this coupon." Coupon is not applied. | Major | Medium | Pass |
| **TC_MYN_CART_007** | Apply expired coupon code | Expired coupon. | 1. Add items to cart.<br>2. Type an expired coupon code.<br>3. Click Apply. | Coupon: `EXPIRED50` | Error message: "This coupon has expired." No discount applied. | Major | Low | Pass |

---

## Module 5: Checkout & Pincode Serviceability

### Module Summary
Validates shipping address flows, delivery charges, and pincode constraints.

| Test Case ID | Test Scenario | Pre-requisites | Test Steps | Test Data | Expected Result | Severity | Priority | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: |
| **TC_MYN_CHK_001** | Add new shipping address with auto-filled city/state | Logged in user in Cart. | 1. Click "Place Order" in Cart.<br>2. Click "Add New Address".<br>3. Enter PIN code.<br>4. Observe City/State fields. | Pincode: `110001` | City is auto-populated as "New Delhi" and State as "Delhi". | Major | High | Pass |
| **TC_MYN_CHK_002** | Add shipping address with missing mandatory fields | Address form open. | 1. Leave "Name" and "Mobile Number" blank.<br>2. Enter PIN and Address line.<br>3. Click "Save Address". | Empty fields: Name, Phone | Red validation borders appear under Name and Phone. Save is blocked. | Major | High | Pass |
| **TC_MYN_CHK_003** | Select default shipping address for delivery | Multiple addresses saved. | 1. Proceed to Delivery step.<br>2. Check radio button for address B.<br>3. Click "Continue to Payment". | Addresses: `Home`, `Office` | Address B is highlighted. Shipping charges update based on Address B's regional location. | Major | High | Pass |
| **TC_MYN_CHK_004** | Verify Pincode serviceability boundary check | Remote Pincode. | 1. Enter a valid pincode representing a remote location with no delivery hubs. | Pincode: `790001` (Remote district) | "Delivery not available at this location" message shown. Place order block triggered. | Major | High | Blocked |
| **TC_MYN_CHK_005** | Verify Order Total calculations at Checkout page | Cart contains products. | 1. Navigate to final address verification page.<br>2. Verify Bag Total + Delivery Charge + Tax - Coupon discount matches Net Payable. | Item: `₹1200`<br>Delivery: `₹99`<br>Tax (GST): `₹60`<br>Coupon: `-₹100` | Net Payable reads `₹1259` exactly. Calculation: `1200 + 99 + 60 - 100 = 1259`. | Critical | High | Pass |

---

## Module 6: Payments & Security

### Module Summary
Validates card processing, UPI flows, Cash on Delivery, wallet payments, and security (3DS redirection).

| Test Case ID | Test Scenario | Pre-requisites | Test Steps | Test Data | Expected Result | Severity | Priority | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: |
| **TC_MYN_PAY_001** | Complete payment using Test Credit Card (Success path) | Mock Gateway enabled. | 1. Select "Credit Card".<br>2. Enter card details, CVV, expiry.<br>3. Click Pay.<br>4. On OTP page, enter `123456`. | Card: `4111 1111 1111 1111`<br>CVV: `123`<br>OTP: `123456` | Redirection to order success page. Cart is emptied. Order status is "Order Placed". | Critical | High | Pass |
| **TC_MYN_PAY_002** | Payment failure with incorrect CVV / Expiry | On payment screen. | 1. Select Credit Card.<br>2. Enter valid card but wrong expiry date (past date).<br>3. Try to submit. | Card Expiry: `05/22` (past) | UI validation blocks submission. Error: "Please enter a valid expiry date." | Critical | High | Pass |
| **TC_MYN_PAY_003** | Verify UPI payment redirect flow (Collect Request) | UPI App active. | 1. Select UPI.<br>2. Input valid UPI ID.<br>3. Click Pay.<br>4. Trigger collect request to app. | VPA: `anjali@okaxis` | Timer (5:00 mins) starts on Myntra screen. Approving notification on UPI app completes payment and redirects Myntra. | Critical | High | Pass |
| **TC_MYN_PAY_004** | Verify UPI payment cancellation by user | UPI screen. | 1. Initiate UPI payment.<br>2. On UPI redirect screen, click "Cancel Transaction". | Action: `Cancel` | Transaction is cancelled. User is taken back to Checkout payment page with cart items intact. | Major | High | Pass |
| **TC_MYN_PAY_005** | Verify Cash on Delivery (COD) order flow | COD available for PIN. | 1. Select "Cash on Delivery" option.<br>2. Enter CAPTCHA characters shown.<br>3. Click "Confirm Order". | CAPTCHA match | Order is placed successfully. Success page shows: "Payment due at delivery: ₹1259". | Critical | High | Pass |
| **TC_MYN_PAY_006** | Place order combining Myntra Credits & Credit Card | Wallet has balance. | 1. Check "Use Myntra Credits".<br>2. Wallet balance (e.g., ₹500) is applied.<br>3. Select Credit Card for remaining ₹759. | Wallet: `₹500`<br>Cart: `₹1259` | Wallet is debited, card payment of ₹759 is triggered, order successfully processed. | Major | Medium | Pass |
| **TC_MYN_PAY_007** | Validate payment screen session timeout | On payment gateway. | 1. Redirect to payment page.<br>2. Do not interact for 10 minutes.<br>3. Attempt to enter details after timeout. | Timeout: `10 mins` | Session expires. User redirected to cart page with error: "Transaction timed out. Please try again." | Major | Medium | Pass |
| **TC_MYN_PAY_008** | Verify payment processing error - bank server down | Simulating server error. | 1. Select Net Banking (SBI).<br>2. Initiate payment.<br>3. Mock response: `Bank Server 500`. | Bank: `SBI` (Mock Down) | User redirected back to payment page with error: "Bank server is busy. Your money (if debited) will be refunded." | Critical | High | Fail |

---

## Module 7: Order Management, Tracking & Returns/Exchanges

### Module Summary
Validates order history details, status tracking, cancellations, and return/exchange workflows.

| Test Case ID | Test Scenario | Pre-requisites | Test Steps | Test Data | Expected Result | Severity | Priority | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: |
| **TC_MYN_ORD_001** | Verify invoice generation and download | Order is placed. | 1. Go to "Orders".<br>2. Select active order.<br>3. Click "Download Invoice". | Order: `OD-1928371` | PDF invoice downloads containing correct seller details, GSTIN, item pricing, and address. | Major | Medium | Pass |
| **TC_MYN_ORD_002** | Cancel an order before shipment | Order status is "Placed". | 1. Go to "Orders".<br>2. Click "Cancel Order".<br>3. Select reason (e.g., "Change of mind").<br>4. Submit. | Reason: `Change of mind` | Order status changes to "Cancelled". Refund email triggered. Product stock restocked in DB. | Critical | High | Pass |
| **TC_MYN_ORD_003** | Verify Order cancellation block post-shipment | Order status: "Shipped". | 1. Navigate to "Orders" for a shipped item. | Order Status: `Shipped` | "Cancel Order" button is hidden. User must use return/refusal at doorstep instead. | Major | Medium | Pass |
| **TC_MYN_ORD_004** | Verify live order tracking statuses | Order in transit. | 1. Go to "Orders".<br>2. Click "Track".<br>3. Compare tracking stages (Placed -> Dispatched -> In Transit -> Out for Delivery -> Delivered). | Courier API data | Visual tracking stepper updates accurately according to mockup API events. | Major | High | Pass |
| **TC_MYN_ORD_005** | Request refund return within 14-day window | Order delivered today. | 1. Go to "Orders".<br>2. Click "Return".<br>3. Select reason & refund destination (Myntra Credit).<br>4. Confirm return slot. | Refund Mode: `Myntra Credit` | Return request approved. Return pickup scheduled. Mock pickup ID generated. | Critical | High | Pass |
| **TC_MYN_ORD_006** | Request Size Exchange for clothing product | Order delivered today. | 1. Go to "Orders".<br>2. Click "Exchange".<br>3. Select size "XL" instead of "L".<br>4. Select exchange pickup date.<br>5. Confirm. | Current size: `L`<br>Exchange size: `XL` | Exchange request created. Reverse pickup of "L" and delivery of "XL" created in logistics database. | Critical | High | Fail |
| **TC_MYN_ORD_007** | Verify Return Request rejection post 14-day return window | Order delivered 15 days ago. | 1. Locate older order in History.<br>2. Check for Return button. | Order Date: `06/05/2026` | "Return" and "Exchange" buttons are disabled/hidden for this order. | Major | Medium | Pass |

---

## Module 8: Myntra Insider Loyalty Program

### Module Summary
Validates loyalty points accumulation, coupon redemption, and tier upgrades.

| Test Case ID | Test Scenario | Pre-requisites | Test Steps | Test Data | Expected Result | Severity | Priority | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: |
| **TC_MYN_INSD_001** | Verify loyalty points accumulation on order delivery | Delivered order exists. | 1. Order delivered successfully.<br>2. Navigate to Myntra Insider dashboard.<br>3. Check points balance. | Order Value: `₹2000`<br>Accrual rate: `₹1 = 1 point` | User is credited 2000 Insider points. Balance updates correctly. | Minor | Medium | Pass |
| **TC_MYN_INSD_002** | Redeem Insider points for coupon rewards | User has 1000 points. | 1. Go to Insider rewards catalog.<br>2. Select "₹100 Off Coupon".<br>3. Click "Redeem Points". | Reward ID: `COUP-100` | Points balance decrements by 1000. Unique discount coupon code is generated and added to user's profile. | Minor | Medium | Pass |
| **TC_MYN_INSD_003** | Verify Tier Upgrade (Insider -> Select -> Elite) | Points cross threshold. | 1. Place high-value orders to cross Elite tier threshold (e.g., 5000 points).<br>2. Complete delivery. | Cumulative points: `5200` | User tier upgrades to "Elite". "Elite Member" badge displayed on profile, unlocking free shipping. | Minor | Low | Pass |
