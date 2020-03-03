# ReactivePay Flexy Commission - On-fly tuning service for payment commissions

This service works using flexy-guard rule filtering enging where instead
of setting up the rules, you post commissions using the following JSON
format:

``` none
{
    "header": {
        "type": "PayinRequest"
    },
    "body": {
        "self": {
            "rate": "0.5",
            "fee": "1"
        },
        "provider": {
            "rate": "0.4",
            "fee": "0.3"
        }
    }
}
```

Where header section identifies payment request params to fetch
commission schedule for and body contains of "self" (commssion charged
by the system) and "provider" (commission charged by payment provider)
sections These sections contain commission schedule defined by the
following keywords:

**rate** - rate is % based commission fee (like: 0.5%, 0.6%)

**fee** - tand fee is fixed price commission fee (like: 0.1 USD, 0.4
USD)

Please note that no currecny or percentage symbol should be posted along
with a float number

To perform initial service setup please follow the steps:

1.  Post definition section (defines payment parameters to fetch
    commission sch. for)

![image](https://reactivepay-docs.readthedocs.io/en/latest/_images/fl_d.png)

``` none
[
{
    "param": {
    "name": "to_profile",
    "param": {
        "name": "source",
        "param": {
        "name": "type"
        }
    }
    }
},
{
    "param": {
    "name": "type"
    }
},
{
    "param": {
    "name": "to_profile",
    "param": {
        "name": "source",
        "param": {
        "name": "type",
        "param": {
            "name": "country_bank"
        }
        }
    }
    }
}
]
```

2.  Post basic commission schedule

![image](https://reactivepay-docs.readthedocs.io/en/latest/_images/fl_c.png)

``` none
{
"header": {
    "type": "PayinRequest"
},
"body": {
    "self": {
    "rate": "0.5",
    "fee": "1"
    },
    "provider": {
    "rate": "0.4",
    "fee": "0.3"
    }
}
}
```

More commission schedule examples are below:

  - commission schedule depends on profile, payment source (channel,
    type, country of issuer institution)

<!-- end list -->

``` none
{
"header": {
    "to_profile": "3",
    "source": "default",
    "type": "PayinRequest",
    "country_bank": "RU"
},
"body": {
    "self": {
    "rate": "2.2",
    "fee": "10"
    },
    "provider": {
    "rate": "1.1",
    "fee": "5"
    }
}
}
```

  - commission schedule depends on profile, payment source (channel,
    type)

<!-- end list -->

``` none
{
"header": {
    "to_profile": "3",
    "source": "default",
    "type": "PayinRequest"
},
"body": {
    "self": {
    "rate": "2.2",
    "fee": "10"
    },
    "provider": {
    "rate": "1.1",
    "fee": "5"
    }
}
}
```
