# 🍎 AI-Based Food Image Classifier using Power Automate

This project uses **Power Automate**, **Azure Blob Storage**, and **Computer Vision AI** to analyze uploaded food images and classify them as **healthy**, **unhealthy**, or a **mixture of both**. The results are then emailed as feedback.

---

## 📌 Features

- Automatically triggers when an image is uploaded to Azure Blob Storage
- Uses AI (Computer Vision) to extract image tags
- Checks confidence scores and classifies food type
- Sends smart feedback via email:
  - ✅ Healthy Food
  - ❌ Unhealthy Food
  - ⚖️ Both

---

## 🧠 Tech Stack

| Tool              | Description                        |
|-------------------|------------------------------------|
| Power Automate    | Logic builder & automation flow    |
| Azure Blob Storage| Stores uploaded images             |
| Azure Computer Vision API | Tag extraction from images  |
| Office 365 (Email)| Sends feedback via email           |

---

## 🔄 Flow Steps

1. **Trigger**: When a blob is added to a specific Azure container
2. **HTTP Action**: Sends image to Vision API and gets tags
3. **Parse JSON**: Extracts `tags`, `confidence`, and `name`
4. **Loop (For each)**:
    - If `confidence > 0.8`
        - If `name == fruit` → set `hasHealthy = true`
        - If `name == cheese` → set `hasUnhealthy = true`
5. **Final Condition** (After loop):
    - ✅ If both: "Healthy & Unhealthy"
    - ✅ If only healthy: "Healthy"
    - ✅ If only unhealthy: "Unhealthy"
6. **Send Email**: Based on classification result

---

## 🧪 Sample Output

```json
{
  "tags": [
    {"name": "fruit", "confidence": 0.98},
    {"name": "cheese", "confidence": 0.92}
  ]
}
