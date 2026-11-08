# Doctor Clinic WhatsApp Receptionist

AI-powered WhatsApp receptionist for doctor clinics.

## Features

- Appointment booking via WhatsApp
- Clinic timings management
- Lead follow-up automation
- Staff handoff

## Tech Stack

- Workflow engine: n8n
- WhatsApp gateway: Twilio / WATI / Gupshup
- LLM: FreeLLMAPI (gpt-4o-mini)
- Database: SQLite / PostgreSQL / Supabase

## Setup

Option A - n8n Cloud:
1. Sign up at n8n.cloud
2. Create workflow from workflows/ folder
3. Add WhatsApp provider credentials
4. Add FreeLLMAPI key
5. Connect database
6. Activate

Option B - Self-Hosted:
1. git clone this repo
2. Copy .env.example to .env
3. Fill in credentials
4. docker-compose up -d
5. Open n8n UI at localhost:5678
6. Import workflow from workflows/ folder

## Safety Rules

- Never give medical advice
- Never prescribe medication
- Never diagnose
- Always redirect to consult your doctor

## License

MIT
