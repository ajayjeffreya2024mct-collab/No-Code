# Experiment 9: Exploration of AI-Enabled Capabilities Embedded in Modern No-Code Applications

## 1. Aim

To explore and demonstrate the AI features available in modern no-code platforms and to evaluate how they enhance the applications built on them.

## 2. Objectives

- Identify categories of AI capabilities embedded in no-code tools.
- Try at least two AI features hands-on in a no-code platform.
- Evaluate accuracy, usefulness, limitations, and responsible-use considerations.

## 3. Requirements

| Item | Details |
|---|---|
| Platform | Zoho Creator (free trial) is used in this lab sequence. Alternatives: Microsoft Power Apps with AI Builder/Copilot, Airtable AI, Glide AI, Bubble with AI plugins |
| Sample data | A few text reviews, images (receipts or business cards), and a small tabular dataset |
| Browser | Chrome, Edge, or Firefox |

> **Availability note:** AI features, names, plans, and regional availability differ across platforms and change frequently. Check the platform's current documentation and your plan before starting. If a feature below is unavailable to you, substitute another AI feature the platform offers.

## 4. Theory

### 4.1 Categories of AI in No-Code Platforms

| Category | What It Does | Typical Use in an App |
|---|---|---|
| **AI-assisted app building** | Generates app structure, forms, or workflows from a natural-language prompt | "Create a leave request app with manager approval" |
| **Text analysis (NLP)** | Sentiment analysis, keyword extraction, language detection, summarization | Classify customer feedback as positive/negative |
| **Document and image intelligence** | OCR, business-card or receipt scanning, object detection | Auto-fill expense forms from receipt photos |
| **Predictive analytics** | Predict outcomes from historical data | Forecast churn, estimate lead conversion |
| **Conversational assistants** | Chatbots and natural-language queries on data | "Show me overdue tasks by team" |
| **Generative AI actions** | Draft emails, summarize records, generate content using LLM connectors | Summarize a case history; draft a reply |
| **AI-assisted automation** | Suggests or builds workflow logic and formulas | Generate scripts/formulas from a description |

### 4.2 Examples Across Platforms (illustrative; verify current features)

| Platform | Example AI Offerings |
|---|---|
| Zoho Creator | Zia assistant and AI fields (such as text, image, and document analysis), prediction capabilities, AI-assisted app and script help |
| Microsoft Power Platform | Copilot for building apps/flows, AI Builder models (form processing, text classification, prediction) |
| Airtable | AI fields for summarizing, categorizing, and generating text |
| Glide | AI components for text and image tasks in apps |
| Bubble | AI plugins and API connectors to external AI models |

### 4.3 How AI Is Integrated

1. **Built-in AI fields or components:** configure options, no code required.
2. **Connectors/API calls:** call an AI service (LLM, vision, speech) from a workflow.
3. **Natural-language builders:** prompt-to-app or prompt-to-formula features.

### 4.4 Responsible-Use Considerations

- **Accuracy and hallucination:** AI outputs can be wrong; add human review for important decisions.
- **Privacy:** Avoid sending sensitive personal data to AI services without a policy and consent.
- **Bias and fairness:** Check for biased outcomes, especially in people-related decisions.
- **Transparency:** Tell users when AI-generated content or decisions are involved.
- **Cost and limits:** AI calls may consume credits or count against usage quotas.

## 5. Procedure

### Part A: Survey the Platform's AI Features

1. Log in to the platform (e.g., Zoho Creator).
2. Browse the documentation and form-builder/field palette for AI-related items.
3. Record all AI features you can find in the table in Section 6.

### Part B: AI Text Analysis (Sentiment / Keywords)

1. Create an application named **Customer Feedback**.
2. Add a form **Feedback** with fields: Customer Name (Text), Email (Email), Comments (Multi-line).
3. Add an AI field (if available) that analyzes the **Comments** field, such as sentiment analysis or keyword extraction. If AI fields are unavailable, use a connector or a custom function that calls an AI service.
4. Enter at least 8 sample comments covering clearly positive, negative, mixed, and ambiguous language.
5. Record the AI result for each comment and compare it with your own judgment.

### Part C: Document or Image Intelligence (OCR / Scanning)

1. Create a form **Expense Claim** with fields: Vendor, Date, Amount, Receipt (Image/File).
2. Add an AI field for text or document recognition if the platform supports it.
3. Upload at least 5 sample receipts or business cards (use clear, non-sensitive samples; avoid real personal data).
4. Compare the extracted values to the actual values and calculate accuracy.

### Part D: Prediction (Optional)

1. Prepare a small dataset (for example, past leads with a "converted" outcome).
2. Use the platform's prediction builder (or AI Builder model) to train a basic model.
3. Review the platform's accuracy or confidence indicators.
4. Test predictions on a few new records.

### Part E: AI-Assisted Building (Optional)

1. Use the prompt-to-app or assistant feature with a prompt such as: *"Create an employee leave management app with a leave request form, manager approval, and a dashboard."*
2. Review the generated forms, fields, and workflows.
3. Note what is missing, wrong, or needs manual correction.

### Part F: Conversational Assistant (Optional)

1. Ask the platform's assistant natural-language questions about your data, such as *"How many feedback entries were negative this week?"*
2. Evaluate correctness against the actual data.

## 6. Observations

### AI Feature Inventory

| Feature | Category | Available on Your Plan? | Setup Effort (Low/Med/High) |
|---|---|---|---|
| | | | |

### Sentiment Analysis Evaluation

| # | Comment | AI Result | Your Judgment | Match? |
|---|---|---|---|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |

**Accuracy** = (Number of matches / Total comments) x 100 = ____ %

### OCR / Scanning Evaluation

| # | Field | Actual Value | Extracted Value | Correct? |
|---|---|---|---|---|
| 1 | Vendor | | | |
| 1 | Amount | | | |

**Field-level accuracy** = (Correct fields / Total fields) x 100 = ____ %

### AI-Assisted Build Review (if done)

| Item | Observation |
|---|---|
| Prompt used | |
| Components correctly generated | |
| Components missing or incorrect | |
| Manual effort still required | |

## 7. Result

AI-enabled capabilities of a no-code platform were explored and evaluated for accuracy, usability, and limitations.

## 8. Conclusion

Embedded AI lets non-programmers add intelligent features, such as text analysis, document extraction, and predictions, to their applications with little effort. Results should be validated, since accuracy varies with data quality, and responsible-use practices (privacy, transparency, human review) should be applied.

## 9. Viva Questions

1. Name four AI capabilities commonly embedded in no-code platforms.
2. How does an AI field differ from calling an external AI service through an API?
3. What is OCR and where is it useful in business apps?
4. Why should AI output be reviewed by humans for critical decisions?
5. What privacy risks arise when sending application data to AI services?
6. What is a prediction model's accuracy and how can you check it?
