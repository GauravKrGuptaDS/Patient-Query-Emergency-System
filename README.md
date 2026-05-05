# 🏥 Health Query & Emergency Response Workflow (n8n)

## 🚀 Project Overview

This project implements a **health query assistant with emergency detection** using n8n. It allows patients to:

* Get **general health advice** using an AI model
* Automatically detect **emergency situations**
* Log emergency cases into **Google Sheets** for further action

The workflow ensures safe handling of health-related queries by separating **routine queries** from **critical emergency scenarios**.

---

## 🧩 Architecture

```
Health Query Webhook
        ↓
Safety Check & Categorization
        ↓
    Emergency Router
      /        \
   YES          NO
   ↓            ↓
Append Row     Health Information AI
 (Google Sheet)      ↓
       ↓         Check AI Success
Emergency Response     ↓
       ↓         Format Health Response
        \        /
             Merge
              ↓
        Send Response
```

---

## ⚙️ Workflow Components

### 1. Health Query Webhook

* Entry point of the workflow
* Accepts user input (health-related query)

---

### 2. Safety Check & Categorization

* Evaluates the user query

* Uses **keyword-based detection** to identify emergency scenarios

* Matches predefined critical terms such as:

  * "chest pain"
  * "difficulty breathing"
  * "bleeding"
  * "unconscious"

* Classifies the query into:

  * Emergency
  * Non-emergency

---

### 3. Emergency Router

* Routes requests based on keyword detection result

**True (Emergency):**

* Triggered when predefined emergency keywords are found in the user query

**False (Non-Emergency):**

* No emergency keywords detected; treated as a general health query

---

### 4. Emergency Flow

#### Append Row in Google Sheet

* Stores emergency details such as:

  * Query
  * Timestamp
  * (Optional) User details

#### Emergency Response

* Sends predefined emergency guidance
* Example:

  * "Please seek immediate medical attention or contact emergency services"

---

### 5. Health Information AI

* Uses an AI model to generate responses
* Provides general health guidance
* Avoids diagnosis or prescriptions

---

### 6. Check AI Success

* Verifies if AI response was generated successfully
* Routes failures to fallback handling

---

### 7. Format Health Response

* Structures the AI output into a user-friendly format

---

### 8. AI Error Handler

* Handles failures from AI node
* Returns a safe fallback message

---

### 9. Merge Node

* Combines responses from:

  * Emergency path
  * AI response path

---

### 10. Send Response

* Sends final response back to the user

---

## 📊 Data Storage

### Google Sheets (Emergency Logging)

Used to store emergency cases for tracking and follow-up.

**Fields (example):**

* Timestamp
* User Query
* Severity

---

## 🔒 Safety Considerations

* The system does **not provide medical diagnosis**
* Emergency cases are **prioritized and separated**
* AI responses are **validated before sending**
* Fallback responses are used in case of failure

---

## ⚠️ Limitations

* Emergency detection is **keyword-based**, which may miss edge cases or context-specific emergencies
* Google Sheets is not suitable for real-time emergency handling
* No real-time alerting (SMS/Call) is implemented
* Limited user/session tracking

---

## 🔮 Future Improvements

* Integrate **PostgreSQL** for robust storage
* Add **SMS/Email alerts (Twilio)** for emergencies
* Implement **user/session management**
* Add **location tracking for emergency services**
* Improve classification using hybrid (rules + AI)
* Add multilingual support

---

## 🛠️ Tech Stack

* **n8n** – Workflow automation
* **LLM (AI Model)** – Health response generation
* **Google Sheets API** – Emergency logging

---

## 📌 Use Cases

* Health query chatbot
* Patient triage assistant
* Emergency detection system (prototype)

---

## 📣 Disclaimer

This system is intended for **informational purposes only** and should not be used as a substitute for professional medical advice, diagnosis, or treatment. Always seek the advice of a qualified healthcare provider in case of medical emergencies.

---

## 👨‍💻 Author

Developed as part of an AI workflow automation project using n8n.
