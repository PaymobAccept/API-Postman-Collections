# Paymob API Postman Collections 🚀

This repository contains a comprehensive suite of Postman collections designed to facilitate the integration of Paymob's payment solutions across **Egypt, Saudi Arabia, the United Arab Emirates, and Oman**. These collections cover the entire payment lifecycle, from initial intention to recurring subscriptions and post-payment operations.

---

## 📂 Collections in this Repository

### 1. Intention APIs

The Intention API is the starting point for creating, updating, or retrieving a payment request.

* 
**Unified Checkout**: Allows customers to choose their preferred payment method from a single page.


* 
**Customization**: Supports overriding default callback URLs and setting custom expiration times for payment links.



### 2. Pay with Saved Card

This collection focuses on tokenization to enable faster future transactions.

* 
**CIT (Customer Initiated Transaction)**: Requires the cardholder to be present to enter their CVV for authorization.


* 
**MIT (Merchant Initiated Transaction)**: Allows merchants to process payments via API using saved tokens without direct customer involvement.


* 
**Prerequisites**: Requires securing a card token through an initial successful 3DS transaction.



### 3. Subscription Module

Manage recurring payments with flexible billing cycles including weekly, bi-weekly, monthly, quarterly, semi-annual, and annual plans.

* 
**Plan Management**: Define billing terms, reminder days, and retrial logic for failed attempts.


* 
**Lifecycle Control**: Endpoints to suspend, resume, or permanently cancel individual customer subscriptions.


* 
**Card Management**: Add secondary cards or change the primary payment method associated with a subscription.



### 4. Refund, Void & Capture

Handle financial adjustments after a transaction has been processed.

* 
**Refund**: Reverse a transaction (Merchant to Customer), supporting both full and partial amounts.


* 
**Void**: Cancel a transaction occurred on the same business day without incurring fees.


* 
**Capture**: Finalize an authorized amount; if not captured within 14 days, the transaction is automatically voided.



### 5. Transaction Inquiry

Retrieve the status and technical details of any transaction.

* 
**Inquiry Methods**: Search using Paymob's `order_id`, your own `merchant_order_id`, or the specific `transaction_id`.


* 
**Data Access**: Provides details on success status, gateway response codes, and masked card information.



---

## 🛠️ Setup & Authentication

### 1. Generate Authentication Token

Most management APIs (like Subscriptions) require a Bearer token generated using your API Key.

* 
**Requirement**: Include your `api_key` in the request body.


* 
**Expiration**: The generated token is valid for **60 minutes**.


* 
**Usage**: Add as `Authorization: Bearer {token}` in subsequent headers.



### 2. Secret & Public Keys

* 
**Secret Key**: Used in the `Authorization` header as `Token {Secret_Key}` for Intention, Refund, Void, and Capture APIs.


* 
**Public Key**: Required to construct the Unified Checkout URL for customer redirection.



---

## 🆘 Troubleshooting

| Error | Message | Potential Solution |
| --- | --- | --- |
| **401 Unauthorized** | Invalid credentials | Verify your Secret Key and the `Token` prefix in the header.

 |
| **406 Not Acceptable** | `unmatched_item_prices` | Ensure the total `amount` exactly matches the sum of all `items`.

 |
| **404 Not Found** | ID does not exist | Ensure you are using Test IDs with Test Keys or Live IDs with Live Keys.

 |

---

## 📞 Support

* 
**Documentation**: [Paymob Developer Portal](https://developers.paymob.com).


* 
**Support Email**: [support@paymob.com](mailto:support@paymob.com).



---

**Next Step**: Would you like me to help you create a **Postman Environment template** containing these variables (`Secret_Key`, `base_url`, `Integration_ID`) so you can import it alongside these collections?
