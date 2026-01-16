#  NanoGen Studio API

This document provides a complete reference for the NanoGen Studio API.

---

## Table of Contents

1. [API Overview](#api-overview)
2. [Authentication](#authentication)
3. [Endpoints](#endpoints)
   - [`POST /api/generate`](#post-apigenerate)
4. [Data Structures](#data-structures)
   - [AIRequestConfig](#airequestconfig)
   - [AIResponse](#airesponse)
5. [Error Handling](#error-handling)

---

## API Overview

The NanoGen Studio API provides a unified interface for interacting with various generative AI models.

**Base URL**: `/api`

---

## Authentication

Currently, the API is intended for internal use and does not have a user-facing authentication mechanism. Future versions will incorporate authentication for multi-user support.

---

## Endpoints

### `POST /api/generate`

This is the primary endpoint for all AI generation tasks, including image creation, editing, and analysis.

**Request Body**

```json
{
  "prompt": "A futuristic cityscape",
  "images": ["data:image/png;base64,..."],
  "config": {
    "model": "gemini-3-flash-preview",
    "temperature": 0.7
  }
}
```

**Response Body**

```json
{
  "image": "data:image/png;base64,...",
  "text": null,
  "groundingSources": []
}
```

---

## Data Structures

### AIRequestConfig

This object allows for detailed configuration of the AI generation request.

| Field | Type | Description |
|---|---|---|
| `model` | `string` | The AI model to use. |
| `temperature` | `number` | Controls the creativity of the output. |
| `seed` | `number` | For reproducible results. |
| `thinkingBudget` | `number` | Enables deep reasoning for complex tasks. |
| `useSearch` | `boolean` | Enables Google Search grounding. |

### AIResponse

The unified response format for all AI generation requests.

| Field | Type | Description |
|---|---|---|
| `image` | `string` | The generated image in base64 format. |
| `text` | `string` | Textual output from the AI. |
| `groundingSources`| `Array` | Sources used for Google Search grounding. |

---

## Error Handling

The API uses standard HTTP status codes to indicate the success or failure of a request. The response body will contain a `message` field with more details about the error.

---

**Last Updated**: 2026-01-08
