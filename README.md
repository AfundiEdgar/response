# response
TECHNICAL PROJECT MANAGEMENT
SCENARIO
You've just joined Pawa IT as a Technical Product Manager for AI Solutions. As part of your onboarding, you need to review an assessment from NM. This exercise will help you understand:
1) Team Capabilities: What are the technical strengths and gaps in your engineering team?
2) Code Quality Standards: How well does the current code align with production requirements?
3) Product Development Process: How do you guide technical decisions from a product perspective?

THE ORIGINAL ASSIGNMENT
NM was asked to build an AI-powered Q&A web application using FastAPI (backend), Next.js (frontend), TailwindCSS (styling), and an LLM integration of his choice. Here is his submission: https://github.com/NMmwangemi/llm-app

INSTRUCTIONS
1. High-Level Review (GitHub Repository)
- Code Quality Score (1-10): Rate the overall code quality with brief justification
- Production Readiness (Ready/Needs Work/Not Ready): Assess if this code could be deployed to production
- Technical Strengths (2-3 points): What did NM do well technically?
- Technical Concerns (2-3 points): What are the main technical issues you identify

2. Backend Review (FastAPI):
- Code Quality: Cleanliness, documentation, organization, and adherence to coding best practices.
- Adherence to Technical Stack Requirements: Verify that the candidate has used Python with FastAPI for the backend and Next.js for the frontend, as specified.
- Technical Implementation: Assess the successful integration of Next.js, FastAPI, TailwindCSS, and the selected LLM.
- Error Handling: Are errors properly caught and returned to the frontend?

3. Product Management Perspective: Based on your review, identify at least three areas where the candidate's submission could be improved from both a technical and project management perspective. For each area:
- Technical Issue/Gap: What specifically needs to be improved?
- Product Impact: How does this affect user experience or business value?
- Implementation Approach: How would you guide the engineer to implement this?
- Priority Level: High/Medium/Low and why?

Example format:
Improvement 1: [Title]
- Technical Issue: The API lacks input validation for user queries
- Product Impact: Users could submit empty queries causing poor UX and wasted LLM tokens
- Implementation: Add Pydantic models for request validation with clear error ,z
- Priority: High - affects user experience and operational costs

4. Production Deployment Planning: Explain the following concerns based on your Product Management expertise and experiences;
- Scalability Concerns: What would happen if this application had 1000+ concurrent users?
- Cost Optimisation: How could we reduce LLM API costs while maintaining quality?
- Monitoring & Analytics: What metrics should we track for this application?

5. Developer Feedback & Mentoring: Write a brief (150-200 words) feedback message you would give to NM covering:
- What did he do well?
- Key areas for improvement (specific and actionable)
- Next steps for professional development
- How this work contributes to the broader product goals

6. Sprint Planning Scenario: You need to assign NM his next task. Based on his demonstrated capabilities in this assessment, choose the most appropriate assignment:
- Option A: Lead the development of a new chatbot feature for customer support
- Option B: Refactor and optimize the existing AIi product backend APIs
- Option C: Build a simple analytics dashboard for tracking AI conversation metrics in our AI product
- Option D: Create API integrations with third-party CRM systems

Explain Your Choice/ Justification: Explain why this task matches NM's current skill level and development needs.

SUBMISSION FORMAT
We use GitHub for submissions to keep the process streamlined and aligned with standard developer workflows. Please create your analysis and submission Markdown file (.md), as it can be rendered directly in GitHub.

You can make this repo private or public. If you want to make it private, please share this repo to oslimonk and share the link in your submission.

TO COMPLETE THE ASSESSMENT, PLEASE SUBMIT YOUR GITHUB LINK AS YOUR RESPONSE   
Link to The code repository is dead so I am unable to proceed with this assesment, however, here is how I would go about it from a high level overview:
 
1) High‑Level Review
Code Quality Score (1–10):  
Rationale: Stack choice is appropriate for an AI Q&A app. Without source access, we are working on an assumption of a basic but workble structure, typical of a first iteration, with room for testing, typing, and deployment hardening.

Production Readiness:  
Core surfaces missing in many first submissions: auth, observability, robust error handling, streaming, CI/CD, infra as code, rate limiting, token cost controls.


Clear separation of concerns between API and UI, with modern tooling (FastAPI + Next.js + Tailwind).
Simple LLM integration that is easy to iterate on (OpenAI/Anthropic/HF Inference).
Developer‑friendly local run story (uvicorn / `npm run dev`). 
Minimal validation and error normalization across API responses.
Lack of streaming (SSE/websocket) and cancellation control for long LLM calls.
Missing observability (structured logs, traces, metrics) and cost tracking for LLM usage. 

2) Backend (FastAPI) Review
 
Expected good: Pydantic models, typed routes, service/layout split (`routers/`, `services/`, `schemas/`, `core/`).  
Gaps to check: docstrings, module‑level comments, consistent typing, `settings.py` via Pydantic Settings, `httpx` with timeouts/retries, central exception handlers.

Adherence to Stack Requirements: 
Backend: Python and FastAPI  
Frontend: Next.js &TailwindCSS   
LLM: any working provider (Gemini is the assumption)

Technical Implementation
API endpoints to accept a question, optional context, and return an answer.  
Frontend chat UI with Tailwind, minimal state management.  
Optional RAG (vector DB) if implemented.

Error Handling:
Look for: a `@app.exception_handler` for `HTTPException` and generic exceptions.

Plus client‑side surfacing with toasts. 

3) Product Management Perspective — Improvements
 Improvement 1: Input validation & limit
 Improvement 2: Unified error model & retries
 Improvement 3: Streaming responses & cancel
 Improvement 4: Observability & cost telemetry
 Improvement 5: Prompt and output safeguards
 Improvement 6: CI/CD and environment parity

4) Production Deployment Planning
 Scalability (1k+ concurrent users)
 Bottlenecks: LLM latency and API concurrency.
 Cost Optimisation:
 Prompt trimming and context windows; use conversation memory sparingly.  
 Monitoring & Analytics (KPIs)
 Latency: p50/p95 end‑to‑end, LLM time, queue time.  
 Reliability: error rate by code, timeout rate, vendor failure rate.  
 Quality: answer acceptance, thumbs up/down, re‑ask rate, hallucination flags.  
 Cost: tokens in/out, $ per request/user/segment, cache hit rate.  
 Growth: DAU/WAU, session length, retention, feature usage.  
 Ops: saturation (CPU/mem), open sockets, queue depth, worker restarts

5) Developer Feedback & Mentoring (150–200 words)
The chosen stack is a modern, sensible stack and got the core loop working. The next leap is moving from demo to product. Focus on inputs, errors, and visibility. Move prompts out of code, version them, and add lightweight output validation to reduce formatting errors. On the frontend,surface error states clearly and keep the chat UI responsive while tokens stream. For growth, set up CI to run linting, type checks, and a few high‑value tests on every PR, then ship with a minimal Dockerized pipeline. As next steps, build an analytics page to track costs and user behavior, then revisit model routing to balance quality and price. This work aligns with Pawa IT’s goals: reliable AI experiences that are measurable, affordable, and easy to iterate.


6) Sprint Planning — Next Assignment
Build a simple analytics dashboard for AI conversation metrics

It exercises both sides of the stack without deep third‑party dependencies. Deliverables:  
Backend: `/metrics` service and `/admin/analytics` API returning aggregates (requests/day, p95 latency, tokens/$ per user, error buckets).  
Storage: Postgres table for request logs (id, ts, user_id, model, tokens_in/out, latency_ms, status, cached:boolean).  
Frontend: Next.js page with charts (Recharts/Chart.js), filters by date/model/user.  
Ops: Prometheus exporter and a Grafana board for ops metrics.

Success here proves ownership of reliability and cost, and sets the baseline for future feature work (chatbot improvements, RAG, rate limiting).
