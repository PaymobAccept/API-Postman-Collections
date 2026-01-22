# Paymob API Postman Collections

Welcome to the official **Paymob API Postman Collections** repository. This project provides a comprehensive set of API tools and documentation for developers looking to integrate Paymob's payment solutions into their platforms across **Egypt, Saudi Arabia, UAE, and Oman**.

---

## 📂 Collections Overview

This repository contains five specialized Postman collections, each designed to handle specific payment lifecycles and business logic.

### 1. **Intention APIs** 💳

The core of the Paymob unified experience. Use these APIs to create, update, and retrieve payment requests.

* 
**Key Feature:** Supports unified checkout where customers can choose from multiple payment methods.


* 
**Main Endpoint:** `POST /v1/intention/`.



### 2. **Pay with Saved Card** 🔐

Enable seamless returning-customer experiences through tokenization.

* 
**CIT (Customer Initiated):** Returning customers pay by simply entering their CVV.


* 
**MIT (Merchant Initiated):** Charge saved tokens via API for background processing.


* 
**Workflow:** Create Intention  Unified Checkout  Tokenization Callback.



### 3. **Subscription Module** 🔄

Manage recurring billing for services, memberships, or installments.

* 
**Flexible Cycles:** Weekly, Monthly, Quarterly, or Annual plans.


* 
**Lifecycle Management:** APIs for suspending, resuming, and canceling active subscriptions.


* 
**Card Management:** Add secondary cards or change the primary payment method for any user.



### 4. **Refund, Void & Capture** 💸

Post-transaction management tools to handle financial operations.

* 
**Refund:** Reverse transactions (Merchant to Customer) with optional partial refunds.


* 
**Void:** Cancel a same-day transaction before settlement to avoid fees.


* 
**Capture:** Finalize an authorized transaction within 14 days.



### 5. **Transaction Inquiry** 🔍

Retrieve deep technical details and statuses for any transaction.

* 
**Search Methods:** Query by `transaction_id`, `order_id`, or your own `merchant_order_id`.


* 
**Detailed Response:** Access card metadata, gateway response codes, and customer billing info.



---

## 🛠️ Getting Started

### Prerequisites

1. 
**Paymob Dashboard Account:** Sign up at [accept.paymob.com](https://accept.paymob.com).


2. 
**API Keys:** Locate your **Secret Key**, **Public Key**, and **API Key** in the **Settings → Account Info** section of your dashboard.


3. 
**Integration IDs:** Configure your desired payment methods (Cards, Wallets, etc.) in **Developers → Payment Integrations**.



### Setup Instructions

1. **Import Collections:** Download the `.json` files from this repo and import them into your Postman Workspace.
2. **Configure Environment:**
* Set `base_url` (e.g., `https://accept.paymob.com` for Egypt).


* Set `Secret_Key` (format: `Token sk_test_...`).


* Set `API_KEY` to generate your 60-minute **Authentication Token**.





---

## 🔐 Security & Webhooks

* 
**HMAC Validation:** Always verify the HMAC signature on callbacks (Transaction Processed, Token Created) to ensure data integrity.


* 
**Token Security:** Store saved card tokens securely in your database; never store raw card numbers.



---

## 🆘 Troubleshooting & Support

| Common Error | Likely Cause | Solution |
| --- | --- | --- |
| **401 Unauthorized** | Invalid Secret Key | Check the `Authorization` header format.

 |
| **406 Not Acceptable** | `unmatched_item_prices` | Ensure `amount` = sum of all `items[].amount`.

 |
| **404 Not Found** | Invalid Integration ID | Ensure you use Live IDs with Live Keys (and vice-versa).

 |

**Developer Resources:**

* 📖 [Official Documentation](https://developers.paymob.com) 


* 📧 [Support Email](mailto:support@paymob.com) 



---

**Next Steps**
Would you like me to help you format the specific Postman environment template to match these collections so you can include it in the repository as well?
