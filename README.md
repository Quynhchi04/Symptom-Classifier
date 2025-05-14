# 🤖 Symptom Classifier Dataset Repository

This repository contains annotated training data for the **Symptom Classifier**, a feature designed to help users identify potential symptoms based on image inputs and generate text responses. The assistant responds to user-submitted images (such as rashes or other visible symptoms) and provides suggestions or queries for further information.

---

## 📁 Repository Structure
```
Symptom-Classifier/
│
├── data/
│ ├── raw/ # Raw collected image data
│ ├── annotated/ # Annotated image data files (CSV/JSON)
│ │ ├── symptom_batch1.json
│ │ └── ...
│ ├── processed/ # Cleaned, labeled data
│ │ └── ...
│
├── notebooks/ # Jupyter notebooks for preprocessing/training
│ └── ...
|
├── schema/
│ └── image_schema.json # Data schema definition for image inputs
│
├── scripts/ # Python scripts (e.g., for preprocessing)
│ └── ...
|
├── annotation_guidelines.md # Instructions for labeling image data
│
└── README.md # This file
```

## 🧾 Data Schema

Each data entry follows this schema:

| Field         | Type     | Description                                 |
|---------------|----------|---------------------------------------------|
| input         | object   | Image data (e.g., file path or base64) and optional question from user |
| response      | string   | Suggested or generated response             |
| intent        | string   | Purpose of the message (e.g., report_symptom, ask_diagnosis) |
| entities      | list     | Extracted keywords/phrases from image context or question (e.g., ["rash", "arm"]) |
| sentiment     | string   | Detected sentiment: positive, neutral, negative |
| meta          | object   | Additional metadata (e.g., age, gender, timestamp) |

---

## 🏷️ Annotation Process

- Annotators label each image with:
  - **Intent**: What is the user trying to do or express (e.g., report_symptom, ask_diagnosis)?
  - **Entities**: Key terms such as body parts or symptoms detected from the image or user input.
  - **Sentiment**: Emotional tone inferred from the image context or text.
  - **Meta Data**: Optional fields such as age, gender, and timestamp to enhance context.
- All annotations follow the [Annotation Guidelines](annotation/annotation_guidelines.md).

---

## 🧪 Example Entry

```json
{
  "input": {
    "image_path": "data/raw/rash_456.jpg",
    "question": "Should I be worried about this rash on my arm?"
  },
  "response": "It looks like a mild allergic rash. Monitor for 48 hours. If it spreads or itches severely, seek medical advice.",
  "intent": "report_symptom",
  "entities": ["rash", "arm"],
  "sentiment": "negative",
  "meta": {
    "age": 23,
    "gender": "male",
    "timestamp": "2025-05-14T12:34:56Z"
  }
}