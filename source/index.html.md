---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - python
  - shell


toc_footers:

includes:
  - errors

search: true
---

# Introduction

Welcome to our internal API documentation. This documentation is intended for both business and developer users to understand what API functionality we support and how to use it.

Currently, we have documented two API groups:

1. Events API - which interacts with Usercities
2. Data services API - which interacts with our Data warehouse

# Events API

The Events API requires no authentication. It provides a single entry point that captures events from various stages of the user journey. Here is a summary of the functionality that it currently provides:

* Salesforce email generation
* Dialer lead generation
* Storage of leads, application journeys in Suite CRM
* Some custom functions for specific countries/verticals

## Dialer Lead Generation

> Example of calling the Events API to generate a Lead in TMG

```python

import httplib2

headers = {
  'Content-type': 'application/json',
  'Usercity-Auth-Token': 'c1550bd0-e187-4bce-9044-846eb89cad8f'
  }

payload = {
  "phone": "995551234",
  "email": "steve.walsh@compareglobalgroup.com",  
  "vertical": "car_insurance",
  "locale": "HK",  
  "language": "ES",
  "attributes": {
    "usercityEventName": "postFromFunnel",
  },
  "source_url": "http://moneyhero.hk"
}
events_url = "http://moneyhero.hk/api/events/submit"

http = httplib2.Http()
http.request(events_url, 'POST', body = payload, headers = headers)

```

In terms of dialers, currently, we support TMG only. The dialer lead generation functionality requires an initial event message that contains the required query parameters listed below. Subsequent events can be sent with additional required fields listed below. The dialer lead generation logic uses an email address to merge all of these events together and allow for 15 minutes of inactivity before sending the lead to the dialer.

### Required Query Parameters for Initial Event

Parameter | Description
--------- | -----------
phone | The dialer cannot function without a phone number
email | Usercity uses the email address field to determine unique users and merge all events associated with a user journey (within last 15 minutes together)
vertical | Used to identify segmentation config
locale | Used to identify segmentation config
language | Required but not Used
attributes/usercityEventName | The first event with the listed required parameters must have the usercityEventName set to 'postFromFunnel' in order to generate a TMG lead. Subsequent events can have a different type
source_url | Used to indicate where the user dropped off on their user journey

### Required Query Parameters for Subsequent Events

Parameter | Description
--------- | -----------
phone | The dialer cannot function without a phone number
email | Usercity uses the email address field to determine unique users and merge all events associated with a user journey (within last 15 minutes together)
vertical | Used to identify segmentation config
locale | Used to identify segmentation config
language | Required but not Used
attributes/usercityEventName | The first event with the listed required parameters must have the usercityEventName set to 'postFromFunnel' in order to generate a TMG lead. Subsequent events can have a different type
source_url | Used to indicate where the user dropped off on their user journey


## Salesforce Marketing Cloud (Email)

### Send Policy Documents to Customer


> To call lambda directly:

```python

import lambda_service



lambda_service.execute("{"ULR":}")


```

```java



```

> To call from API Gateway:

```python

import lambda_service



lambda_service.execute("{"ULR":}")


```

```java



```

To trigger a policy document email, the following internal API must be used:






## Suite CRM

## Custom functions

### Payment Guard - Hong Kong Travel Insurance

### Email Completed Applications to Provider - Hong Kong Personal Loan

### Application Forms submitted to MULE for Provider - Singapore


# Data Services API
