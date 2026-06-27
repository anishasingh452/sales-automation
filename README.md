# Multi-Agent Sales Automation

[![Powered by n8n](https://img.shields.io/badge/Powered_by-n8n-FF6600?style=for-the-badge&logo=n8n&logoColor=white)](https://n8n.io)
[![LLM - OpenRouter](https://img.shields.io/badge/LLM-OpenRouter-000000?style=for-the-badge)](https://openrouter.ai/)
[![CRM - Pipedrive](https://img.shields.io/badge/CRM-Pipedrive-00A651?style=for-the-badge&logo=pipedrive&logoColor=white)](https://www.pipedrive.com/)
[![Voice - ElevenLabs](https://img.shields.io/badge/Voice-ElevenLabs-111111?style=for-the-badge)](https://elevenlabs.io/)

> **End-to-End Autonomous Sales Workflow Powered by Specialized AI Agents: From Prospect Discovery to Demo Booking.**

---

## Overview

The **Multi-Agent Sales Automation** system is an end-to-end intelligent orchestration built to automate the entire sales pipeline. Triggered simply by uploading an Ideal Customer Profile (ICP) as a PDF, the system autonomously discovers prospects, enriches leads, crafts personalized outreach, conducts AI voice calls, schedules demos, and records deals directly into your CRM.

## The AI Agent Swarm

This system is built around 7 highly specialized AI agents working synchronously:

1. **Business Development Manager (BDM) Agent (The Orchestrator):** Watches Google Drive for new ICP uploads, extracts/analyzes requirements, and delegates tasks to specialized agents.
2. **Prospecting Agent:** Discovers qualified companies and contacts based on the ICP, and verifies email addresses.
3. **RevOps Agent:** Automatically structures and stores prospect data in the CRM (Creates Organizations, Contacts, and Leads).
4. **SDR Agent:** Reads CRM contacts and automatically drafts highly personalized outreach emails in Gmail.
5. **Account Executive Agent (Voice AI):** Engages in real-time voice conversations with prospects, answers questions, and qualifies demo booking intent.
6. **Demo Booking Agent:** Coordinates real-time calendar availability, resolves scheduling conflicts, and automatically creates Google Calendar events.
7. **Deal Recording Agent:** Converts qualified prospect interactions into structured CRM entities (Deals) and triggers real-time alerts.

## Tech Stack & Integrations

* **Orchestration:** [n8n](https://n8n.io)
* **LLM Intelligence:** [OpenRouter](https://openrouter.ai/) (Utilizing top-tier models like OpenAI GPT-4/GPT-5 variants)
* **Voice AI:** [ElevenLabs](https://elevenlabs.io/) (Speech-to-Text & Text-to-Speech)
* **CRM:** [Pipedrive](https://www.pipedrive.com/)
* **Contact Enrichment:** [Hunter.io](https://hunter.io/) (Domain Search, Email Finder, Email Verifier)
* **Workspace & Comms:** Google Workspace (Drive, Gmail, Calendar)
* **Notifications:** [Pushover](https://pushover.net/)

---

## Prerequisites

Before running the application, ensure you have active accounts and API keys for the following services:
* **n8n Instance** (Self-hosted or Cloud)
* **OpenRouter API Key**
* **ElevenLabs API Key**
* **Hunter API Key**
* **Pipedrive API Token** (Ensure you have Admin access to configure pipelines and custom fields)
* **Google Cloud Console Service Account** (With access to Google Drive, Gmail, and Google Calendar APIs)
* **Pushover Application Token & User Key**

---

## Installation & Setup

### 1. Import the Workflow Orchestration
1. Open your n8n instance.
2. Click on **Workflows** -> **Import from File**.
3. Select the provided `workflow.json` (or copy/paste the JSON definition).
4. Save the workflow.

### 2. Configure Credentials in n8n
Navigate to **Credentials** in n8n and set up the following:
* Add your **OpenRouter API Key** (Under generic Header Auth or OpenAI compatible node).
* Add your **ElevenLabs API Key**.
* Connect your **Pipedrive** account via OAuth or API Key.
* Add your **Hunter.io API Key**.
* Set up Google Service Account credentials and authenticate **Google Drive**, **Google Calendar**, and **Gmail**.
* Add your **Pushover** keys for the notification nodes.

### 3. CRM Preparation (Pipedrive)
* Ensure your Pipedrive pipeline has standard stages configured (e.g., *Lead Discovered*, *Contacted*, *Demo Scheduled*, *Qualified*).
* Verify that the RevOps and Deal Recording agents map correctly to your specific Pipedrive custom fields. 

### 4. Google Drive Preparation
* Create a dedicated folder in your Google Drive named `Sales_Automation_ICPs`.
* Share this folder with your Google Service Account email to ensure the system can listen for file creation triggers.

---

## How to Run the Application

The beauty of this system is its fully autonomous nature. Once setup is complete, it requires zero manual data entry.

1. **Activate the Workflow:** Ensure your n8n workflow is set to **Active**.
2. **Trigger the Process:** 
   * Create an Ideal Customer Profile (ICP) detailing your target industry, titles, company sizes, and pain points.
   * Export this profile as a `.pdf` file.
   * Upload the PDF to the `Sales_Automation_ICPs` folder in Google Drive.
3. **Monitor the Magic:**
   * **Data Extraction:** The BDM agent will instantly download and parse the PDF.
   * **Prospecting & CRM:** Check your Pipedrive inbox; you will see new verified Leads popping up within minutes.
   * **Outreach:** Check your Gmail Drafts to review or auto-send the personalized emails created by the SDR Agent.
   * **Notifications:** You will receive real-time push notifications via Pushover as demos are successfully scheduled by the Account Executive and Demo Booking agents.

---

## Troubleshooting

* **No Workflow Trigger:** Verify that the Google Drive polling node is checking the exact Folder ID where you upload the ICP PDF.
* **Email Drafts Not Generating:** Check OpenRouter rate limits or account balance. Ensure the SDR Sub-Agent node has proper Gmail write permissions.
* **Demo Scheduling Fails:** Verify that your Google Calendar permissions allow the Service Account to create events and check availability for the specified user.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
