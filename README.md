
# MediNotes Pro — Healthcare Consultation Assistant

MediNotes Pro is a **demo healthcare consultation assistant** that helps clinicians transform raw consultation notes into three clear, structured outputs:

- **Summary** for medical records  
- **Next steps** for clinician follow-up  
- **Patient-friendly email** written in simple, non-technical language  

> ⚠️ **Demo only**  
> This application is for product and engineering demonstration purposes.  
> **Do not use with real patient data. Not for clinical use.**

---

## What It Does

MediNotes Pro streamlines clinical documentation by using AI to:

- Generate a concise, structured consultation summary suitable for records
- Produce clear next steps, follow-ups, and safety-netting guidance
- Draft a patient-friendly email explaining outcomes and instructions
- Stream responses in real time for fast feedback
- Enforce authentication and subscription access controls

---

## How It Works

1. A clinician signs in using secure authentication
2. Consultation details are entered via a structured form:
   - Patient name
   - Date of visit
   - Free-text consultation notes
3. The frontend sends a **POST request** to the backend with a JWT
4. The FastAPI backend:
   - Validates input with Pydantic
   - Verifies the Clerk authentication token
   - Sends a structured prompt to OpenAI
5. AI output is streamed back using **Server-Sent Events (SSE)** and rendered as formatted Markdown

---

## Tech Stack

### Frontend
- **Next.js** (Pages Router)
- **TypeScript**
- **Tailwind CSS**
- **React Markdown**
- **react-datepicker**

### Authentication & Access Control
- **Clerk**
  - Secure authentication
  - Protected routes
  - Subscription gating (`Protect`, `PricingTable`)

### Backend
- **FastAPI** (Python)
- **Pydantic** for request validation
- **JWT verification** via Clerk
- **OpenAI API** with streaming responses

### Streaming
- **Server-Sent Events (SSE)**
- `@microsoft/fetch-event-source`

---

## Local Setup

### 1) Install dependencies

```bash
npm install
````

### 2) Run the development server

```bash
npm run dev
```

Visit: [http://localhost:3000](http://localhost:3000)

### 3) Production build check

```bash
npm run build
```

---

## Environment Variables

Create a `.env.local` file at the project root.
**Do not commit this file.**

```env
# Clerk
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=YOUR_VALUE_HERE
CLERK_SECRET_KEY=YOUR_VALUE_HERE
CLERK_JWKS_URL=YOUR_VALUE_HERE

# OpenAI
OPENAI_API_KEY=YOUR_VALUE_HERE
```

---

## Deployment (Vercel)

Deploy the application using the Vercel CLI:

```bash
vercel --prod
```

Ensure the same environment variables are configured in the Vercel dashboard.

---

## Example Consultation Input

**Patient Name:** Jane Smith
**Date:** Today
**Notes:**
Patient presents with persistent cough for 2 weeks. No fever.
Chest clear on examination. Blood pressure 120/80.
Likely viral bronchitis. Prescribed rest and fluids.
Follow up if symptoms persist beyond another week.

---

## Example Output

* **Summary:** Structured visit summary for medical records
* **Next steps:** Follow-up guidance and safety-netting
* **Patient email:** Clear, friendly explanation and instructions

---

## Security Notes

* No consultation data is stored by default
* Authentication is required for all API requests
* This project does **not** implement HIPAA/GDPR compliance features
* Additional measures would be required for real healthcare use:

  * Encryption at rest
  * Audit logging
  * Role-based access control
  * Patient consent management
  * Data retention policies

---

## Troubleshooting

### Build error: invalid UTF-8 sequence

* Ensure files are saved as **UTF-8**
* Avoid special characters like `•` in source code
* Prefer ASCII separators such as `|` or `-`

### Streaming issues

* Confirm the API endpoint uses `POST`
* Ensure the Authorization header includes a valid Clerk JWT
* Check that SSE is not blocked by the browser or proxy

---

## Previous Documentation

If this repository previously contained a different project or iteration, see
`README-ARCHIVE.md` for the archived documentation.

---

## License

MIT License

```

