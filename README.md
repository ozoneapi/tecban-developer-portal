![Tecban](/images/logo.png)

# TecBan open banking API

Welcome to the TecBan open banking API developer portal.


## Table of contents

  - [Introduction](#introduction)
  - [API specifications](#api-specifications)
  - [Sandbox](#sandbox)
  - [Support](#support)


## Introduction

This initial version of the TecBan open banking API is based on the [UK open banking standard](https://standards.openbanking.org.uk/) which allows Third Party Providers (TPPs) to access Account Information Services (AIS), Payment Initiation Services (PIS) and funds confirmation requests for Payment Service User (PSU) accounts held at an Account Servicing Payment Service Provider (ASPSP) or bank. 

Access to these services on behalf of PSUs is controlled by Strong Customer Authentication (SCA) within the ASPSP's web or mobile app as part of OpenID Connect authorisation flows. This API currently support app->app, mobile-web->app, web->web authentication flows.


## API specifications

Please see the following specifications which are supported:

  - [Open ID Foundation's Financial Grade API (FAPI) Profile](https://openid.net/specs/openid-financial-api-part-2-wd-06.html)
    - This specification enables user authentication of consents for open banking
  - [TecBan open banking API specification](https://openbankinguk.github.io/read-write-api-site3/) - based on the UK open banking read/write API specification v3.1
    - This specification describes the resources that are available in our APIs
    
    
## Sandbox

Our API Sandbox contains a full simulation of the TecBan API but without connecting to any real customer accounts. Below are the paths of our well-known endpoints for the Sandbox environments:

  - Authorisation Server 1: Provides both strict and permissive client profiles in headless and non headless options.
    - OIDC Well Known endpoint: https://ob-issuer1.tecban-sandbox.o3bank.co.uk/.well-known/openid-configuration
    - `baseUrl`: https://ob-api1.tecban-sandbox.o3bank.co.uk:4501/v1.0
  - Authorisation Server 2: Provides a more permissive security profile is used to help TPP onboarding and learning
    - OIDC Well Known endpoint: https://ob-issuer2.tecban-sandbox.o3bank.co.uk/.well-known/openid-configuration
    - `baseUrl`: https://ob-api2.tecban-sandbox.o3bank.co.uk:4502/v1.0

### Certificate support

The TecBan API requires both 'Transport' and 'Signing' Certificates. For the Sandbox API, please contact TecBan (see below).

### Postman collection

The best way to test out our API is to use our [Postman collections](TBC).

Please see our [Step-by-step guide to using Postman](TBC). 

### Sandbox user accounts for testing

| user   | password |
| -------|----------|
| rora   | rora     |
| mits   | mits     |
| ivsa   | ivsa     |

### Swagger
You can download swagger specifications for the TecBan open banking API from [here](https://github.com/OpenBankingUK/read-write-api-specs/tree/v3.1.5).

## Support

If you have any questions or issues, please raise an issue via the following channel: [openbanking.support@tecban.com.br](mailto:openbanking.support@tecban.com.br)


Powered by:

![Ozone API](/images/logo.png)