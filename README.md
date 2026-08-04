# Stitch (stitch-money)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Stitch is a South African payments and open-banking infrastructure company. Its single GraphQL API at https://api.stitch.money/graphql powers Pay By Bank (instant EFT) and LinkPay payment initiation, bank account verification, financial data access (accounts, transactions, balances), payouts and disbursements, refunds, and signed webhook subscriptions, authenticated via OAuth2 client-credentials Bearer tokens.

> Note: This catalog covers **Stitch.money** (slug `stitch-money`), the African fintech / payments & open-banking provider at https://stitch.money. It is distinct from any unrelated "Stitch" ETL / data-integration product.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/stitch-money/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/stitch-money/refs/heads/main/apis.yml)

## Tags

- Payments
- Open Banking
- Pay By Bank
- GraphQL
- Africa
- South Africa
- Fintech

## Timestamps

- **Created:** 2026-06-21
- **Modified:** 2026-06-21

## APIs

### Stitch Payments (Pay By Bank)

Pay By Bank (instant EFT) and LinkPay payment initiation via the clientPaymentInitiationRequestCreate and clientPaymentAuthorizationRequestCreate GraphQL mutations, with payment status queried through the Relay node field and completion delivered by signed webhooks.

- **Human URL:** [https://docs.stitch.money/payment-products/payins/paybybank/integration-process](https://docs.stitch.money/payment-products/payins/paybybank/integration-process)
- **Base URL:** `https://api.stitch.money/graphql`

#### Tags

- Payments
- Pay By Bank
- Instant EFT
- GraphQL

#### Properties

- [Documentation](https://docs.stitch.money/payment-products/payins/paybybank/integration-process)
- [API Reference](https://docs.stitch.money/api)
- [OpenAPI](openapi/stitch-money-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GraphQL](graphql/stitch-money-graphql.md) — [GraphQL Specification](https://spec.graphql.org/)
- [Postman Collection](collections/stitch-money.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stitch-money.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Stitch Account Verification API

Bank account verification via the verifyBankAccountDetails GraphQL query, confirming account holder name, account number, and bank against the BankAccountVerificationInput and returning a VerifiedBankAccountDetails breakdown.

- **Human URL:** [https://docs.stitch.money/payment-products/bank-account-verification/integration-process](https://docs.stitch.money/payment-products/bank-account-verification/integration-process)
- **Base URL:** `https://api.stitch.money/graphql`

#### Tags

- Account Verification
- Bank Account
- KYC
- GraphQL

#### Properties

- [Documentation](https://docs.stitch.money/payment-products/bank-account-verification/integration-process)
- [API Reference](https://docs.stitch.money/api)
- [OpenAPI](openapi/stitch-money-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GraphQL](graphql/stitch-money-graphql.md) — [GraphQL Specification](https://spec.graphql.org/)
- [Postman Collection](collections/stitch-money.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stitch-money.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Stitch Financial Data API

User-permissioned financial data access - bank accounts, transactions, balances and debit orders - queried through the user node with bankAccounts, transactions, and runningBalance fields using a user access token.

- **Human URL:** [https://stitch.money/blog/how-to-integrate-stitch-using-graphql](https://stitch.money/blog/how-to-integrate-stitch-using-graphql)
- **Base URL:** `https://api.stitch.money/graphql`

#### Tags

- Financial Data
- Accounts
- Transactions
- Balances
- GraphQL

#### Properties

- [Documentation](https://stitch.money/blog/how-to-integrate-stitch-using-graphql)
- [API Reference](https://docs.stitch.money/api)
- [OpenAPI](openapi/stitch-money-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GraphQL](graphql/stitch-money-graphql.md) — [GraphQL Specification](https://spec.graphql.org/)
- [Postman Collection](collections/stitch-money.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stitch-money.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Stitch Payouts and Disbursements API

Outbound disbursements and payouts to beneficiary bank accounts via the clientDisbursementInitiate GraphQL mutation, using amount, destination account details, a beneficiary reference, and a nonce to enforce idempotent uniqueness.

- **Human URL:** [https://docs.stitch.money/payment-products/payouts/disbursements](https://docs.stitch.money/payment-products/payouts/disbursements)
- **Base URL:** `https://api.stitch.money/graphql`

#### Tags

- Payouts
- Disbursements
- GraphQL

#### Properties

- [Documentation](https://docs.stitch.money/payment-products/payouts/disbursements)
- [API Reference](https://docs.stitch.money/api)
- [OpenAPI](openapi/stitch-money-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GraphQL](graphql/stitch-money-graphql.md) — [GraphQL Specification](https://spec.graphql.org/)
- [Postman Collection](collections/stitch-money.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stitch-money.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Stitch Refunds API

Full and partial refunds against a prior Pay By Bank or Card payment via the clientRefundInitiate GraphQL mutation, referencing the originalPaymentId of a payment initiation request or card transaction.

- **Human URL:** [https://docs.stitch.money/payment-products/payouts/refunds](https://docs.stitch.money/payment-products/payouts/refunds)
- **Base URL:** `https://api.stitch.money/graphql`

#### Tags

- Refunds
- Payouts
- GraphQL

#### Properties

- [Documentation](https://docs.stitch.money/payment-products/payouts/refunds)
- [API Reference](https://docs.stitch.money/api)
- [OpenAPI](openapi/stitch-money-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GraphQL](graphql/stitch-money-graphql.md) — [GraphQL Specification](https://spec.graphql.org/)
- [Postman Collection](collections/stitch-money.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stitch-money.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Stitch Webhooks and Subscriptions API

Signed webhook subscriptions created per client to receive payment, disbursement, refund, and account-linking event callbacks, configured via the clientWebhookAdd GraphQL mutation against an HTTPS endpoint with a shared secret.

- **Human URL:** [https://docs.stitch.money/graphql](https://docs.stitch.money/graphql)
- **Base URL:** `https://api.stitch.money/graphql`

#### Tags

- Webhooks
- Subscriptions
- Events
- GraphQL

#### Properties

- [Documentation](https://docs.stitch.money/graphql)
- [API Reference](https://docs.stitch.money/api)
- [OpenAPI](openapi/stitch-money-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [GraphQL](graphql/stitch-money-graphql.md) — [GraphQL Specification](https://spec.graphql.org/)
- [Postman Collection](collections/stitch-money.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stitch-money.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/Stitch-Money)
- [LinkedIn](https://www.linkedin.com/company/stitchmoney)
- [Website](https://stitch.money/)
- [Documentation](https://docs.stitch.money)
- [Plans](plans/stitch-money-plans-pricing.yml)
- [Rate Limits](rate-limits/stitch-money-rate-limits.yml)
- [Fin Ops](finops/stitch-money-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
