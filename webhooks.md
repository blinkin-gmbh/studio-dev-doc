# Blinkin Webhooks Documentation

## Introduction

Blinkin uses webhooks to send real-time notifications about events in your account to your application. This document explains how to set up and use webhooks with Blinkin.

## Getting Started

1. Log in to Studio
2. Navigate to a Blink Settings > Webhooks
3. Add a new webhook endpoint URL where you want to receive notifications

## Available Webhook Events

Blinkin currently supports three types of webhook requests:

1. Single Form Response
2. Multiple Form Responses
3. AI Response

## Secure your Webhook Endpoint
On the Webhooks page you can create a Secure Key which will be sent in the header of the webhook request. You can use this key to verify that the request headers is coming from Blinkin. Named as `x-sign-secret`

## Request Format

Webhook requests are sent as HTTP POST requests to your specified endpoint. The request body contains a JSON payload with event details.

### Example Payload (Single Form Request)

```json
{
  "type": "form-response",
  "payload": {
    "form": {
      "id": "64340390-c960-4445-8a5f-ee762db610ed",
      "name": "Form 1",
      "fields": [
        {
          "id": "543bd6a0-012a-4354-a743-23bedef92347",
          "label": "GPS Location",
          "type": "image"
        }
      ]
    },
    "step": {
      "id": "928507ac-b902-41fb-a2e4-a62402da3f60",
      "name": "Step #1"
    },
    "blink": {
      "id": 213,
      "name": "Untitled Project 3"
    },
    "answers": {
      "543bd6a0-012a-4354-a743-23bedef92347": [
        "https://picassostorage.blob.core.windows.net/tenant/default/forms/01J5TB72HPP9BEQVKQ2VZ1GFM7.jpeg"
      ]
    },
    "submissionId": 328,
    "sessionId": 950,
    "submittedAt": "2024-08-21T08:30:10.042Z"
  }
}
```

### Example Payload (Multiple Forms Request)

```json
{
  "type": "form-response",
  "payload": {
    "forms": [{
      "id": "64340390-c960-4445-8a5f-ee762db610ed",
      "name": "Form 1",
      "fields": [
        {
          "id": "543bd6a0-012a-4354-a743-23bedef92347",
          "label": "GPS Location",
          "type": "image"
        }
      ]
    }, {
      "id": "78340390-c960-4445-8a5f-ee762db610ed",
      "name": "Form 2",
      "fields": [
        {
          "id": "666bd6a0-012a-4354-a743-23bedef92347",
          "label": "First name",
          "type": "short-text"
        }
      ]
    }],
    "steps": [{
      "id": "928507ac-b902-41fb-a2e4-a62402da3f60",
      "name": "Step #1"
    }, {
      "id": "32307ac-b902-41fb-a2e4-a62402da3f60",
      "name": "Step #2"
    }],
    "blink": {
      "id": 213,
      "name": "Untitled Project 3"
    },
    "answers": {
      "666bd6a0-012a-4354-a743-23bedef92347": "John",
      "543bd6a0-012a-4354-a743-23bedef92347": [
        "https://picassostorage.blob.core.windows.net/tenant/default/forms/01J5TB72HPP9BEQVKQ2VZ1GFM7.jpeg"
      ]
    },
    "submissionId": 328,
    "sessionId": 950,
    "submittedAt": "2024-08-21T08:30:10.042Z"
  }
}
```

### Example Payload (AI Response)

```json
{
  "type": "ai-response",
  "payload": {
    "blink": {
      "id": 92,
      "name": "AI"
    },
    "step": {
      "id": "2244f5d9-ee16-4f19-850b-b800b5e18308",
      "name": "Step #2"
    },
    "result": {
      "sourceInput": {
        "url": "https://picassostorage.blob.core.windows.net/ai-storage/1724336212884.jpeg",
        "name": "image"
      },
      "nextStep": {
        "id": "155ec927-68f5-4bc9-9731-c30658406429",
        "name": "Step #3"
      }
    },
    "sessionId": "988",
    "submittedAt": "2024-08-22T11:16:58.171Z"
  }
}
```