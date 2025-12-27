# Atlassian Integration Service (Azure Logic Apps)

## Overview
This project is a serverless middleware solution designed to automate the synchronization between **GitHub** development workflows and **Jira Service Management**. 

## Architecture
- **Source**: GitHub Webhook (Push Events)
- **Middleware**: Azure Logic Apps (Event-driven)
- **Destination**: Jira REST API v3

## Key Features
- **Dynamic Routing**: Extracts Jira Issue Keys (e.g., SAM1-10) directly from GitHub commit messages.
- **Automated Reporting**: Posts real-time build and deployment status updates as comments on relevant tickets.
- **Security**: Implements Basic Auth via Base64 encoded headers.

## Technical Stack
- Azure Logic Apps
- JSON Schema Validation
- Atlassian Document Format (ADF)

Built with Azure Logic Apps and Atlassian APIs.
commencing integration test
