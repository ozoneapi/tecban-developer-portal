# AISP Resources and Data Models - v3.1.2

Resources accessed using the aisp PSD2 role are detailed below.

## Table of Contents

  - [Resource Details](#markdown-header-resource-details)
      - [Account Access Consents](#markdown-header-account-access-consents)
      - [Accounts](#markdown-header-accounts)
      - [Balances](#markdown-header-balances)
      - [Transactions](#markdown-header-transactions)
      - [Beneficiaries](#markdown-header-beneficiaries)
      - [Products](#markdown-header-products)
      - [Direct Debits](#markdown-header-direct-debits)
      - [Standing Orders](#markdown-header-standing-orders)
      - [Scheduled Payments](#markdown-header-scheduled-payments)
      - [Parties](#markdown-header-parties)
      - [Statements](#markdown-header-statements)
  - [Endpoints](#markdown-header-endpoints)

## Resource Details

Below we have captured the TecBan specific details of the standard API endpoints.

### Account Access Consents

**[Account Access Consents API](Account%20Access%20Consents.md)**

### Accounts

**[Accounts API](Accounts.md)**

TecBan members will have one of the following accounts:

 *  E-money Business Wallet
 *  Business Current Account

### Balances

**[Balances API](Balances.md)**

Balances shown in this endpoint include `Expected`, `InterimAvailable` and `InterimCleared`, however `Expected` balance is the value displayed most widely to our members within the TecBan apps.

### Transactions

**[Transactions API](Transactions.md)**

### Beneficiaries

**[Beneficiaries API](Beneficiaries.md)**

Payment recipients are accessible via the Beneficiaries API.  Payments are currently only permitted to pre-registered beneficiaries or one of the Member's other accounts (for account transfers).  This API is useful when setting up payments.

### Products

**[Products API](Products.md)**

TecBan currently offers Business Current Accounts and Business E-Money Accounts.

### Direct Debits

**[Direct Debits API](Direct%20Debits.md)**

### Standing Orders

**[Standing Orders API](Standing%20Orders.md)**

DateTime elements have been used so that there is consistency across all API endpoints using dates. However, for Standing Orders we only process based on the day element, therefore, the time portion of the DateTime element will be defaulted to 00:00:00+00:00.

Standing orders will only return `FirstPaymentAmount` which will be the same amount for the duration of the standing order.

### Scheduled Payments

**[Scheduled Payments API](Scheduled%20Payments.md)**

DateTime elements have been used so that there is consistency across all API endpoints using dates. However, for Standing Orders we only process based on the day element, therefore, the time portion of the DateTime element will be defaulted to 00:00:00+00:00.

### Parties

**[Parties API](Parties.md)**

### Statements

**[Statements API](Statements.md)**

## Endpoints

The API endpoints for these resources are given below.

They can be accessed from the following baseUrl: `https://rs1.tecban-sandbox.o3bank.co.uk:4501/v1.0/open-banking/v3.1/aisp/**`

| Resource |Endpoints |
| --- |--- |
| [account-access-consents](Account%20Access%20Consents.md) |POST /account-access-consents |
| [account-access-consents](Account%20Access%20Consents.md) |GET /account-access-consents/{ConsentId} |
| [account-access-consents](Account%20Access%20Consents.md) |DELETE /account-access-consents/{ConsentId} |
| [accounts](Accounts.md) |GET /accounts |
| [accounts](Accounts.md) |GET /accounts/{AccountId} |
| [balances](Balances.md) |GET /accounts/{AccountId}/balances |
| [balances](Balances.md) |GET /balances |
| [transactions](Transactions.md) |GET /accounts/{AccountId}/transactions |
| [transactions](Transactions.md) |GET /transactions |
| [beneficiaries](Beneficiaries.md) |GET /accounts/{AccountId}/beneficiaries |
| [beneficiaries](Beneficiaries.md) |GET /beneficiaries |
| [products](Products.md) |GET /accounts/{AccountId}/product |
| [products](Products.md) |GET /products |
| [direct-debits](Direct%20Debits.md) |GET /accounts/{AccountId}/direct-debits |
| [standing-orders](Standing%20Orders.md) |GET /accounts/{AccountId}/standing-orders |
| [scheduled-payments](Scheduled%20Payments.md) |GET /accounts/{AccountId}/scheduled-payments |
| [parties](Parties.md) |GET /accounts/{AccountId}/parties |
| [parties](Parties.md) |GET /accounts/{AccountId}/party |
| [parties](Parties.md) |GET /party |
| [statements](Statements.md) |GET /accounts/{AccountId}/statements |
| [statements](Statements.md) |GET /accounts/{AccountId}/statements/{StatementId}/file |