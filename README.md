<img width="1443" height="780" alt="image" src="https://github.com/user-attachments/assets/da6ec623-1ad6-4bf9-b901-6d57c904422b" />
### **GitHub README Structure**

#### **1. Project Overview**

A serverless integration bridge between GitHub and Jira Cloud using Azure Logic Apps. This project automates ticket updates while ensuring system resilience through advanced retry policies.

#### **2. System Architecture & Workflow**

> <img width="1344" height="781" alt="image" src="https://github.com/user-attachments/assets/1860ef83-7b71-4ac5-8d25-8672c7418ee5" />


* This diagram shows the end-to-end event-driven architecture, starting from a GitHub Webhook trigger to the final Jira REST API call.
* **Technical Note**: I used a "Guard Clause" (Condition block) to validate payloads, ensuring only commits with a valid Jira Key (SAM-XXX) proceed to the API.

#### **3. Data Parsing & Logic**

To extract the Jira Key from the commit message, I used these dynamic expressions:

* **Find Key Start**: `indexOf(item()?['message'], 'SAM-')`
* **Extract Key**: `substring(item()?['message'], outputs('Start_Index'), 7)`

#### **4. Resilience Engineering (The Retry Policy)**

> <img width="1443" height="780" alt="image" src="https://github.com/user-attachments/assets/09f7ac1b-8bda-431f-b4c3-95e46987d694" />


* I implemented an **Exponential Backoff** policy to handle transient network errors.
* **Configurations**:
* **Count**: 4 attempts.
* **Intervals**: Start at `PT20S`, min `PT10S`, and max `PT1H`.


* This ensures the integration is "production-ready" and respects Jira's API rate limits.

#### **5. Verification & Results**

><img width="1857" height="895" alt="succeedevent" src="https://github.com/user-attachments/assets/07d4498d-1764-4279-8e91-4b0a27359d00" />
<img width="1572" height="894" alt="image" src="https://github.com/user-attachments/assets/fb322248-97b0-4a2b-8f20-d1cf8446d589" />
<img width="1857" height="895" alt="failuretestcase" src="https://github.com/user-attachments/assets/fb994d84-262c-47df-bbfc-2c16892461f8" />



* **Run History**: Proves 100% success rate across multiple test cases, including "Cold Starts" and varied commit lengths.
* **Jira Evidence**: Shows the final formatted comment in the Jira ticket, confirming successful REST API authentication and ADF payload delivery.

#### **6. Monitoring & Alerting**

> <img width="1920" height="587" alt="emailnotification" src="https://github.com/user-attachments/assets/154c079a-c380-4ccb-8be6-5d3d90561e68" />


* As a Support Engineer, visibility is key. I added an Office 365 action to send automated alerts, ensuring the team is notified the moment a critical sync is processed.

---

