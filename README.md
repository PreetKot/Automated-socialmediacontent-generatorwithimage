# Automated Social Media Content Generator (with Image)

An **n8n workflow** that automatically turns an AI-related news link into:
1) a short **article summary**,  
2) a **ready-to-post LinkedIn caption**, and  
3) a **generated image** (via Freepik AI),  
then publishes the post to **LinkedIn**.

---

## What’s in this repo

- **`Automated Social Media Content Generation with Image.json`** — the n8n workflow export you can import into your n8n instance.
- **`Automated-socialmedia-contentgen-withimage.jpeg`** — a screenshot/preview of the workflow.

---

## Workflow overview (high level)

1. **Google Sheets Trigger**  
   Watches a Google Sheet for new rows (e.g., a row containing a `newslink`).

2. **Summarize Article (Gemini / LangChain node)**  
   Uses an LLM (Google Gemini Chat Model) to summarize the article from the provided link.

3. **Create LinkedIn Post (Gemini / LangChain node)**  
   Writes a professional LinkedIn post as an industry expert, based on the summary.

4. **Generate Image Prompt (Gemini / LangChain node)**  
   Produces a concise (≤ 50 words) prompt for an accompanying LinkedIn visual.

5. **Freepik AI Image Generation (HTTP Request + polling)**  
   Sends the image prompt to Freepik AI and polls until the image is ready.

6. **Download Image**  
   Downloads the generated image.

7. **Post to LinkedIn**  
   Publishes the LinkedIn post with the generated image.

---

## Requirements

- An **n8n** instance (self-hosted or cloud)
- **Google Sheets** credentials configured in n8n
- **Google Gemini** access configured in n8n (Gemini chat model nodes)
- **LinkedIn** credentials configured in n8n (LinkedIn node)
- A **Freepik API key** for image generation (used in the HTTP Request node)

---

## Setup / How to use

1. **Import the workflow**
   - In n8n: **Workflows → Import from File**
   - Select: `Automated Social Media Content Generation with Image.json`

2. **Connect credentials**
   - Google Sheets (for the trigger)
   - Google Gemini (for the 3 LLM steps)
   - LinkedIn (for publishing)
   - Freepik (via HTTP Request header `x-freepik-api-key`)

3. **Configure your Google Sheet**
   - Ensure your trigger sheet contains a column used by the workflow (commonly `newslink`).
   - Add a new row with a valid article URL to trigger the automation.

4. **Test run**
   - Use “Execute workflow” in n8n with a sample row.
   - Confirm you get:
     - summary text
     - LinkedIn caption text
     - generated image
     - successful LinkedIn post

---


## Customization ideas

- Change the tone/format for the LinkedIn post (more casual, more technical, add hashtags, etc.).
- Post to other platforms (X/Twitter, Instagram, Facebook) using additional n8n nodes.
- Store outputs back into Google Sheets (summary, caption, image URL).
- Add moderation/approval steps before publishing.

---

## License

Add a license if you plan to share or reuse this project publicly (e.g., MIT).
