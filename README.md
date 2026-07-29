# Paymob API Postman Collections

This repository contains the official Postman collections for integrating **Paymob's payment products**. Seven collections cover two products: **Accept** (payment acceptance — intentions, saved cards, subscriptions, refunds, inquiries, payment links) and **Payouts** (disbursements). Accept is available in **Egypt, Saudi Arabia (KSA), United Arab Emirates (UAE), and Oman**; Payouts is available in **Egypt, UAE, and KSA**.

---

## 📂 Collections Overview

### Accept APIs

#### 1. Intention APIs
The **Intention API** is the modern way to initiate payments, supporting multiple payment methods (Cards, Wallets, Kiosk, etc.) through a single integration point.
* **Unified Checkout**: Redirect customers to a Paymob-hosted page where they can choose their preferred method.
* **Customization**: Supports overriding callback URLs and setting specific expiration times for each payment link.

#### 2. Pay with Saved Card
Enable a seamless "One-Click" checkout experience by using tokenization. Tokens are generated after a successful 3DS transaction.
* **CIT (Customer Initiated)**: For returning customers who are present during checkout (requires CVV).
* **MIT (Merchant Initiated)**: For automated charges like subscriptions or top-ups where the customer is not present.

#### 3. Subscription Module
A specialized tool for managing recurring billing, supporting weekly, bi-weekly, monthly, quarterly, and annual cycles.
* **Plan Management**: Create plans with specific retrial logic and reminder days for failed payments.
* **Lifecycle APIs**: Endpoints to suspend, resume, or cancel subscriptions programmatically.

#### 4. Refund, Void & Capture
Essential post-payment operations for financial management and order fulfillment.
* **Refund / Void**: Full or partial reversal of a transaction, or instant cancellation of a same-day transaction to avoid processing fees.
* **Capture**: Finalize an "Authorize-only" transaction. Amounts not captured within 14 days are automatically voided.

#### 5. Transaction Inquiry
Deep-dive into your transaction history for reconciliation or customer support.
* **Search Flexibility**: Query using your own `merchant_order_id`, Paymob's `order_id`, or the specific `transaction_id`.
* **Card Tokens**: Retrieve the saved card tokens associated with an order.

#### 6. V2 QuickLink
Generate shareable payment links for customers without building a checkout flow.
* **Create & Cancel**: Send an amount, customer details, and integration to get a shareable URL; cancel it before it is paid.
* **Live / Test**: The `is_live` flag selects between test and live behaviour for the link.

### Payouts APIs

#### 7. Payouts
A **separate product** for sending money out — different hosts, different authentication, and staging/production environments rather than country-only.
* **Instant Cashin**: Disburse to Vodafone Cash, Etisalat Cash, Orange Cash, bank wallets, bank cards, instant bank transfers, and Egypt Post.
* **Inquiries & Topup**: Bulk transaction inquiry by ID or your own reference, budget inquiry, and topup by bank transfer or from your Accept balance.
* **Auth**: OAuth2 password grant with refresh tokens — the access token is captured and applied automatically.

> **Note:** Four Payouts requests (Bulk Transaction Inquiry by Reference and the three Topup requests) carry an inline caveat that their endpoint path was inferred from naming convention. Verify them against the live docs before relying on them.

---

## 🌍 Base URLs & Environments

Each environment file sets exactly one variable — the base URL — and nothing else.

### Accept — `base_url`

| Country | Base URL | Environment |
| :--- | :--- | :--- |
| **Egypt** | `https://accept.paymob.com` | `EGY` |
| **Saudi Arabia** | `https://ksa.paymob.com` | `KSA` |
| **UAE** | `https://uae.paymob.com` | `UAE` |
| **Oman** | `https://oman.paymob.com` | `OMN` |

### Payouts — `payouts_base_url`

| Country | Environment Type | Base URL | Environment |
| :--- | :--- | :--- | :--- |
| **Egypt** | Staging | `https://stagingpayouts.paymobsolutions.com` | `PAYOUTS-EGY-STAGING` |
| **Egypt** | Production | `https://payouts.paymobsolutions.com` | `PAYOUTS-EGY-PROD` |
| **UAE** | Staging | `https://stagingpayouts-uae.paymobsolutions.com` | `PAYOUTS-UAE-STAGING` |
| **UAE** | Production | `https://payouts-uae.paymobsolutions.com` | `PAYOUTS-UAE-PROD` |
| **KSA** | Staging | `https://stagingpayouts.paymob.sa` | `PAYOUTS-KSA-STAGING` |
| **KSA** | Production | `https://payouts.paymob.sa` | `PAYOUTS-KSA-PROD` |

**How it works:** import the files from `environments/`, then pick one from the environment dropdown at the top-right of Postman. The environment value overrides the collection's default, so switching from `EGY` to `KSA` re-points every request in every Accept collection without editing anything. With no environment selected, the collection defaults apply — Egypt for Accept, Egypt-staging for Payouts.

The two products use different variable names on purpose: an Accept environment sets only `base_url` and a Payouts environment sets only `payouts_base_url`, so selecting the wrong one can never redirect a request to the other product's host.

> ⚠️ These files are committed to the repository. Do **not** type API keys, secrets, or passwords into them — anything saved in an environment is written to the file. Keep credentials in the collection variables or in a private environment you don't commit.

---

## 🛠️ Setup & Authentication

1. **Import**: Download the `.json` files and import them into your Postman Workspace — both the collections at the root (`<Name>.postman_collection.json`) and the environment files under `environments/` (`<NAME>.postman_environment.json`).
2. **Authentication**: Three mechanisms are used across the collections.
   * **Secret Key** — used for Intentions and Post-pay APIs. Header format: `Authorization: Token {{secret_key}}`.
   * **API Key → Bearer Token** — post your `{{API_KEY}}` to `/api/auth/tokens` to receive a 60-minute token, then send it as `Authorization: Bearer {{auth_token}}`. Used by Subscriptions, Transaction Inquiry, and QuickLink.
   * **OAuth2 (Payouts only)** — `generate_token` exchanges `CLIENT_ID` / `CLIENT_SECRET` / `USERNAME` / `PASSWORD` for an access token. The collection stores it automatically in `TOKEN` and applies it to every request, so no manual copying is needed. Use `refresh_token` when it expires.
3. **Variables**: `base_url` and `payouts_base_url` ship with working defaults (Egypt, and Egypt-staging for Payouts), so a freshly imported collection runs without any setup. Everything else — your keys and IDs — is declared in each collection with an empty value, ready to fill in.

---

## 🔑 Variables

Every variable used by a request is declared in its collection with an empty value, so it appears in Postman's variable editor after import. These are the ones you fill in:

| Variable | What it is |
| :--- | :--- |
| `secret_key` | Secret key sent as `Authorization: Token …` |
| `API_KEY`, `auth_token` | API key, and the 60-minute bearer token it returns |
| `integration_id` | Payment-method integration ID |
| `public_key`, `client_secret` | Build the Unified Checkout redirect URL |
| `merchant_order_id`, `transaction_id` | Your own order reference / Paymob's transaction ID |
| `CLIENT_ID`, `CLIENT_SECRET`, `USERNAME`, `PASSWORD` | Payouts OAuth2 credentials |
| `TOKEN`, `REFRESH_TOKEN` | Payouts — populated automatically, leave empty |

Billing fields (`first_name`, `last_name`, `email`, `phone_number`, `amount_cents`) use the same name in every Accept collection, so one set of values works across all of them.

---

## 📞 Support & Documentation

* **Official Docs**: [Paymob Developer Portal](https://developers.paymob.com)
* **Support**: For technical assistance, contact [support@paymob.com](mailto:support@paymob.com) or reach out to your account manager.

---
*Maintained by the Paymob Technical Support Team.*
