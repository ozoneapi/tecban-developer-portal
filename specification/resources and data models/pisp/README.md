# PISP Resources and Data Models - v3.1.2

Resources accessed using the pisp PSD2 role are detailed here:

  -  [Domestic Payment Consents](domestic-payment-consents.md)
  -  [Domestic Payments](domestic-payments.md)
  -  [Domestic Scheduled Payment Consents](domestic-scheduled-payment-consents.md)
  -  [Domestic Scheduled Payments](domestic-scheduled-payments.md)
  -  [Domestic Standing Order Consents](domestic-standing-order-consents.md)
  -  [Domestic Standing Orders](domestic-standing-orders.md)

### Domestic Payment Consents 

**[Domestic Payment Consents API](domestic-payment-consents.md)**

  - There is no MAX ‘InstructedAmount/Amount' mandated by TecBan API. 50,000 R$ is the default maximum when opening a
 TecBan account, but thresholds can be managed by the customer. TecBan suggest PISP notify the PSU that the same limits
  apply as in their TecBan app. It is possible from time to time that `domestic-payment-consents` is authorised but
   payment initiation fails due to account limits.  
  - InstructedAmount/Currency must be R$   
  - RemittanceInformation/Reference is mandatory field and must adhere to the following: 
      - Valid characters - "A-Z", "0-9", "space", "&", "-", ".", "/" 
      - Contiguous characters – user enters 6 or more valid characters but without contiguous string of at least  
  6 alphanumeric characters - Must contain a contiguous string of at least 6 alphanumeric characters 
      - Homogeneous string – user enters 6 or more valid characters (including valid non-alphanumeric characters) - 
  After stripping out non-alphanumeric characters the resulting string cannot consist of all the same character

*PISP may also opt to populate reference field on behalf of the PSU


  - `Domestic-payment-consents` will only be authorised if the `CreditorAccount` details are that of an
 already existing `beneficiary` i.e. one the PSU has previously created in their app. if a 
 consent contains recipient info that does not meet this criteria then error will be returned to
  the front end, the consent will remain in status `awaiting authorisation` and the PSU will not be redirected.
  -  The PISP can approach this in one of two ways: 
      - Notify PSU that only payments to existing recipients 
   are permitted and in the event this condition is not met TecBan will not authorise the consent and 
   display error modal to user  
      - Integrate with TecBan beneficiaries API and can confirm that the recipient
    already exists before sending the consent to allow for a better user experience
  -  Only local instrument 
     supported is faster payment scheme UK.OBIE.FPS, if anything other than this is sent by PISP in consent
      payload then an error will be returned. However, this field is not mandatory so we suggest PISP simply 
      not include this field and TecBan will stage consent as a faster payment.
  -  Only support Account/SchemeName UK.OBIE.SortCodeAccountNumber for both `DebtorAccount` and `CreditorAccount`, any other enum provided will return error. 
  -  Payments can be made on all days including Saturdays, Sundays and Bank Holidays 

### Domestic Payments 

**[Domestic Payments API](domestic-payments.md)**


### Domestic Scheduled Payment Consents

**[Domestic Scheduled Payment Consents API](domestic-scheduled-payment-consents.md)**

  -  There is no MAX ‘InstructedAmount/Amount' mandated by TecBan API. 50,000 R$ is the default maximum when opening a
 TecBan account, but thresholds can be managed by the customer. TecBan suggest PISP notify the PSU that the same limits
  apply as in their TecBan app. It is possible from time to time that `domestic-payment-consents` is authorised but
   payment initiation fails due to account limits. 
  -  InstructedAmount/Currency must be R$ 
  -  RemittanceInformation/Reference is mandatory field and must adhere to the following: 
      - Valid characters - "A-Z", "0-9", "space", "&", "-", ".", "/" 
      - Contiguous characters – user enters 6 or more valid characters but without contiguous string of at least 
  6 alphanumeric characters - Must contain a contiguous string of at least 6 alphanumeric characters 
      - Homogeneous string – user enters 6 or more valid characters (including valid non-alphanumeric characters) - 
  After stripping out non-alphanumeric characters the resulting string cannot consist of all the same character 


*PISP may also opt to populate reference field on behalf of the PSU


  -  `Domestic-scheduled-payment-consents` will only be authorised if the `CreditorAccount` details are that of an
 already existing `beneficiary` i.e. one the PSU has previously created in their app. if a 
 consent contains recipient info that does not meet this criteria then error will be returned to
  the front end, the consent will remain in status `awaiting authorisation` and the PSU will not be redirected. 
  - The PISP can approach this in one of two ways:  
      - Notify PSU that only payments to existing recipients  
   are permitted and in the event this condition is not met TecBan will not authorise the consent and 
   display error modal to user  
      - Integrate with TecBan beneficiaries API and can confirm that the recipient 
    already exists before sending the consent to allow for a better user experience 
   -  Only local instrument 
     supported is faster payment scheme UK.OBIE.FPS, if anything other than this is sent by PISP in consent
      payload then an error will be returned. However, this field is not mandatory so we suggest PISP simply 
      not include this field and TecBan will stage consent as a faster payment. TODO  
   -  Only support Account/SchemeName UK.OBIE.SortCodeAccountNumber for both `DebtorAccount` and `CreditorAccount`, any other enum provided will return error. 
   -  `RequestedExecutionDateTime` must be no more than 1 calendar year in advance, falling short of this PISP will be returned an error 
   -  Payments can be made on all days including Saturdays, Sundays and Bank Holidays 

### Domestic Scheduled Payments

**[Domestic Scheduled Payments API](domestic-scheduled-payments.md)**


### Domestic Standing Order Consents

**[Domestic Standing Order Consents API](domestic-standing-order-consents.md)**

  -  There is no MAX ‘FirstPaymentAmount/Amount' mandated by TecBan API. 50,000 R$ is the 
default maximum when opening a TecBan account, but thresholds can be managed by the 
customer. TecBan suggest PISP notify the PSU that the same limits apply as in their TecBan app. It 
is possible from time to time that `domestic-payment-consents` is authorised but payment 
initiation fails due to account limits. 
  -  FirstPaymentAmount/Currency must be R$ 
  -  Initiation/Reference is mandatory field and must adhere to the following rules: 
      - Valid characters - "A-Z", "0-9", "space", "&", "-", ".", "/" 
      - Contiguous characters – user enters 6 or more valid characters but without contiguous string  
  of at least 6 alphanumeric characters - Must contain a contiguous string of at least 6 alphanumeric characters 
      - Homogeneous string – user enters 6 or more valid characters (including valid non-alphanumeric characters) - 
  After stripping out non-alphanumeric characters the resulting string cannot consist of all the same character 


*PISP may also opt to populate reference field on behalf of the PSU


  -  `Domestic-standing-order-consents` will only be authorised if the `CreditorAccount` details are that of an already 
existing `beneficiary` i.e. one the PSU has previously created in their app. if a consent contains recipient info that 
does not meet this criteria then error will be returned to the front end, the consent will remain in status 
`awaiting authorisation` and the PSU will not be redirected. 
  - The PISP can approach this in one of two ways: 
      - Notify PSU that only payments to exisitng recipients are permitted and in the event this condition
     is not met TecBan will not authorise the consent and display error modal to user  
      - Integrate with TecBan beneficiaries API and can confirm that the recipient already exists before 
    sending the consent to allow for a better user experience 
   -  Only support SchemeName UK.OBIE.SortCodeAccountNumber for both `DebtorAccount` and `CreditorAccount`, 
  any other enum provided will return error.
   - ` Initiation/FirstPaymentDateTime` must be no more than 1 calendar year in advance, or  PISP will be returned an error
   - `Initiation/FinalPaymentDateTime` must be after ` Initiation/FirstPaymentDateTime` by at least a calendar day,
   or PISP will be returned error
   - ‘Initiation/Frequency’ supported by TecBan are IntrvlMnthDay:01:xx andIntrvlWkDay:01:xx,  
  the following rules apply:
      - IntrvlMnthDay:01:xx Same day every month (i.e. if made on 4th May 
  the next payment will be made on the 4th June), however if a payment is made on either the 29th, 
  30th, 31st of the month and one of the months a payment is scheduled to be in has fewer days than the month of the 
  first payment then that payment will be made on the LAST day of that month. (e.g. first payment on 30th Jan > 
  next payment 28th Feb > next payment 30th March. 
          - first two digits after IntrvlMnthDay must be set at '01', indicating a one monthly interval else PISP
   will be returned error 
          - last two digits after IntrvlMnthDay are not considered or validated by TecBan 
    (payment will be made as per the day in FirstPaymentDateTime)
       - IntrvlWkDay:01:xx Same day of the week as the first payment 
   (i.e. if first payment is made on Friday > next payment is made on Friday the following week) -
    this is number of the week i.e. 1 = monday 
          - first two digits after IntrvlMnthWkDay must be set at '01'
          - last two digits after IntrvlMnthWkDay are not taken in to account by TecBan  
    (payment willbe made as per the day in FirstPaymentDateTime)
   -  NumberOfPayments not supported by TecBan (will return error if provided) 
   -  RecurringPaymentDateTime not supported by TecBan (will return error if provided) 
   -  RecurringPaymentAmount not supported by TecBan (will return error if provided) 
   -  FinalPaymentAmount not supported by TecBan (will return error if provided) 

### Domestic Standing Orders

**[Domestic Standing Orders API](domestic-standing-orders.md)**



## Endpoints

The API endpoints for these resources are given below.
They can be accessed from the following baseUrl: {TODO need url} 

| Resource |Endpoints |
| --- |--- |
| [domestic-payment-consents](domestic-payment-consents.md) |POST /domestic-payment-consents |
| [domestic-payment-consents](domestic-payment-consents.md) |GET /domestic-payment-consents/{ConsentId} |
| [domestic-payment-consents](domestic-payment-consents.md) |GET /domestic-payment-consents/{ConsentId}/funds-confirmation |
| [domestic-payments](domestic-payments.md) |POST /domestic-payments |
| [domestic-payments](domestic-payments.md) |GET /domestic-payments/{DomesticPaymentId} |
| [domestic-scheduled-payment-consents](domestic-scheduled-payment-consents.md) |POST /domestic-scheduled-payment-consents |
| [domestic-scheduled-payment-consents](domestic-scheduled-payment-consents.md) |GET /domestic-scheduled-payment-consents/{ConsentId} |
| [domestic-scheduled-payments](domestic-scheduled-payments.md) |POST /domestic-scheduled-payments |
| [domestic-scheduled-payments](domestic-scheduled-payments.md) |GET /domestic-scheduled-payments/{DomesticScheduledPaymentId} ] |
| [domestic-standing-order-consents](domestic-standing-order-consents.md) |POST /domestic-standing-order-consents |
| [domestic-standing-order-consents](domestic-standing-order-consents.md) |GET /domestic-standing-order-consents/{ConsentId} |
| [domestic-standing-orders](domestic-standing-orders.md) |POST /domestic-standing-orders |
| [domestic-standing-orders](domestic-standing-orders.md) |GET /domestic-standing-orders/{DomesticStandingOrderId} |

### Notes

Definitions for Mandatory, Conditional and Optional are given in the [Read/Write Data API Profile](../../profiles/read-write-data-api-profile.md#categorisation-of-implementation-requirements).

## Payment Initiation Resource Compatibility

|  | |Read-Write API Profile |Read-Write API Profile |Read-Write API Profile |Payment Initiation API Profile |Payment Initiation API Profile |Payment Initiation API Profile |File Payments API Profile |File Payments API Profile |File Payments API Profile |
| --- |--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |
|  | |v3.1 |v3.1.1 |3.1.2 |v3.1 |v3.1.1 |3.1.2 |v3.1 |v3.1.1 |3.1.2 |
| Domestic Payment Consents |v3.1 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE |n/a | | |
|  |v3.1.1 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE | | | |
|  |v3.1.2 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE | | | |
| Domestic Payments |v3.1 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE |n/a | | |
|  |v3.1.1 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE | | | |
|  |v3.1.2 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE | | | |
| Domestic Scheduled Payment Consents |v3.1 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE |n/a | | |
|  |v3.1.1 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE | | | |
|  |v3.1.2 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE | | | |
| Domestic Scheduled Payments |v3.1 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE |n/a | | |
|  |v3.1.1 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE | | | |
|  |v3.1.2 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE | | | |
| Domestic Standing Order Consents |v3.1 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE |n/a | | |
|  |v3.1.1 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE | | | |
|  |v3.1.2 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE | | | |
| Domestic Standing Orders |v3.1 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE |n/a | | |
|  |v3.1.1 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE | | | |
|  |v3.1.2 |TRUE |TRUE |TRUE |TRUE |TRUE |TRUE | | | |
