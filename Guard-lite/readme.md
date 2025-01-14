# DamascoGuard LITE API Documentation

---

## **Company Overview**

Damasco AI is a real-time security platform designed to protect AI-powered systems—like DeFi protocols and DAOs—from threats such as prompt injections, data leaks, and smart contract exploits. By acting as a “firewall” between large language models (LLMs) and sensitive operations, Damasco ensures secure, compliant interactions without sacrificing performance.

With a focus on adaptive threat detection, strict validation layers, and seamless integration into blockchain and AI infrastructure, Damasco empowers organizations to leverage AI safely and transparently. As the demand for trustworthy, autonomous systems grows, Damasco is positioned to become the security standard for decentralized, AI-driven ecosystems.

---

## **DamascoGuard LITE API**

### **Overview**

The DamascoGuard LITE API is a streamlined version of the full DamascoGuard API, designed specifically for the community to provide simplified yet powerful monitoring and analysis of messages. It assigns a safety score, identifies inappropriate content, detects potential security breaches, and more. This API can be seamlessly integrated to monitor agent replies or user message requests and can also function as an LLM by generating direct replies. The LITE version offers essential features, making it an accessible and effective solution for community-driven use cases.

---

### **Base URL**
https://guard.damasco.ai/monitoring

---

## **Authentication**

- **Auth Type**: API Key Authentication  
- **API Key**: You can obtain your API key from the Damasco dashboard at [dash.damasco.ai](https://dash.damasco.ai).

### **How to use the API Key**

Include your API key in the `x-api-key` header:

```bash
x-api-key: <your-api-key>
```

## **Request Details**
	•	HTTP Method: POST
	•	Endpoint: /monitoring

## **Request Parameters**

| **Parameter**   | **Type**  | **Description**                                                                                                 | **Required** |
|-----------------|-----------|-----------------------------------------------------------------------------------------------------------------|--------------|
| **message**     | `string`  | The message to be analyzed or generated.                                                                         | Yes          |
| **product**     | `string`  | The name of the LLM product (e.g., OpenAI, Llama). **Currently, only OpenAI is supported.**                      | No          |
| **model**       | `string`  | The specific model to use (e.g., GPT-4o, GPT-4o-mini, GPT-4, GPT-3.5).                                           | No          |
| **prompt_reply**| `boolean` | If `TRUE`, DamascoGuard will process the prompt and return the generated reply; if `FALSE`, only analysis occurs. | Yes          |

## **Example Use Case Scenarios**

1. **Customer Support Sentiment Analysis**: Detect if customer messages express frustration or are requesting assistance.  
2. **Sales Intent Detection**: Identify when users are inquiring about purchasing or subscribing to services.  
3. **Prompt Injection Prevention**: Mitigate attempts to manipulate LLMs through malicious prompts.  
4. **Inappropriate Content Detection**: Identify and block harmful or inappropriate content in user-generated messages.  

### **Example Request (Python)**

Here is an example of a POST request to the DamascoGuard API using Python:

```
python import requests

url = "https://guard.damasco.ai/monitoring"
api_key = "your_api_key_here"

payload = {
    "message": "Can I see last month’s financial report?",
    "product": "openai",
    "model": "gpt-4",
    "prompt_reply": False
}

headers = {
    "x-api-key": api_key,
    "Content-Type": "application/json"
}

response = requests.post(url, json=payload, headers=headers)
print(response.json())
```

### **Response Format**

The API will return a JSON object containing the following keys:

#### **Response Body Example**

```json
{
  "message": "Your financial report is not available at the moment due to privacy settings.",
  "success": true,
  "objective": "Request for financial report information.",
  "sentiment": "Curiosity",
  "keywords": "financial report, privacy settings",
  "ai_score": 85,
  "inappropriate_score": 0,
  "hack_score": 5,
  "security_breach": 0,
  "support_request": true,
  "sales_request": false
}
```

#### **Field Descriptions**

| Field               | Type    | Description                                                                                   |
|---------------------|---------|-----------------------------------------------------------------------------------------------|
| `message`           | string  | The message of the user.                                                                       |
| `success`           | boolean | Indicates whether the request was processed successfully.                                      |
| `objective`         | string  | The detected objective or intent of the message (e.g., "requesting financial data", "inquiring about services"). |
| `sentiment`         | string  | The detected sentiment of the message (e.g., Joy, Curiosity, Frustration, Anxiety, Hope).       |
| `keywords`          | string  | Relevant keywords extracted from the message (e.g., "financial report, privacy settings").      |
| `ai_score`          | integer | Probability that the message was generated by AI (0 to 100).                                    |
| `inappropriate_score` | integer | Indicates the likelihood that the message contains inappropriate content (0 to 100).          |
| `hack_score`        | integer | Probability that the message is attempting to hack or manipulate the AI (0 to 100).             |
| `security_breach`   | integer | Indicates a security breach attempt (e.g., unauthorized data access or exploitation attempts) (0 to 100). |
| `support_request`   | boolean | Indicates if the message is a support-related inquiry (True/False).                             |
| `sales_request`     | boolean | Indicates if the message is sales-related (True/False).                                              |

### **Error Responses**

#### **Common Errors**

| Error Code | Message                | Description                                                                                         |
|------------|------------------------|-----------------------------------------------------------------------------------------------------|
| 400        | Bad Request            | Missing or invalid parameters. Ensure that all required fields are correctly formatted.              |
| 401        | Unauthorized           | Invalid API Key. Ensure that your key is correct and active.                                         |
| 403        | Forbidden              | Your API key does not have sufficient permissions.                                                   |
| 429        | Rate Limit Exceeded    | You have exceeded the rate limit for your API key.                                                    |
| 500        | Internal Server Error  | An error occurred on the server side. Try again later or contact support.                             |

### **How to Get an API Key**

To start using the DamascoGuard API, follow these steps:
1. Go to Damasco Dashboard.
2. Select the amount of credits you wish to purchase.
3. Transfer the specified amount to the provided wallet address.
4. Once the transaction is confirmed, you will receive your credits.
5. You can monitor your usage and available credits on your dashboard.

### **Technical Support**

For technical issues or questions, please contact our support team at:

- **Email**: support@damasco.ai
- **SLA**:
  - **Response Time**: 24 hours (Standard)
  - **Critical Issues**: 12 hours (Priority)
  - **Uptime Guarantee**: 99.5%

---

This documentation serves as a complete guide to integrate DamascoGuard into your business processes securely and efficiently. For further customization or inquiries, feel free to reach out!
