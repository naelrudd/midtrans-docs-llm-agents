---
updatedAt: 2026-05-07T18:14:57.000Z
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
    "title": "Esign APIs",
    "description": "APIs for Esign related operations such as certificate registration and document signing.",
    "version": "1.2.0",
    "contact": {
      "name": "GoTo OneKYC Team"
    }
  },
  "servers": [
    {
      "url": "https://onekyc.ky.id.sandbox.gopayapi.com",
      "description": "Sandbox - OneKYC Gateway"
    },
    {
      "url": "https://onekyc.ky.id.gopayapi.com",
      "description": "Production - OneKYC Gateway"
    }
  ],
  "paths": {
    "/esign-partner/v1/initiate-flow": {
      "post": {
        "summary": "Initiate Flow",
        "description": "Fetch the user token/launch URL needed to start the identity verification flow on frontend.\nAdditional details passed in this API will be stored and used during submission processing.\n",
        "operationId": "initiateFlow",
        "parameters": [
          {
            "$ref": "#/components/parameters/OneKycToken"
          },
          {
            "$ref": "#/components/parameters/EsignOnboardingPartner"
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
            "$ref": "#/components/responses/BadRequest"
          },
          "401": {
            "$ref": "#/components/responses/Unauthorized"
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
          },
          "500": {
            "$ref": "#/components/responses/InternalServerError"
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
        "description": "OneKYC Partner token generated using the Get Partner Token API",
        "schema": {
          "type": "string"
        },
        "example": "eyJraWQiOiJlYzdmMjY0ZS0wNDkwLTQxODgtYTRjZS0wMWZlMzQ2MWFmYzUi..."
      },
      "EsignOnboardingPartner": {
        "name": "x-esign-onboarding-partner",
        "in": "header",
        "required": true,
        "description": "Used to identify the source of the request (generated by OneKYC team)",
        "schema": {
          "type": "string"
        },
        "example": "CLIENT_X-BE-CERT_REG"
      },
      "PartnerUserId": {
        "name": "x-partner-user-id",
        "in": "header",
        "required": true,
        "description": "User ID of the current session. OneKYC will tie this info to the resulting submission ID",
        "schema": {
          "type": "string"
        },
        "example": "ddd91k2n-81j2-nsm9-019m-msj1291829ja"
      },
      "PartnerUserIdType": {
        "name": "x-partner-user-id-type",
        "in": "header",
        "required": true,
        "description": "Detailed name of the User ID. OneKYC will tie this info to the resulting submission ID",
        "schema": {
          "type": "string"
        },
        "example": "CLIENT_X_USER_ID"
      },
      "PartnerSessionId": {
        "name": "x-partner-session-id",
        "in": "header",
        "required": true,
        "description": "Session ID (generated by partner) used as correlation ID between partner and OneKYC. Must be unique for each invocation",
        "schema": {
          "type": "string"
        },
        "example": "test-0008"
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
            "$ref": "#/components/schemas/PhoneNumber"
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
      "PhoneNumber": {
        "type": "string",
        "description": "Phone number of user.",
        "example": "628188888889"
      },
      "ErrorResponse": {
        "type": "object",
        "properties": {
          "success": {
            "type": "boolean",
            "example": false
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
            "description": "Error code:\n- 110: Unauthorized, invalid token in header parameters\n- 900: Unknown error (500)\n- 1650: Missing header parameters (4XX)\n"
          },
          "entity": {
            "type": "string",
            "description": "Entity where the error occurred"
          },
          "cause": {
            "type": "string",
            "description": "Detailed message of the error"
          }
        }
      }
    },
    "responses": {
      "BadRequest": {
        "description": "Bad Request - Invalid input or missing required parameters",
        "content": {
          "application/json": {
            "schema": {
              "$ref": "#/components/schemas/ErrorResponse"
            },
            "example": {
              "success": false,
              "errors": [
                {
                  "code": "1539",
                  "cause": "PARTNER_USER_ID_CAN_NOT_BE_EMPTY"
                },
                {
                  "code": "1539",
                  "cause": "PARTNER_USER_ID_TYPE_CAN_NOT_BE_EMPTY"
                },
                {
                  "code": "1650",
                  "cause": "ESIGN_PARTNER_CAN_NOT_BE_EMPTY"
                },
                {
                  "code": "1650",
                  "cause": "ESIGN_ONBOARDING_PARTNER_CAN_NOT_BE_EMPTY"
                },
                {
                  "code": "1653",
                  "cause": "SUBMISSION_ID_DOES_NOT_BELONG_TO_CURRENT_USER"
                }
              ]
            }
          }
        }
      },
      "Unauthorized": {
        "description": "Unauthorized - Invalid or missing authentication token",
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
                  "cause": "UNAUTHORIZED"
                }
              ]
            }
          }
        }
      },
      "InternalServerError": {
        "description": "Internal Server Error - An unexpected error occurred on the server",
        "content": {
          "application/json": {
            "schema": {
              "$ref": "#/components/schemas/ErrorResponse"
            },
            "example": {
              "success": false,
              "errors": [
                {
                  "code": "900",
                  "cause": "GENERIC_SERVICE_ERROR"
                }
              ]
            }
          }
        }
      }
    }
  }
}
```