# SendToN8N Responder

**SendToN8N** is a custom [Cortex](https://github.com/TheHive-Project/Cortex) responder that sends observable, alert, or case data to an [n8n](https://n8n.io/) workflow via a webhook.

This integration enables streamlined automation and orchestration between TheHive/Cortex and n8n for enrichment, alerting, ticketing, or other custom actions. ( Sky Is The Limit )

## Supported Data Types

- `thehive:case`
- `thehive:alert`
- `thehive:case_artifact`
- `thehive:case_task`
- `thehive:case_task_log`


## Installation

1. Clone or copy the responder into your Cortex responders directory:

    ```bash
    cd /opt/Custom-Analyzers/responders 
    git clone https://github.com/elohim666/Cortex-n8n-responder.git
    ```

2. Set proper permissions:

    ```bash
    cd Cortex-n8n-responder
    chmod 755 n8n.py
    chown cortex:cortex n8n.py
    pip install -r requirements.txt
    ```


3. Restart Cortex or click "Refresh Responders" in the Cortex UI.

   ```bash
   systemctl restart cortex
    ```

## Configuration

In the Cortex UI:

1. Go to **Organization > Responders**.
2. Locate and enable `n8n`.
3. Set the required configuration parameter:

| Name            | Type   | Required | Description                          |
|-----------------|--------|----------|--------------------------------------|
| `webhook` | string | Yes      | The full URL of the n8n webhook endpoint |

Example value:  
`https://n8n.example.com/webhook/thehive_trigger/abc123`

## Example Payload

The responder will send a POST request with JSON like this:

```json
{
  "type": "thehive:case_artifact",
  "id": "1234567890",
  "title": "Example Case",
  "observables": [
    {
      "dataType": "domain",
      "data": "malicious.com"
    }
  ]
}
