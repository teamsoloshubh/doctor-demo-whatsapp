# Setup Guide

Kaise setup karna hai - step by step, non-coder friendly.

## Option A: n8n Cloud (Easiest - No Server Needed)

1. Sign up at n8n.cloud
2. Create workflow from the JSON files in workflows/ folder
3. Add WhatsApp credentials (Twilio / WATI / Gupshup)
4. Add FreeLLMAPI key
5. Connect database (Supabase or hosted PostgreSQL)
6. Activate workflow
7. Test with a WhatsApp message

Time: ~30 minutes
Cost: n8n Cloud free tier (2500 executions)

## Option B: Self-Hosted (Full Control)

1. Clone the repo: git clone https://github.com/teamsoloshubh/doctor-demo-whatsapp.git
2. Copy .env.example to .env and fill in credentials
3. docker-compose up -d
4. Open n8n UI at localhost:5678
5. Import workflows from workflows/ folder
6. Test with a real WhatsApp message

Time: ~1 hour
Cost: VPS or local PC

## Troubleshooting

### WhatsApp not receiving messages
- Check WhatsApp provider dashboard for active sessions
- Verify phone number is correct in .env
- Ensure webhook URL is accessible

### n8n not triggering
- Check n8n logs: docker-compose logs n8n
- Verify webhook URL is correct
- Test with curl

### LLM not responding
- Check FreeLLMAPI is running
- Verify API key in .env
- Check model name matches available models

## Next Steps

1. Configure clinic timings in docs/clinic-config.md
2. Import lead CRM schema
3. Set up staff handoff email
4. Test with a real patient number
