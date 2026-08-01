---
updatedAt: 2026-04-30T08:52:14.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Initiate Flow

Fetch the user token/launch URL needed to start the identity verification flow on frontend.
Additional details passed in this API will be stored and used during submission processing.


# OpenAPI definition

```json
{
  "openapi": "3.0.3",
  "info": {
    "title": "eSign API - Initiate Flow",
    "description": "Identity verification flow initiation API.",
    "version": "1.0.0",
    "contact": {
      "name": "GTF Team"
    }
  },
  "servers": [
    {
      "url": "https://onekyc.ky.id.staging.gopayapi.com",
      "description": "IAB Gateway - Staging"
    }
  ],
  "tags": [
    {
      "name": "Flow",
      "description": "Identity verification flow APIs"
    }
  ],
  "paths": {
    "/esign-partner/v1/initiate-flow": {
      "servers": [
        {
          "url": "https://onekyc.ky.id.staging.gopayapi.com",
          "description": "IAB Gateway - Staging"
        }
      ],
      "post": {
        "tags": [
          "Flow"
        ],
        "summary": "Initiate Flow",
        "description": "Fetch the user token/launch URL needed to start the identity verification flow on frontend.\nAdditional details passed in this API will be stored and used during submission processing.\n",
        "operationId": "initiateFlow",
        "servers": [
          {
            "url": "https://onekyc.ky.id.staging.gopayapi.com",
            "description": "IAB Gateway - Staging"
          }
        ],
        "parameters": [
          {
            "$ref": "#/components/parameters/OneKycToken"
          },
          {
            "$ref": "#/components/parameters/OnboardingPartner"
          },
          {
            "$ref": "#/components/parameters/PartnerUserId"
          },
          {
            "$ref": "#/components/parameters/PartnerUserIdType"
          },
          {
            "$ref": "#/components/parameters/PartnerSessionId"
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/InitiateFlowRequest"
              },
              "examples": {
                "verifiedPhone": {
                  "summary": "With Verified Phone",
                  "value": {
                    "flow": "STANDALONE_IDENTITY_VERIFICATION",
                    "source": "SDK",
                    "successRedirectionUrl": "http://myserver.com/success-page",
                    "failureRedirectionUrl": "http://myserver.com/failure-page",
                    "additionalDetails": {
                      "phoneNumber": "628188888889",
                      "dataVerification": {
                        "phoneNumber": {
                          "isVerified": true,
                          "verificationReferenceId": "string-referencing-to-phonenumber-verification"
                        }
                      }
                    }
                  }
                },
                "verifiedEmail": {
                  "summary": "With Verified Email",
                  "value": {
                    "flow": "STANDALONE_IDENTITY_VERIFICATION",
                    "source": "SDK",
                    "successRedirectionUrl": "http://myserver.com/success-page",
                    "failureRedirectionUrl": "http://myserver.com/failure-page",
                    "additionalDetails": {
                      "email": "test@xyz.com",
                      "dataVerification": {
                        "email": {
                          "isVerified": true,
                          "verificationReferenceId": "string-referencing-to-email-verification"
                        }
                      }
                    }
                  }
                },
                "web": {
                  "summary": "Web SDK integration",
                  "value": {
                    "flow": "STANDALONE_IDENTITY_VERIFICATION",
                    "source": "WEB_SDK",
                    "successRedirectionUrl": "http://myserver.com/success-page",
                    "failureRedirectionUrl": "http://myserver.com/failure-page",
                    "additionalDetails": {
                      "phoneNumber": "628188888889",
                      "dataVerification": {
                        "phoneNumber": {
                          "isVerified": true,
                          "verificationReferenceId": "string-referencing-to-phonenumber-verification"
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Successfully initiated flow",
            "content": {
              "application/json": {
                "schema": {
                  "oneOf": [
                    {
                      "$ref": "#/components/schemas/InitiateFlowSdkResponse"
                    },
                    {
                      "$ref": "#/components/schemas/InitiateFlowWebSdkResponse"
                    }
                  ]
                }
              }
            }
          },
          "400": {
            "description": "Request headers or body validation failed",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "example": {
                  "success": false,
                  "errors": [
                    {
                      "code": "1650",
                      "cause": "ESIGN_PARTNER_CAN_NOT_BE_EMPTY"
                    },
                    {
                      "code": "1650",
                      "cause": "ESIGN_ONBOARDING_PARTNER_CAN_NOT_BE_EMPTY"
                    },
                    {
                      "code": "1539",
                      "cause": "PARTNER_USER_ID_CAN_NOT_BE_EMPTY"
                    },
                    {
                      "code": "1539",
                      "cause": "PARTNER_USER_ID_TYPE_CAN_NOT_BE_EMPTY"
                    },
                    {
                      "code": "1539",
                      "cause": "PARTNER_SESSION_ID_CANNOT_BE_EMPTY"
                    },
                    {
                      "code": "1539",
                      "cause": "INVALID_FLOW"
                    },
                    {
                      "code": "1539",
                      "cause": "INVALID_PARTNER"
                    },
                    {
                      "code": "1539",
                      "cause": "INVALID_SOURCE"
                    },
                    {
                      "code": "1539",
                      "cause": "ADDITIONAL_DETAILS_IS_NULL"
                    },
                    {
                      "code": "1539",
                      "cause": "EMAIL_IS_NULL/EMAIL_IS_INVALID"
                    },
                    {
                      "code": "1539",
                      "cause": "PHONE_NUMBER_OR_EMAIL_IS_REQUIRED"
                    },
                    {
                      "code": "1539",
                      "cause": "PHONE_NUMBER_IS_INVALID"
                    },
                    {
                      "code": "1539",
                      "cause": "DATA_VERIFICATION_IS_EMPTY"
                    },
                    {
                      "code": "1539",
                      "cause": "EMAIL_VERIFICATION_IS_REQUIRED"
                    },
                    {
                      "code": "1539",
                      "cause": "EMAIL_VERIFICATION_REFERENCE_ID_IS_REQUIRED"
                    },
                    {
                      "code": "1539",
                      "cause": "PHONE_NUMBER_VERIFICATION_MUST_BE_TRUE"
                    },
                    {
                      "code": "1539",
                      "cause": "PHONE_NUMBER_VERIFICATION_REFERENCE_ID_IS_REQUIRED"
                    },
                    {
                      "code": "1539",
                      "cause": "DUPLICATE_PARTNER_SESSION_ID"
                    }
                  ]
                }
              }
            }
          },
          "401": {
            "description": "Invalid credentials",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "example": {
                  "success": false,
                  "data": null,
                  "errors": [
                    {
                      "code": "110",
                      "entity": "ESIGN_ADAPTER",
                      "cause": "UNAUTHORIZED"
                    }
                  ]
                }
              }
            }
          },
          "403": {
            "description": "Invalid onboarding partner",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ErrorResponse"
                },
                "example": {
                  "success": false,
                  "errors": [
                    {
                      "code": "110",
                      "cause": "ONBOARDING_PARTNER_DOES_NOT_BELONG_TO_CLIENT"
                    }
                  ]
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "parameters": {
      "OneKycToken": {
        "name": "x-onekyc-token",
        "in": "header",
        "required": true,
        "description": "IAB Partner token generated using the Get Partner Token API",
        "schema": {
          "type": "string"
        }
      },
      "OnboardingPartner": {
        "name": "x-onboarding-partner",
        "in": "header",
        "required": true,
        "description": "Used to identify the source of the request. Generated by IAB team.\nExample: CLIENT_X-WEB_SDK-STANDALONE_IDENTITY_VERIFICATION\n",
        "schema": {
          "type": "string"
        }
      },
      "PartnerUserId": {
        "name": "x-partner-user-id",
        "in": "header",
        "required": true,
        "description": "User ID of the current session. IAB will tie this info to the resulting submission ID.",
        "schema": {
          "type": "string"
        },
        "example": "c94d9a0d0ba648388842053db2a0d3ae"
      },
      "PartnerUserIdType": {
        "name": "x-partner-user-id-type",
        "in": "header",
        "required": true,
        "description": "Detailed name of the User ID. IAB will tie this info to the resulting submission ID.",
        "schema": {
          "type": "string"
        },
        "example": "GOPAY_ACCOUNT_ID"
      },
      "PartnerSessionId": {
        "name": "x-partner-session-id",
        "in": "header",
        "required": true,
        "description": "Session ID of the current session (generated by partner) that can be used as a correlation ID.\nShould be uniquely generated for each invocation. Acts as idempotency ID between Partner BE and IAB BE.\n",
        "schema": {
          "type": "string",
          "format": "uuid"
        },
        "example": "dd2a4352-8d65-4d24-8280-7c30ac8db83a"
      }
    },
    "schemas": {
      "InitiateFlowRequest": {
        "type": "object",
        "required": [
          "flow",
          "source"
        ],
        "properties": {
          "flow": {
            "type": "string",
            "description": "Specifies which flow to use",
            "enum": [
              "STANDALONE_IDENTITY_VERIFICATION"
            ]
          },
          "source": {
            "type": "string",
            "description": "Specifies which source the partner uses",
            "enum": [
              "SDK",
              "WEB_SDK"
            ]
          },
          "successRedirectionUrl": {
            "type": "string",
            "description": "URL where user will be redirected upon successful completion (required if source = WEB_SDK)"
          },
          "failureRedirectionUrl": {
            "type": "string",
            "description": "URL where user will be redirected if flow fails (required if source = WEB_SDK)"
          },
          "additionalDetails": {
            "$ref": "#/components/schemas/AdditionalDetails"
          }
        }
      },
      "AdditionalDetails": {
        "type": "object",
        "properties": {
          "email": {
            "type": "string",
            "format": "email",
            "description": "Email of the user",
            "example": "abc@xyz.com"
          },
          "phoneNumber": {
            "type": "string",
            "description": "Phone number of user.\nValidation: Start with 62, 11-15 chars (62 included)\n",
            "example": "628188888889"
          },
          "dataVerification": {
            "$ref": "#/components/schemas/DataVerification"
          },
          "userLocale": {
            "type": "string",
            "description": "Language to use for this flow",
            "enum": [
              "en_ID",
              "id_ID"
            ],
            "default": "id_ID"
          }
        }
      },
      "DataVerification": {
        "type": "object",
        "description": "Details of verification done by partner on behalf of the user",
        "properties": {
          "email": {
            "type": "object",
            "properties": {
              "isVerified": {
                "type": "boolean",
                "description": "Boolean field to determine if email has been verified by partner"
              },
              "verificationReferenceId": {
                "type": "string",
                "description": "Required if email.isVerified = true. ReferenceId for email verification."
              }
            }
          },
          "phoneNumber": {
            "type": "object",
            "properties": {
              "isVerified": {
                "type": "boolean",
                "description": "Boolean field to determine if phone number has been verified by partner"
              },
              "verificationReferenceId": {
                "type": "string",
                "description": "Required if phoneNumber.isVerified = true. ReferenceId for phone verification."
              }
            }
          }
        }
      },
      "InitiateFlowSdkResponse": {
        "type": "object",
        "properties": {
          "success": {
            "type": "boolean",
            "example": true
          },
          "data": {
            "type": "object",
            "properties": {
              "token": {
                "type": "string",
                "description": "IAB user token generated for the session"
              },
              "expirySeconds": {
                "type": "string",
                "description": "Time period in seconds for which the token will be valid",
                "example": "5184000"
              },
              "expiresAt": {
                "type": "string",
                "description": "End time value in epoch timestamp",
                "example": "1746253972"
              }
            }
          }
        }
      },
      "InitiateFlowWebSdkResponse": {
        "type": "object",
        "properties": {
          "success": {
            "type": "boolean",
            "example": true
          },
          "data": {
            "type": "object",
            "properties": {
              "launchUrl": {
                "type": "string",
                "format": "uri",
                "description": "Launch URL to start KYC flow for web users"
              },
              "expirySeconds": {
                "type": "string",
                "description": "Time period in seconds for which the token will be valid",
                "example": "5184000"
              },
              "expiresAt": {
                "type": "string",
                "description": "End time value in epoch timestamp",
                "example": "1750069227"
              }
            }
          }
        }
      },
      "ErrorResponse": {
        "type": "object",
        "properties": {
          "success": {
            "type": "boolean",
            "example": false
          },
          "data": {
            "type": "object",
            "nullable": true
          },
          "errors": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Error"
            }
          }
        }
      },
      "Error": {
        "type": "object",
        "properties": {
          "code": {
            "type": "string",
            "description": "Error code"
          },
          "cause": {
            "type": "string",
            "description": "Detailed message of the error"
          },
          "entity": {
            "type": "string",
            "description": "Entity that caused the error"
          }
        }
      }
    }
  }
}
```