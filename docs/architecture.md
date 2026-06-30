# System Architecture

## Overview

This project is an AI-powered Gmail automation system built using **n8n**, **OpenAI**, **Docker**, and **Gmail**.

The workflow automatically processes incoming customer emails, understands the user's intent using AI, retrieves relevant order information when required, generates contextual responses, and sends replies through Gmail. Order-related interactions are also archived as JSON files on an FTP server for future reference and auditing.

---

# High-Level Architecture

```text
                           Customer
                               │
                               ▼
                         Gmail Inbox
                               │
                               ▼
                      n8n Automation Workflow
                               │
        ┌──────────────────────┼──────────────────────┐
        │                      │                      │
        ▼                      ▼                      ▼
  Email Processing      AI Intent Analysis     Order Lookup
        │                      │                      │
        └──────────────────────┼──────────────────────┘
                               │
                               ▼
                     Response Generation
                               │
                ┌──────────────┴──────────────┐
                ▼                             ▼
         Gmail Reply                 Order JSON Backup
                                                │
                                                ▼
                                           FTP Server
```

---

# System Components

## Gmail

Gmail serves as the communication channel between customers and the automation system.

Responsibilities include:

* Receiving customer emails
* Sending AI-generated replies
* Managing conversation threads

---

## n8n Workflow

n8n orchestrates the complete automation process.

Responsibilities include:

* Monitoring incoming emails
* Extracting relevant email information
* Routing requests based on customer intent
* Calling AI services
* Processing order-related requests
* Sending email responses
* Generating JSON backups
* Uploading files to the FTP server

---

## OpenAI

OpenAI provides the intelligence behind the automation.

Used for:

* Intent classification
* Natural language understanding
* Response generation
* Context-aware email drafting

---

## Order Data Source

The workflow retrieves order-related information whenever a customer requests updates or support.

Depending on the request, relevant order details are processed and formatted before generating a response.

---

## FTP Server

Order interactions are archived as structured JSON files.

Responsibilities include:

* Storing processed order data
* Maintaining audit records
* Supporting future integrations and reporting
* A sample generated file (`ORD-1777289966070.json`) is included in this repository for demonstration purposes.
---

# Workflow

## Incoming Email Processing

1. A customer sends an email.
2. Gmail triggers the n8n workflow.
3. Email content is extracted and normalized.
4. OpenAI analyzes the customer's request.
5. The workflow determines the appropriate action.

---

## Order Request Handling

1. Customer requests order information.
2. Relevant order details are retrieved.
3. Information is validated and formatted.
4. A structured JSON record is created.
5. The JSON file is uploaded to the FTP server.
6. AI generates a personalized response.
7. Gmail sends the reply to the customer.

---

## General Customer Queries

1. Customer sends a non-order-related question.
2. AI understands the request.
3. A contextual response is generated.
4. Gmail delivers the reply.

---

# Design Principles

The architecture is designed around the following principles:

* AI-assisted email automation
* Modular workflow design
* Event-driven processing
* Low-code automation with n8n
* Reusable workflow components
* Structured data archival
* Easy deployment using Docker

---
## Setup

1. Clone the repository.
2. Start n8n using Docker Compose.
3. Import `workflows/gmail-automation.json`.
4. Create the following credentials in n8n:
   - Gmail OAuth2
   - OpenAI API
   - FTP
5. Assign the created credentials to the corresponding workflow nodes.
6. Activate the workflow.
----

# Technology Stack

| Component           | Technology                  |
| ------------------- | --------------------------- |
| Workflow Automation | n8n                         |
| AI Model            | OpenAI                      |
| Email Service       | Gmail                       |
| Deployment          | Docker & Docker Compose     |
| Programming         | JavaScript (n8n Code Nodes) |
| Data Exchange       | JSON                        |
| File Storage        | FTP Server                  |

---

# Benefits

* Automated customer email handling
* AI-generated contextual responses
* Faster response times
* Reduced manual effort
* Structured order record archival
* Modular and maintainable workflow
* Easy deployment using Docker
* Easily extensible for additional business workflows
