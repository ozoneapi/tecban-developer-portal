# TecBan Open Banking API

Welcome to the TecBan Open Banking API Developer Portal.


## Table of Contents

  - [Open Banking](#markdown-header-open-banking)
  - [API Docs](#markdown-header-api-docs)
  - [API Helpers](#markdown-header-api-helpers)
  - [Sandbox API](#markdown-header-sandbox-api)
  - [Production API](#markdown-header-production-api)
  - [Support](#markdown-header-support)
  - [Changelog](#markdown-header-changelog)

## Open Banking

The TecBan Open Banking API is based on the Open Banking Standard which allows regulated Third Party Providers (TPPs) to access Account Information Services (AIS), Payment Initiation Services (PIS) and funds confirmation requests for member accounts.  Access to these services on behalf of members is controlled by strong customer authentication within TecBan apps as part of OpenID Connect authorisation flows. 

__Correct? We currently support app->app, mobile-web->app, web->web authentication flows__.

TecBan is an FCA registered Account Servicing Payment Service Provider (ASPSP) who provides access to these services via the Open Banking standard.  You can find out more about Open Banking here: [What is Open Banking](https://www.openbanking.org.uk/customers/what-is-open-banking/).


## API Docs

Please see the following specifications we have aligned with:

  - [Dynamic Client Registration (DCR) Specification](https://openbanking.atlassian.net/wiki/spaces/DZ/pages/1078034771/Dynamic+Client+Registration+-+v3.2)
    - Use this specification to register your TPP client to use our APIs
  - [Open ID Foundation's Financial Grade API (FAPI) Profile](https://openid.net/specs/openid-financial-api-part-2-wd-06.html)
    - This specification enables user authentication of consents for open banking
  - [TecBan Open Banking API Specification](./specification/README.md) - based on Open Banking Read/Write API Specification v3.1.2
    - This specification describes the resources that are available on our service
    - [Account Information Services API](./specification/resources%20and%20data%20models/aisp/README.md)
        -  https://rs1.tecban-sandbox.o3bank.co.uk:4501/v1.0/open-banking/v3.1/aisp/**
    - [Confirmation of Funds API](./specification/resources%20and%20data%20models/cbpii/README.md)
        -  https://rs1.tecban-sandbox.o3bank.co.uk:4501/v1.0/open-banking/v3.1/cbpii/**
    - [Payment initiation services API](./specification/resources%20and%20data%20models/pisp/README.md)
        -  https://rs1.tecban-sandbox.o3bank.co.uk:4501/v1.0/open-banking/v3.1/pisp/**s

## API Helpers

### Dynamic Client Registration

Our API allows dynamic client registration in order to create a valid client that is able to use our Authorisation Server.  We *only* trust Software Statement Assertions (SSAs) issued by the Open Banking Directory provided by OBIE.  `eIDAS` certificates are supported via onboarding to the Open Banking Directory (as discussed in more detail below).

  - The url of the registration endpoint is advertised on our OIDC Discovery Endpoints (see below) using the `registration_endpoint` claim.
  - The `aud` claim used in the outer JWT of a Dynamic Client Registration request is the OBIE issued `org_id` (as documented in the OBIE DCR v3.1 standard)

### Production security profile

As defined further in the [TecBan Open Banking API Specification](./specification/README.md) 

  - ID Token Signing Algorithm: `PS256`
  - Response Types: `code`, `id_token`
  - Request Object Signing Algorithms: `PS256`
  - Token Endpoint Auth Singing Algorithms: `PS256`
  - Token Endpoint Auth Methods: `private_key_jwt`, `tls_client_auth`
  - For `private_key_jwt` - the `aud` claim is the url of the token endpoint as specified in [OIDC client authentication](https://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication)
  - The `request` object used in [OIDC flows](https://openid.net/specs/openid-connect-core-1_0.html#RequestObject) the `aud` claim is the issuer url from the TecBan ASPSP .wellknown endpoint (linked below).

  > **Note**: Our Sandbox API also offers less strict profiles to assist with integraiton testing.  See below for more details.

### Certificate Support

  - `OB Transport` & `OB Signing` (Open Banking Certificates) - Full support via OBIE Directory
      - `OBWAC` & `OBSEAL` - Support *not* yet enabled
  - `QWAC` & `QSEAL` (eIDAS Certificates) - Direct support *not* yet enabled.  These certificates can be used to onboard to OBIE Directory, then connecting to our service with OBIE issued `OB Transport` & `OB Signing` certs

## Sandbox API

Our API Sandbox contains a full simulation of our APIs but without connecting to any real customer accounts. Any developer can access this Sandbox using their own self signed certificates.

### Try our API in the Sandbox

Below are the paths of our well-known endpoints for the Sandbox environments.

  - Authorisation Server 1: Provides both strict and permissive client profiles in headless and non headless options.
    - OIDC Well Known endpoint: https://ob-issuer1.tecban-sandbox.o3bank.co.uk/.well-known/openid-configuration 
    - `baseUrl`: https://ob-api1.tecban-sandbox.o3bank.co.uk:4501/v1.0 
    
    ##### Authorisation Server 1: Security Profiles
    
    | Profile Name | idTokenSigningAlgs | tokenEndPointAuthenticationMethods | Response Types | requestObjectSigningAlgs | tokenEndPointAuthSigningAlgs | autoLogin |
    | --- | --- | --- | --- | --- | --- | --- |
    | TechBan Sandbox 1 - Strict, UI |PS256 |private_key_jwt tls_client_auth|code id_token |PS256 |PS256 |false |
    | TechBan Sandbox 1 - Strict, Headless |PS256 |private_key_jwt tls_client_auth|code id_token |PS256 |PS256 |true |
    | TechBan Sandbox 1 - Permissive, Headless |PS256 |client_secret_basic client_secret_jwt private_key_jwt tls_client_auth |code code id_token |none HS256 RS256 PS256 |none HS256 RS256 PS256 | true |
    | TechBan Sandbox 1 - Permissive, UI |PS256 |client_secret_basic client_secret_jwt private_key_jwt tls_client_auth |code code id_token |none HS256 RS256 PS256 |none HS256 RS256 PS256 |false |

  - Authorisation Server 2: Provides a more permissive security profile is used to help TPP onboarding and learning
    - OIDC Well Known endpoint: https://ob-issuer2.tecban-sandbox.o3bank.co.uk/.well-known/openid-configuration 
    - `baseUrl`: https://ob-api2.tecban-sandbox.o3bank.co.uk:4502/v1.0 

    ##### Authorisation Server 2 Security Profiles

    | Profile Name | idTokenSigningAlgs | tokenEndPointAuthenticationMethods | Response Types | requestObjectSigningAlgs | tokenEndPointAuthSigningAlgs | autoLogin |
    | --- | --- | --- | --- | --- | --- | --- |
    |TechBan 2 - Standard | |client_secret_basic|code id_token |PS256 |PS256 |false |
    |TechBan 2 - Headless | |client_secret_basic|code id_token |PS256 |PS256 |true |


### Sandbox Testing Info

#### Sandbox User Accounts

| user   | password |
| -------|----------|
| rora   | rora     |
| mits   | mits     |
| ivsa   | ivsa     |

## Production API

Our Production API can be accessed by any authorised TPP who has enrolled on the OBIE Directory and has production Open Banking certificates.

Below are the paths of our well-known endpoints for the production environment.

  - Authorisation Server: Our production authorisation server uses the strict profile defined above and testable in the Sandbox.
    - OIDC Well Known endpoint: https://issuer1.tecban-sandbox.o3bank.co.uk/.well-known/openid-configuration 
    - `baseUrl`: https://rs1.tecban-sandbox.o3bank.co.uk:4501/v1.0 
    - Security profile is as defined above

## Support

If you have any questions or issues, please raise an issue via the following channel: openbanking.support@tecban.com.br 

## Changelog
| Version/Tag | Date       | Changes                                                         |
| ------------|------------|-----------------------------------------------------------------|
| v1.0.0      | 2019-09-25 | AIS: Accounts & Balances release                                |
| v1.0.1      | 2019-10-21 | Added additional TPP onboarding info                            |
| v1.0.2      | 2019-10-31 | Production Information                                          |
| v1.0.3      | 2019-11-11 | AIS: Transactions, Beneficiaries, Products added                |
| v1.0.4      | 2019-12-17 | AIS: Standing Orders, Scheduled Payments, Direct Debits.  CBPII |
| v1.0.5      | 2020-01-14 | Updated supported certificates                                  |
| v1.0.6      | 2020-03-13 | Added PISP, AIS: statements and parties                         |