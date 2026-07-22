# AI-Powered Competitor News Monitor & Weekly Digest
Automated n8n workflow that fetches AI/automation news, summarizes with AI, and delivers a weekly digest via Gmail.

## Description
This project implements an n8n workflow that collects headlines about AI and automation from public sources (TensorFeed and VentureBeat), processes them with a language model (GPT‑5.1), and generates a weekly digest automatically sent via Gmail.  
The goal is to provide a clear and professional summary of 5 key insights every week.


## Table of Contents
- [Workflow](#workflow)
- [Methodology](#methodology)
- [Prompts](#prompts)
- [Sample Output](#sample-output)
- [Results](#results)
- [Conclusion](#conclusion)

## Workflow
The workflow runs every Monday at 9 AM using a **Schedule Trigger**.  
It fetches news from:

- [TensorFeed](https://tensorfeed.ai/api/news)  
- [VentureBeat](https://venturebeat.com/feed/)  

If both sources fail, a fallback email is sent to notify that no valid headlines were found that week.

![n8n](Images/n8n_Workflow.png)

## Methodology
1. **Data Collection**: HTTP Request and RSS Feed nodes.  
2. **Validation**: Guardrails nodes to filter content.  
3. **Processing**: Code nodes merge titles and normalize data.  
4. **Insight Generation**: OpenAI node with GPT‑5.1 returns exactly 5 takeaways in `Title — Comment` format.  
5. **Formatting**: Code node builds a simple HTML digest.  
6. **Delivery**: Gmail node sends the digest email.

## Prompts
The prompt used in the OpenAI node:

```text
You are an assistant that analyzes news headlines about AI and automation.

From this list of 20 headlines:


{{ $json.titles }}


Return exactly 5 key takeaways in the following format, each with:
- "title": a short phrase (max 10 words)
- "comment": a short sentence (max 25 words)

Output only valid in the given format. Do not use JSON, arrays, brackets, quotes, or any other structure. And do not respond with anything else.
```

## Sample Output
The email contains an HTML digest with 5 headlines and short comments, under the title **Weekly Digest – AI & Automation**.

![Email Exito](Images/Envio_Exitoso.png)

If there is no data found in the requests, the email sent will be:

![Email Fallo](Images/Envio_Fallido.png)

## Results 
- The data requests were obtained and normalized into one format.
- The AI prompt was accurate and produced a good result.
- The decision to send the email in HTML format was made by the workflow logic, not by the AI model.
- The workflow can deliver an email with the latest news in a chosen field.

## Conclusion 
The workflow validates the requested data and controls the email logic outside the AI model. This avoids inconsistent HTML formats and ensures a stable weekly digest.
