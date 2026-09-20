# VendorPlus Backend

FastAPI backend for **VendorPlus**, an AI-powered supplier follow-up and risk monitoring platform. It automates vendor status calls, turns supplier responses into structured delivery data, scores vendor risk, and triggers escalations.

> Built with [Eman (@Eman2123)](https://github.com/Eman2123) for the CALL-E hackathon. Full project (frontend + backend): [Eman2123/VendorPlus](https://github.com/Eman2123/VendorPlus)

## What it does

1. Places AI phone calls to vendors through CALL-E
2. Captures the supplier's response
3. Extracts structured delivery info from the conversation
4. Calculates a vendor risk score from delivery signals
5. Escalates high-risk or unreachable vendors by email alert
6. Serves vendor, call history, and dashboard data to the frontend

## Live Deployment

- **Backend API:** https://vendorplus.fastapicloud.dev
- **API Docs (Swagger):** https://vendorplus.fastapicloud.dev/docs
- **Frontend:** https://vendor-plus-xi.vercel.app

## Tech Stack

- Python, FastAPI, Uvicorn
- SQLAlchemy, PostgreSQL (Neon)
- Pydantic
- CALL-E (AI phone calls via CLI)
- Docker

## Project Structure

```text
VendorPlus_Backend/
├── app/
│   ├── db/             # Database models and schema
│   ├── routers/        # API routes
│   ├── schemas/        # Request/response schemas
│   ├── services/       # Calls, extraction, risk engine, alerts
│   └── main.py         # FastAPI application
├── .env.example
├── Dockerfile
├── entrypoint.sh
└── requirements.txt
```

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Aleeshal/VendorPlus_Backend.git
cd VendorPlus_Backend
```

### 2. Create a virtual environment

Python 3.12 is recommended.

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set up environment variables

Copy `.env.example` to `.env` and fill in the values:

```text
DATABASE_URL=
CALLE_API_KEY=
CALLE_ACCOUNT_EMAIL=
ALERT_EMAIL_FROM=
ALERT_EMAIL_APP_PASSWORD=
```

### 5. Set up the CALL-E CLI

Real phone calls need the CALL-E CLI:

```bash
npm install -g @call-e/cli
calle auth login
```

This opens a one-time browser login. The session token is cached locally and reused automatically.

### 6. Run the server

```bash
uvicorn app.main:app --reload
```

API: `http://127.0.0.1:8000`
Interactive docs: `http://127.0.0.1:8000/docs`

## Environment Variables

| Variable | Purpose |
| --- | --- |
| `DATABASE_URL` | PostgreSQL connection string |
| `CALLE_API_KEY` | CALL-E API authentication |
| `CALLE_ACCOUNT_EMAIL` | CALL-E account email |
| `ALERT_EMAIL_FROM` | Sender address for alerts |
| `ALERT_EMAIL_APP_PASSWORD` | App password for alert email delivery |
| `ALLOWED_ORIGINS` | Frontend origins allowed by CORS (comma-separated) |

Never commit real credentials or `.env` files.

## Docs

API contract and implementation notes live in the main repo's [docs folder](https://github.com/Eman2123/VendorPlus/tree/main/docs).

## License

MIT License.
