# Paymob API Postman Collections

This repository contains the official Postman collections for integrating **Paymob's Payment Gateway**. These collections are designed to help developers quickly test and implement payment flows across **Egypt, Saudi Arabia (KSA), United Arab Emirates (UAE), and Oman**.

---

## 📂 Collections Overview

### 1. Intention APIs
The **Intention API** is the modern way to initiate payments. It allows you to create a payment request that supports multiple payment methods (Cards, Wallets, Kiosk, etc.) through a single integration point.
* **Unified Checkout**: Redirect customers to a Paymob-hosted page where they can choose their preferred method.
* **Customization**: Supports overriding callback URLs and setting specific expiration times for each payment link.

### 2. Pay with Saved Card
Enable a seamless "One-Click" checkout experience by using tokenization.
* **CIT (Customer Initiated)**: For returning customers who are present during checkout (requires CVV).
* **MIT (Merchant Initiated)**: For automated charges like subscriptions or top-ups where the customer is not present.
* **Security**: Tokens are generated after a successful 3DS transaction, ensuring the card is valid and authorized.



### 3. Subscription Module
A specialized tool for managing recurring billing and automated payment cycles.
* **Flexible Cycles**: Support for weekly, bi-weekly, monthly, quarterly, and annual billing.
* **Plan Management**: Create plans with specific retrial logic and reminder days for failed payments.
* **Lifecycle APIs**: Endpoints to suspend, resume, or cancel subscriptions programmatically.

### 4. Refund, Void & Capture
Essential post-payment operations for financial management and order fulfillment.
* **Refund**: Full or partial reversal of a transaction (Merchant to Customer).
* **Void**: Instant cancellation of same-day transactions to avoid processing fees.
* **Capture**: Finalize an "Authorize-only" transaction. Note: Amounts not captured within 14 days are automatically voided.

### 5. Transaction Inquiry
Deep-dive into your transaction history for reconciliation or customer support.
* **Search Flexibility**: Query transactions using your own `merchant_order_id`, Paymob's `order_id`, or the specific `transaction_id`.
* **Technical Insights**: Retrieve gateway response codes and detailed payment metadata.

---

## 🌍 Regional Base URLs

Use the appropriate URL based on your merchant account region:

| Country | Base URL |
| :--- | :--- |
| **Egypt** | `https://accept.paymob.com` |
| **Saudi Arabia** | `https://ksa.paymob.com` |
| **UAE** | `https://uae.paymob.com` |
| **Oman** | `https://oman.paymob.com` |

---

## 🛠️ Setup & Authentication

1. **Import Collections**: Download the `.json` files from this repository and import them into your Postman Workspace.
2. **Authentication**:
   * **Secret Key**: Used for Intentions and Post-pay APIs. Header format: `Authorization: Token <YOUR_SECRET_KEY>`.
   * **API Key**: Used to generate a 60-minute Bearer Token for management APIs (like Subscriptions).
3. **Variables**: We recommend creating a Postman Environment with the following keys: `base_url`, `Secret_Key`, `api_key`, and `Integration_ID`.



---

## 🆘 Common Troubleshooting

| Error Code | Meaning | Action |
| :--- | :--- | :--- |
| **401 Unauthorized** | Invalid Credentials | Check if you are using a Test Key in a Live environment or vice-versa. |
| **406 Not Acceptable** | Amount Mismatch | Ensure the total `amount` equals the sum of individual `items` in the request. |
| **404 Not Found** | Resource Missing | Verify the ID (Transaction/Order) exists in the specific region you are querying. |

---

## 📞 Support & Documentation

* **Official Docs**: [Paymob Developer Portal](https://developers.paymob.com)
* **Support**: For technical assistance, contact [support@paymob.com](mailto:support@paymob.com) or reach out to your account manager.

---
*Maintained by the Paymob Technical Support Team.*
