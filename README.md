# Voice-Powered AI Personal Assistant

A sophisticated, voice-activated personal assistant built to streamline your daily administrative tasks. This project uses a powerful combination of workflow automation, agentic AI, and conversational voice technology to manage emails and calendar events entirely through natural language commands.

## ✨ Core Features

- **🗣️ Voice-First Interface:** Interact with your digital workspace using only your voice.
- **📧 Smart Emailing:** Draft and send emails on the fly. The assistant automatically finds the recipient's email from your contacts and signs off with your name.
- **🗓️ Intelligent Scheduling:**
    - **Check Availability:** Ask "Am I free tomorrow at 2 PM?" to check for conflicts.
    - **Create Events:** Book meetings with attendees. The assistant finds their email addresses, confirms availability, and sends the invites.
    - **Default Duration:** Automatically assumes a 30-minute meeting if no duration is specified.
- **🧠 Agentic Logic:** This isn't just a command-follower. The AI agent can perform multi-step tasks, use different tools in sequence, and handle ambiguity.

## 🛠️ Tech Stack

- **Workflow Automation:** [n8n.io](https://n8n.io/) (The central hub for all logic and integrations)
- **AI Agent & Logic:** [OpenAI](https://openai.com/) (GPT models for reasoning and content generation)
- **Conversational Voice:** [ElevenLabs](https://elevenlabs.io/) (For lifelike voice input and output)
- **Integrations:** Google Calendar, Gmail, Google Sheets (as a contact database)

---

## 🚀 Setup and Installation Guide

Follow these steps to get your own personal assistant up and running.

### Prerequisites

- An **n8n** instance (Cloud or self-hosted).
- An **OpenAI** API key.
- An **ElevenLabs** account with API access.
- A **Google Cloud** project with OAuth credentials and the Calendar & Gmail APIs enabled.
- A **Google Sheet** for your contacts with two columns: `Name` and `Email`.

### Step 1: Set up the n8n Workflow

1.  **Import the Workflow:** Download the `n8n-workflow.json` file from this repository and import it into your n8n instance.
2.  **Configure Credentials:** In n8n, go to the "Credentials" section and add your credentials for OpenAI and Google (OAuth2).
3.  **Link Your Contacts Sheet:** In the `contactData` (Google Sheets) tool node, select your credential and choose the Google Sheet you created for your contacts.
4.  **Configure the Agent:**
    - Copy the entire contents of the `prompt.md` file from this repository.
    - In the main "Agent" node in n8n, paste the copied text into the "Prompt" field.
    - Ensure your OpenAI credential is selected.

### Step 2: Set up the ElevenLabs Voice Agent

1.  Log in to your ElevenLabs account and create a new **Voice Agent**.
2.  **Configure the System Prompt:** You can use a simplified version of the main prompt for the ElevenLabs agent. A good starting point is in the `prompt.md` file.
3.  **Create Tools:** In the ElevenLabs agent settings, create the necessary tools (`send_email`, `createCalendarEvent`, etc.). Each tool will point to a specific webhook URL from your n8n workflow.
    - **Tool 1: `send_email`**
        - **Webhook URL:** Copy the webhook URL from the "Email Workflow" in n8n.
        - **Properties:** `recipient_name` (string), `email_context` (string).
    - **Tool 2: `createCalendarEvent`**
        - **Webhook URL:** Copy the webhook URL from the "Calendar Workflow" in n8n.
        - **Properties:** `event_details` (string), `event_timing` (string).
    - *(Add other tools like `checkAvailability` and `deleteCalendarEvent` in the same way, each pointing to the appropriate n8n webhook.)*

### Step 3: Connect and Test!

Once both sides are configured, you can start a conversation with your ElevenLabs voice agent. A voice command will trigger the corresponding tool in ElevenLabs, which calls the n8n webhook, triggering the AI agent to perform the multi-step task.

## 🤝 Contributing & Feedback

This project is a demonstration of what's possible with modern AI and automation tools. If you have ideas for improvements or want to connect, feel free to reach out to me on LinkedIn!

---
