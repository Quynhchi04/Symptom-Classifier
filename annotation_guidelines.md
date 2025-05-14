# 🩺 AI Nurse Assistant — Annotation Guidelines

## 📘 Overview

These guidelines are for annotating image data to train an AI nurse assistant that can:

* Recognize symptoms based on images
* Provide care guidance for visible conditions
* Respond to user queries related to symptoms depicted in images

---

## 📦 Data Schema

Each annotated image must follow this format:

| Field       | Type   | Description                                                                       |
| ----------- | ------ | --------------------------------------------------------------------------------- |
| `input`     | object | Image data (e.g., file path or base64) and optional question from user            |
| `response`  | string | The assistant's suggested or generated reply                                      |
| `intent`    | string | The purpose behind the user’s message                                             |
| `entities`  | list   | Keywords or phrases related to symptoms, body parts, or conditions from the image |
| `sentiment` | string | Detected emotion: `positive`, `neutral`, or `negative`                            |
| `meta`      | object | Additional metadata, such as age, gender, and timestamp                           |

---

## 🎯 Intent Annotation

### What is **Intent**?

Intent represents the user's goal or the action they want to perform.

### ✅ Supported Intents

| Intent                  | Description                                                                    | Example                                          |
| ----------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------ |
| `report_symptom`        | User shares symptoms without asking for further guidance                       | "I have a rash on my arm."                       |
| `ask_health_guidance`   | User asks what to do about a visible symptom or whether to seek medical advice | "Should I visit the doctor for this rash?"       |
| `ask_medical_info`      | User asks for general medical or health information                            | "What causes skin rashes?"                       |
| `share_health_status`   | User shares a background condition or long-term health issue                   | "I have eczema."                                 |
| `ask_medication_info`   | User asks about medication side effects or usage (not for prescriptions)       | "Can I apply cream while using this medication?" |
| `confirm_understanding` | User acknowledges the assistant’s suggestion                                   | "Okay, I’ll keep an eye on it."                  |
| `deny_suggestion`       | User rejects or disagrees with the assistant's suggestion                      | "No, I don’t think that will help."              |
| `greeting`              | User starts the conversation with a greeting                                   | "Hello!"                                         |
| `goodbye`               | User ends the conversation                                                     | "Thanks, goodbye!"                               |
| `other`                 | Any message that doesn’t fit the above categories                              | "I like the way you help."                       |

---

## 🧩 Entity Annotation

### What are **Entities**?

Entities refer to important health-related keywords or phrases detected from the image context or user query. Examples include:

* **Symptoms**: ("rash", "swelling", "redness")
* **Conditions**: ("eczema", "psoriasis")
* **Body parts**: ("arm", "leg", "chest")
* **Time expressions**: ("since morning", "for two days")
* **Care terms**: ("apply cream", "rest")
* **Medication names**: ("hydrocortisone", "antibiotic")

### 📝 Guidelines

* Use **exact phrases** detected from the image or user input.
* Be specific; do not include generic words like “pain” or “feel” on their own.
* Always use **lowercase** unless it’s a proper noun (e.g., “Psoriasis”).

#### ✅ Examples

| Input                                           | Entities                                  |
| ----------------------------------------------- | ----------------------------------------- |
| "I have a red rash on my left arm."             | `["red rash", "left arm"]`                |
| "How long should I treat this skin irritation?" | `["treat", "skin irritation"]`            |
| "I applied hydrocortisone an hour ago."         | `["hydrocortisone", "an hour ago"]`       |
| "My leg is swollen and warm to the touch."      | `["swollen", "leg", "warm to the touch"]` |

---

## 😊 Sentiment Annotation

### What is **Sentiment**?

Sentiment refers to the emotional tone of the user’s message based on the image and text context.

| Sentiment  | When to Use                                                                        | Example                               |
| ---------- | ---------------------------------------------------------------------------------- | ------------------------------------- |
| `positive` | User appears calm, appreciative, or satisfied with the response                    | "This looks much better, thank you!"  |
| `neutral`  | User is neutral or asks for additional information without a strong emotional tone | "I’m not sure if this is serious."    |
| `negative` | User is upset, worried, or seeking help for a troubling symptom                    | "This rash is spreading, I’m scared." |

> If unsure, choose `neutral`.

---

## 🔍 Sample Annotations

### Example 1

```json
{
  "input": {
    "image_path": "data/raw/rash_123.jpg",
    "question": "Should I be concerned about this rash?"
  },
  "response": "It looks like a mild allergic rash. Keep an eye on it, but it should improve. If it worsens, consult a healthcare provider.",
  "intent": "report_symptom",
  "entities": ["rash", "allergic"],
  "sentiment": "concerned",
  "meta": {
    "age": 30,
    "gender": "female",
    "timestamp": "2025-05-14T14:45:23Z"
  }
}
```
