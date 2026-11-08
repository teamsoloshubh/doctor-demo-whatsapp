# Lead CRM Schema

Lead tracking aur follow-up automation ka structure.

## Lead Record

| Field | Type | Description |
|---|---|---|
| id | integer | Auto-increment primary key |
| phone | string | WhatsApp number (with country code) |
| name | string | Patient/lead name |
| status | enum | new, contacted, appointment-booked, converted, lost |
| source | enum | whatsapp, referral, website, walk-in |
| first_contact_date | datetime | When we first contacted |
| last_followup_date | datetime | Last follow-up sent |
| appointment_date | datetime | Booked appointment (if any) |
| notes | text | Any relevant notes |
| created_at | datetime | Record created |
| updated_at | datetime | Last update |

## Follow-up Rules

| Rule | Trigger | Action |
|---|---|---|
| New lead | Status = new | Follow up within 2 hours |
| No response | No reply in 24h | Gentle reminder |
| Appointment booked | Status = appointment-booked | 24h before reminder |
| No-show | Missed appointment | Follow up within 48h |
| Lost lead | Status = lost | Re-engage after 30 days |

## Staff Handoff

When the bot cannot handle a query:
1. Bot sends: I will connect you with our reception team. One moment please.
2. Staff receives notification with full conversation context
3. Staff takes over from WhatsApp
4. Lead status updated to: staff-handled

## Database (SQLite)

CREATE TABLE leads (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  phone TEXT NOT NULL,
  name TEXT,
  status TEXT DEFAULT 'new',
  source TEXT DEFAULT 'whatsapp',
  first_contact_date DATETIME DEFAULT CURRENT_TIMESTAMP,
  last_followup_date DATETIME,
  appointment_date DATETIME,
  notes TEXT,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
  updated_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE appointments (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  lead_id INTEGER REFERENCES leads(id),
  doctor_name TEXT NOT NULL,
  date DATE NOT NULL,
  time_slot TEXT NOT NULL,
  status TEXT DEFAULT 'booked',
  notes TEXT,
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_leads_status ON leads(status);
CREATE INDEX idx_leads_phone ON leads(phone);
CREATE INDEX idx_appointments_date ON appointments(date);
