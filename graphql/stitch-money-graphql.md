# Stitch GraphQL API

The [Stitch](https://stitch.money/) payments and open-banking platform is exposed through a
single GraphQL API. All payment, verification, financial-data, disbursement, refund, and
webhook operations are sent as GraphQL queries and mutations to one endpoint.

- API endpoint: `https://api.stitch.money/graphql` (same URL for test and live clients)
- API reference: <https://docs.stitch.money/api>
- Using GraphQL guide: <https://docs.stitch.money/graphql>
- GraphiQL IDE: <https://ide.stitch.money/>
- GitHub: <https://github.com/Stitch-Money>

> This document covers **Stitch.money**, the South African fintech / payments & open-banking
> provider. It is distinct from any unrelated "Stitch" ETL / data-integration product.

---

## Transport

Stitch uses GraphQL over HTTP. Every request is an HTTP `POST https://api.stitch.money/graphql`
with a JSON body of `{ "query": "...", "variables": { ... } }` and an
`Authorization: Bearer <token>` header. The API follows the Relay server specification, so
collections are exposed as `connection { edges { node { ... } } }` with cursor-based
pagination (`first`, `after`), and single records are fetched through the top-level
`node(id: ...)` field with inline fragments (`... on PaymentInitiationRequest`).

---

## Authentication

Stitch issues OAuth2 Bearer tokens. There are two token types:

| Token type | Grant | Used for |
|------------|-------|----------|
| **Client token** | OAuth2 `client_credentials` (client_id + client_secret / signed client assertion) | Payment requests, disbursements, refunds, bank account verification, webhook config. Scoped, e.g. `client_paymentrequest`, `client_disbursement`, `client_refund`. |
| **User access token** | OAuth2 authorization-code (`code` + PKCE) | Retrieving a user's permissioned financial data (accounts, transactions, balances) and LinkPay account linking. |

The resulting access token is sent as `Authorization: Bearer <token>` on every GraphQL call.

---

## Key operations

### Create a Pay By Bank payment (mutation)

```graphql
mutation CreatePaymentRequest(
  $amount: MoneyInput!
  $payerReference: String!
  $beneficiaryReference: String!
  $externalReference: String
  $beneficiaryName: String!
  $beneficiaryBankId: BankBeneficiaryBankId!
  $beneficiaryAccountNumber: String!
  $expireAt: Date
) {
  clientPaymentInitiationRequestCreate(input: {
    amount: $amount
    payerReference: $payerReference
    beneficiaryReference: $beneficiaryReference
    externalReference: $externalReference
    expireAt: $expireAt
    beneficiary: {
      bankAccount: {
        name: $beneficiaryName
        bankId: $beneficiaryBankId
        accountNumber: $beneficiaryAccountNumber
      }
    }
  }) {
    paymentInitiationRequest {
      id
      url
    }
  }
}
```

### Query payment status (Relay node)

```graphql
query GetPaymentRequestStatus($paymentRequestId: ID!) {
  node(id: $paymentRequestId) {
    ... on PaymentInitiationRequest {
      id
      state {
        __typename
        ... on PaymentInitiationRequestCompleted { date amount }
        ... on PaymentInitiationRequestPending { __typename }
        ... on PaymentInitiationRequestCancelled { reason }
        ... on PaymentInitiationRequestExpired { __typename }
      }
    }
  }
}
```

### LinkPay account linking and reuse (mutations)

```graphql
mutation LinkAccount {
  clientPaymentAuthorizationRequestCreate(input: { ... }) {
    paymentAuthorizationRequest { id url }
  }
}

mutation PayWithLinkedAccount {
  userInitiatePayment(input: { ... }) {
    paymentInitiation { id }
  }
}
```

### Cancel a payment (mutation)

```graphql
mutation CancelPayment($id: ID!) {
  clientPaymentInitiationRequestCancel(input: { paymentRequestId: $id }) {
    paymentInitiationRequest { id }
  }
}
```

### Verify a bank account (query)

```graphql
query VerifyBankAccount($input: BankAccountVerificationInput!) {
  verifyBankAccountDetails(input: $input) {
    accountVerificationResult
    accountHolderVerified
    accountNumberVerified
    accountOpen
  }
}
```

### Financial data — accounts and transactions (query, user token)

```graphql
query UserTransactions {
  user {
    bankAccounts {
      accountNumber
      currentBalance
      transactions(first: 50) {
        edges {
          node {
            id
            amount
            reference
            description
            date
            runningBalance
          }
        }
      }
    }
  }
}
```

### Create a disbursement / payout (mutation)

```graphql
mutation CreateDisbursement(
  $amount: MoneyInput!
  $nonce: String!
  $beneficiaryReference: String!
) {
  clientDisbursementInitiate(input: {
    amount: $amount
    nonce: $nonce
    beneficiaryReference: $beneficiaryReference
    beneficiary: { bankAccount: { name: "...", bankId: ..., accountNumber: "..." } }
  }) {
    disbursement { id status }
  }
}
```

### Issue a refund (mutation)

```graphql
mutation CreateRefund($originalPaymentId: ID!, $amount: MoneyInput!, $nonce: String!) {
  clientRefundInitiate(input: {
    originalPaymentId: $originalPaymentId
    amount: $amount
    nonce: $nonce
    reason: "duplicate"
  }) {
    refund { id status }
  }
}
```

### Register a webhook subscription (mutation)

```graphql
mutation AddWebhook($url: URL!, $secret: String!) {
  clientWebhookAdd(input: { url: $url, secret: $secret }) {
    webhook { id url }
  }
}
```

Stitch signs every webhook callback (e.g. payment completed/failed, disbursement, refund,
account-linking events). For LinkPay, completion/failure is always delivered as a signed
webhook to the client's subscribed endpoint.

---

## Schema

See [`stitch-money-schema.graphql`](./stitch-money-schema.graphql) for a representative SDL
subset of the Stitch GraphQL schema. The authoritative, complete and current schema is
available from the Stitch IDE Docs tab and can be downloaded with `gql-sdl`:

```
gql-sdl https://api.stitch.money/graphql --sdl -o stitch.graphql
```
