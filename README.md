# n8n AI Lead Automation Demo

A portfolio demonstration of CRM lead automation and local AI-assisted lead classification, built with n8n, JavaScript, Google Sheets, Gmail, and Ollama (Qwen 2.5 3B).

## What the project does

The exported n8n workflow contains two separate demonstration paths:

### 1. CRM lead automation
- Receives lead information through a webhook.
- Extracts contact details and service requests.
- Uses JavaScript keyword rules to classify leads as HIGH or NORMAL priority.
- Routes leads through conditional branches.
- Includes Gmail notifications, customer acknowledgements, and Google Sheets logging.

### 2. Local AI classification prototype
- Runs a fixed sample customer message through a local Ollama model (Qwen 2.5 3B).
- Requests a structured JSON response containing `category`, `priority`, and `reason`.
- Validates JSON syntax, required non-empty fields, and allowed priority values using JavaScript.
- Routes valid and invalid outputs to separate branches.
- Preserves the original AI response and validation error for inspection.

## Testing and error handling

I tested the AI branch with a sample urgent heating request. The model returned a JSON response, which passed the validator and followed the valid branch.

I also deliberately requested an invalid plain-text response. The validator rejected it, recorded the parsing error, and routed the item through the false branch. After restoring the normal prompt, the workflow executed successfully again.

## Current limitations

This is a local portfolio prototype, not a production deployment or a client-used system. The AI branch currently uses a fixed sample message and is not connected to the CRM webhook path. The validator checks response structure and permitted priority values; it does not independently verify whether the AI's classification is factually correct against the original customer message. The invalid-output branch is not yet connected to a human-review queue.

## Tools

- n8n
- Ollama with Qwen 2.5 3B (local model)
- JavaScript
- JSON
- Gmail and Google Sheets nodes

## How to explore

1. Import `CRM_Lead_Automation_AI_Demo_PUBLIC.json` into n8n.
2. Configure your own credentials for the Gmail, Google Sheets, and Ollama nodes if you want to run them.
3. Install Ollama and download `qwen2.5:3b` to run the AI demonstration locally.
4. Run the manual trigger to test the AI classification branch.

The exported file is sanitized for public sharing. It does not include working credentials or personal account configuration.
