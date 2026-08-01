---
updatedAt: 2026-05-21T06:19:10.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Introduction - GoPay ID

This document details what is and how to integrate the GoPay ID

# What is GoPay ID?

GoPay ID allows you to let your users verify their identity using their GoPay account.

| Function          | Details                                                                                |
| :---------------- | :------------------------------------------------------------------------------------- |
| Login with GoPay  | A flow where users authenticate using their GoPay account.                             |
| Verify with Gopay | A flow where users verify their identity (KYC/KTP) using their verified GoPay account. |

# What are Benefits of using GoPay ID?

## Benefit for you

GoPay ID enables you to offer secure Login and KYC by leveraging GoPay’s authentication, face verification, and risk prevention systems—eliminating the need to build and operate your own infrastructure.

## Benefit for users

| Login with GoPay                                                                   | Verify with GoPay                                                                        |
| :--------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------- |
| Seamless and secure login using GoPay authentication (OTP, PIN, Face Verification) | Faster and more secure identity verification (KYC) using GoPay account and technologies. |

# High Level Flow

## Happy Flow

![](https://files.readme.io/6309d7de3ee51e1d9a9d45a7ec3db3f54355741161d034104ad827842bc7188e-image.png)

Detailed Sequence Diagram<Anchor label=" is here" target="_blank" href="https://sequencediagram.org/index.html#initialData=C4S2BsFMAIDVIE4gGYE9oHcwAtoHEB7ABwEN0BJAEWmxAHNcoA3ScaZcAjaAExBLoISAWwBQo0glABjEKQB2waACIAqgGdEy6CXXQArpoQSSUkLIVLlABVPB5iaACES0gNaR5PaAGVETc0htXWhrJwBREzMLEkUVWykHBGgAMXDgvWs0qJk5WKtCUnQfSgBpDPwAYRLSnPM8uOVCsmdXDy8KvCdxUUNEAFoAPjDwgC5yRU8ePWACXjnSgE1K0RGhrLHfbC58YjIqaAAjfWBZ+VF5AmAYAhZkjdGtnfgkNEwcXaLoA+JQAnloLMDEYLlcbndQmlHhpHJooNJgHoXih0FhgLhmhRqL8QP9VmkhnhqmVRgAZEj6eTSXDIt5ojF7VAHYSQdEEbwEZC+MoAHXk9OgCEgAEd9JB1EoQDwADTAxzSAgIIXgEh-AFS0SQAAeCh4JEOUEASETfLl9ZIgPSXJScOh0SDeEAAgIkT4tKiiaDQK3gxxEmqPayIZCK4TQGHJO4ocyq3HyPmxbx2pKqmAAQROuEq7MgHuguY2AB5+n6Sen0dAFTwfclpCRwOBDm1AXMiELgwhQ+BHW5HXQ+QKhaLxZLvAm5TXFcqY-9oBrPSMiw9Awh253u738xFCU5RknECnoF35D35HRm+1N+Ei11RkeT2fZhfPd7oLdHCNHhLFTA773z55L3WKF1H0aRpHFPQhXUIh-k0fMCUGEtSlGWt60bdwdHcS4MCgHg7RZOJ6T5QcxQlWdRy8ccK0nVhp3VHhNS8cRtV1fUoH6aAlkqUIEAIcD1HUXMXzfZIkOhGCASFcCQACU9AWwGBUIbJt4ywrhcPwzwlAlOw9D5dEYC46BWz4iCN2fMFXwhMToEqEgiGAfQoLDIxZ2EARxVzJDt1GEDDmEMAqJAdy7UEizris30dx0dRUCpbBeMuQxOOWYzeP49RzMhK9i2JZClPQtx2EVFLuL8gKBNjajhCIKA1X7D4SOHcidEos1qKVWi1XIoTLJE0IIkeDASEC9sKzrZSMOQXjhD5TF3nLIyq2AEbwDCgacpvIzyotTKZ2W1a9AKtpVi3YYoR8bZuCMhUarqqqgTNRiGOYnUEzYyAOIAeQBKt3MovUVvYVlqXYTgMFO8IfLwVloB2yr9tZQ7X1+yB-p4Bry1-OTHwAhdix3JakZANbntEIA"> is here</Anchor>.

## Detailed Flow Diagram

![](https://files.readme.io/1d25cd217f96fe78e1ae5077f759b6e2d2d0f4ddc9820b5a0a3fb97c9b54ddf7-image.png)

Detailed Sequence Diagram<Anchor label="is here" target="_blank" href="https://sequencediagram.org/index.html#initialData=C4S2BsFMAIDVIE4gGYE9oHcwAtoHEB7ABwEN0BJAEWmxAHNcoA3ScaZcAjaAExBLoISAW0w5oAYwIIAdokkkAzpEUAoVaQSgJIUjODQARAFVlCQ9CXQArmY0ktIHXoOGACg+ByE0AEIkJAGtIGR5oAGVEJidICys3XwBRe0dnEn0jDy1vaAAxRLjFaDd8lO1ddNdCUnRwygBpQvwAYTr6sqcKjMNqsj8A4NCmvF91VVtEAFoAPgTEgC5yfRCeIuACXg36gE1m9UgADz0eEgAjKEAkIhp0nihoBEgiSBJgSDCJhCKJJRVVEnADB9oOAQDJAqC6NB1oNLOAHiQeOhDiBFMA1NBikkZiN5tA6JADDtmtBFNZTsIUYoQAQZLwCSQQOB0bCDORkNAibD4YjJARhEQoK9LKE4ABBAAyVFUGIxMgIQoILB8c1xphgwGwME5PHpjKKD2A1lkb2FYTlAB0ZHITetgSRrDIJLgNTBeqgqOxONwBAyZJbpdBWMoObtoHKDFJ+YKYNJoEsmP8QDwAxi5tjfPN8QZXvyoQRBinMYkADyTHE5ojSBzoaEhQvhmNKou48X2x3OzVwRAodBYDX4Yh9D197CWit5mG2xTgojA0HgmSQjhcAMrVRrteprGzfK48LYLgDmoe07WYDrWkjy0PACO1hUBiTABobGZeQgHuAXtTaUnLTcoUgXNaxkVQG2gRV5BKBYIgPbh4CQNAxH7N042oYhQBpPNX0QMD5UbKDd2gNUfGUKAJDRLtEN7cRUI9DCf1UaDsVaBp5lbB0nSontkNwN0PWEAkDzCAh2TaS0R3uSA7wfaBnxwnwpA-VhvywpNTTHIDZxAsZDmOM5LmIt9xQIOhQVXI4bgMyBJmuUI7geJ4XhND4vh+ZkMX+R92XHEC8RAFhC1lfCIKbPBWPqPcZznMEIVNaAiAQAgJEgN4xy2UNEuSlQqUXQs10LLy5PZIF-m5dBODofEwnMmUZSK+1+ykHVLCCOUMCgHhqqCmVwMgnxwraKLdBihdIQArKUrS-QMuJSacohHqgxgRrcGamBw1awJ2s67q6rqvqwoi4bZ0q0F4oNI0-RkVbeRa75wHAU4BiW0J8rejFNzDEL+paIbikQZBpFEEjgVM86APxbxnOgUUz1wZoCBa6AA2g0tBrYuGmqRgjFP+J6BmwxLICBhBRBBWK8q3EtJmg+Y3EB4HRsW6n00zEJEBhimxonOtqfRjNubinTgoVJsVRJdYHmZxdedA1mdwWUkJBSxR9RUSsZGUVH8hYoaHoJoItp2t58UEjIrxkW971ROSwgAoElM-VTf2TAq9Ks84bJDYk3CS1XmUO+QMci4jNaklKAuFzsDeeo3-zarhdqAkIDFRTwijHTtOXmtWWe+sXg+O6BmhIIhDQeIpQZAYQBF+DEQ7Z0lyTABS5Nr-FA5+sKM0sRRUHbJK5VsH2Ev9haqeKfJ0eO2PCdJ0fm4pPOsMjAUCR-CTxGt2T1Idt8nZUzDXYDIPlSSXEMAZAwF7no3kCS0RUMk7VdSZVGkgF+ZOSXykfzpYADImQKEenHQITFtx033IeTka9BT-1tB8dcb19iWVCNZWyAB5WkOpa4ihOIA9gBIuLLgwBAxIbM8AEhJGSZeVIsI6kAXqCCOCgI3C3v2IWssdJzC-q-Jh781xAA">is here</Anchor>