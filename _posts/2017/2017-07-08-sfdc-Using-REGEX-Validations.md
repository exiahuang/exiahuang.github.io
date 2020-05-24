---
categories:
- Salesforce
date: 2017-07-08 08:15:34
description: Salesforce Using REGEX in Validations
layout: post
tags:
- SFDC
- Salesforce
- Apex
title: Salesforce Using REGEX in Validations
update_date: 2020/05/23 23:56:53

---

# Using REGEX in Validations
## Example 1 : Validate Credit Card Number
Description :
Validates that a custom text field called Credit_Card_Number is formatted in 9999-9999-9999-9999 or 9999999999999999 number format when it is not blank.The pattern specifies:
• Four digits (0-9) followed by a dash: \\d{4}-
• The aforementioned pattern is repeated three times by wrapping it in () {3}
• Four digits (0-9)
• The OR character (|) allows an alternative pattern of 16 digits of zero through nine with no dashes: \\d{16}


Validation Formula :
```
NOT( REGEX( Credit_Card_Number__c ,
"(((\\d{4}-){3}\\d{4})|\\d{16})?"))
```
Error Message : Credit Card Number must be in this format: 9999-9999-9999-9999 or 9999999999999999.


## Example 2 : Valid IP Address
Description :
Ensures that a custom field called IP Address is in the correct format, four 3-digit numbers (0-255) separated  by periods.

Validation Formula :
```
NOT(
REGEX( IP_Address__c,
"^((25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\.){3}(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$"
))
```
Error Message : IP Address must be in form 999.999.999.999 where each part is between 0 and 255.


## Example 3 : US Phone Number Has Ten Digits
Description :
Validates that the Phone number is in (999) 999-9999 format. This works by using the

REGEX function to check that the number has ten digits in the (999) 999-9999 format.


Validation Formula : 
```
NOT(REGEX(Phone, "\\D*?(\\d\\D*?){10}"))
```
Error Message : US phone numbers should be in this format: (999) 999-9999.


## Example 4 : Social Security Number Format
Description :
Validates that a custom text field called SSN is formatted in 999-99-9999 number format

(if it is not blank). The pattern specifies:
• Three single digits (0-9):\\d{3}
• A dash
• Two single digits (0-9):\\d{2}
• A dash
• Four single digits (0-9):\\d{4}


Validation Formula :
```
NOT(
OR(
LEN (Social_Security_Number__c) = 0,
REGEX( Social_Security_Number__c , "[0-9]{3}-[0-9]{2}-[0-9]{4}")
))
```
Error Message : SSN must be in this format: 999-99-9999.


This will provide am idea how we can write validations using REGEX.