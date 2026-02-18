# 🤖 Automated LinkedIn Post Creator — n8n Workflow

An intelligent n8n workflow that takes a user's input and automatically generates a **LinkedIn post with an AI-generated image**, then publishes it directly to LinkedIn.

---

## 📌 Workflow Overview

<img width="1529" height="431" alt="image" src="https://github.com/user-attachments/assets/5c678805-128b-44f8-a683-1a80012796c3" />


The workflow is triggered by a form submission and runs through the following pipeline:

```
Form Submission → LinkedIn Post Agent (Tavily) → Image Generation Agent → OpenAI DALL·E → Convert to File → LinkedIn Post
```

---

## 🔁 Flow Breakdown

| Step | Node | Description |
|------|------|-------------|
| 1 | **On Form Submission** | User fills in their name, topic, and description |
| 2 | **LinkedIn Post Creation Agent** | AI agent uses Tavily (web search tool) to research the topic and craft an engaging LinkedIn post |
| 3 | **Image Generation Agent** | AI agent generates a tailored image prompt based on the post content |
| 4 | **HTTP Request (OpenAI Images API)** | Calls `POST https://api.openai.com/v1/images/generations` with the prompt to generate the image |
| 5 | **Convert to File** | Converts the Base64 image string into a file |
| 6 | **LinkedIn: Create a Post** | Publishes the generated post text + image to LinkedIn |

---

## 🧰 Tools & Services Used

- **[n8n](https://n8n.io/)** — Workflow automation platform
- **[Tavily API](https://tavily.com/)** — Real-time web search tool for the AI agent
- **[OpenAI GPT-4o](https://platform.openai.com/)** — Powers both the post creation and image prompt agents
- **[OpenAI DALL·E 3](https://platform.openai.com/docs/guides/images)** — Generates the LinkedIn post image
- **[LinkedIn API](https://developer.linkedin.com/)** — Publishes the final post

---

## 📥 Form Input Fields

When a user submits the form, they provide:

- **Name** — The author's name
- **Topic** — The subject of the LinkedIn post (e.g., "AI in Manufacturing")
- **Description** — A brief context or key points they want covered

---

## ⚙️ Setup Instructions

### 1. Import the Workflow
- In n8n, go to **Workflows → Add Workflow → Import from File**
- Upload the `linkedin-post-creator.json` file

### 2. Configure Credentials
Set up the following credentials in n8n:

| Credential | Where to get it |
|------------|----------------|
| OpenAI API Key | [platform.openai.com](https://platform.openai.com/api-keys) |
| Tavily API Key | [tavily.com](https://tavily.com/) |
| LinkedIn OAuth2 | [LinkedIn Developer Portal](https://developer.linkedin.com/) |

### 3. LinkedIn OAuth Setup
- Create a LinkedIn App at the [Developer Portal](https://www.linkedin.com/developers/)
- Add the OAuth2 redirect URI from n8n
- Request the `w_member_social` scope to allow posting
- Connect the credential in the **LinkedIn node**

### 4. Activate the Workflow
- Toggle the workflow to **Active**
- Share the form URL with users

---

## 🔄 Customization Tips

- **Change post tone** — Modify the system prompt in the LinkedIn Post Creation Agent node (e.g., "Write in a formal tone" or "Use bullet points")
- **Image style** — Adjust the image generation agent's system prompt to match your preferred visual style (e.g., "minimalist", "corporate", "illustrated")
- **Add approval step** — Insert a **Wait** node + email/Slack notification before publishing, so you can review the post before it goes live

---

## 📁 Repository Structure

```
├── README.md
├── linkedin-post-creator.json   # n8n workflow export
```

---

## 🚧 Known Limitations

- LinkedIn's API requires a **verified LinkedIn Developer App** with approved permissions
- Free-tier n8n does not support workflow version history — export the JSON manually after each update
- DALL·E 3 image generation may take 10–20 seconds

---

## 👤 Author

**Suryaraj** — AI Engineer  
Building intelligent automation solutions with Azure AI, n8n, and OpenAI.
