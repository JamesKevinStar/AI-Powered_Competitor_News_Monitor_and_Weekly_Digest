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

## Workflow
The workflow runs every Monday at 9 AM using a **Schedule Trigger**.  
It fetches news from:

- [TensorFeed](https://tensorfeed.ai/api/news)  
- [VentureBeat](https://venturebeat.com/feed/)  

If both sources fail, a fallback email is sent notifying that no valid headlines were found that week.

![n8n](Images/n8n_Workflow.png)

## Methodology
1. **Data Collection**: HTTP Request and RSS Feed nodes.  
2. **Validation**: Guardrails nodes to filter content.  
3. **Processing**: Code nodes to merge titles and normalize data.  
4. **Insight Generation**: OpenAI node with GPT‑5.1, configured to return exactly 5 takeaways in `Title — Comment` format.  
5. **Formatting**: Code node builds a clean HTML digest.  
6. **Delivery**: Gmail node sends the digest email.

## Prompts
Example prompt used in the OpenAI node:





 



## Sample Output
The email contains an HTML digest with 5 headlines and short comments, under the title **Weekly Digest – AI & Automation**.

![Email Exito](Image/Envio_Exitoso.png)

But, if there isno data found in the requests, the email sended will be:

![Email Fallo](Image/Envio_Fallido.png)

## Resultados 
- Se identificó los patrones de comportamiento de compra de los clientes.
- Se clasificó a los clientes en diferentes grupos según su valor monetario, frecuencia de compra y recencia.
- También se determinó qué acciones realizar para cada grupo de clientes.

## Conclusión 
El análisis de datos permitió clasificar a los clientes en grupos distintos, lo cual puede ayudar a diseñar diferentes estrategias para atraer o mantener a los clientes.
