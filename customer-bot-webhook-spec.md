# Velora Customer Bot Webhook Spec

This demo page can notify a duty workflow when human handoff is needed.
The classroom build has a default public ntfy demo channel, so it works without n8n setup.

## Endpoint

Default classroom endpoint:

```text
https://ntfy.sh/velora-cycle-demo-paul-20260707
```

Live demo inbox:

```text
https://ntfy.sh/velora-cycle-demo-paul-20260707
```

You can replace it by pasting an HTTPS n8n or Zapier webhook URL into the page's "值班通道" field.

The page sends:

```http
POST <webhook-url>
Content-Type: text/plain;charset=utf-8
```

## Payload

```text
Velora demo handoff ticket: TICKET-20260707-98424
Customer message: 找真人啊
Suggested next step: 我先幫你接到真人客服流程...
Created: 2026-07-07T12:00:00.000Z
Privacy: demo-only-no-real-customer-data
```

## Minimal n8n workflow

1. Webhook Trigger
   - Method: POST
   - Path: any safe demo path, e.g. `velora-handoff`
2. Optional Set node
   - Keep `id`, `customerMessage`, `handoffMessage`, `createdAt`
3. Notify node
   - Gmail, Telegram, Slack, LINE, or Google Chat
   - Suggested message:

```text
Velora demo handoff ticket: {{$json.id}}
Customer message: {{$json.customerMessage}}
Suggested next step: {{$json.handoffMessage}}
Created: {{$json.createdAt}}
```

## Safety

Do not use real customer data in this classroom demo.
Do not put API keys, cookies, admin URLs, or private order details into the page.
