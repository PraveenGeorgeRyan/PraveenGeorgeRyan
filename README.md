# Praveen George Ryan

**Full-Stack AI Engineer** · Hyderabad, India · I go by Ryan

I build AI products, and the AI-powered tools companies run on: web and mobile front ends, the backend and data layer, and the retrieval and LLM systems on top.

I was an R&D scientist from 2019 to 2021 and have been building software since October 2021. I kept the method: treat an idea as a hypothesis, change one variable at a time, measure the result, write everything down. Agents write a lot of my code; I direct the architecture, review every change and own what ships.

**[Portfolio and case studies](https://www.praveengeorgeryan.online)** · [Résumé (PDF)](https://www.praveengeorgeryan.online/PraveenGeorgeRyan.pdf) · [LinkedIn](https://www.linkedin.com/in/praveen-george-ryan-a4598327b/) · [Email](mailto:praveengeorgeryan.info@gmail.com)

## Lab notebook

Three entries from recent projects. Most of this code is private, so project names link to case studies.

### 01 · Is keyword search enough context for a model?

[Command Hub](https://www.praveengeorgeryan.online/work/command-hub), an internal AI operations platform whose assistant answers questions about a client's history.

- **Assumption:** search the meeting transcripts by keyword, hand the shortlist to the model, and the answers will be good.
- **Test:** built keyword search first and measured it on a question spanning four months.
- **Result:** about 13 of hundreds of documents, skewed towards recent ones, with no match for the same idea in different words. Given that shortlist, a flagship test question went from 2 correct answers in 3 attempts to 0 in 5.
- **Decision:** a five-layer memory: digests, period rollups, a timeline map, two-pass retrieval and semantic search. The two-pass step is strictly additive, so it cannot make an answer worse. Semantic search has a similarity floor, because a confident wrong shortlist does more damage than an empty one.

### 02 · Do these embeddings need a vector database?

Same question in two projects. Different evidence, different answer.

- **Command Hub:** one client's whole history is tens of meetings, so scoring every one in application code is a millisecond of arithmetic. Embeddings stay in a plain `real[]` column, and the schema records that arithmetic and the row count at which to revisit it.
- **[Neshama](https://www.praveengeorgeryan.online/work/neshama):** a fixed corpus of over 1,200 stories shared by every user, which is the case a vector index is built for. Embeddings go in pgvector.

### 03 · Does the documentation describe the system that runs?

[PalAsk](https://www.praveengeorgeryan.online/work/palask), a multi-tenant platform where each creator gets an assistant grounded in their own content.

- **Assumption:** the vector layer works the way the docs say: one collection per creator, OpenAI ada-002 embeddings at 1536 dimensions.
- **Check:** followed the code instead of the docs.
- **Result:** that layer does not run. The code uses one shared collection of 4096-dimension vectors and separates tenants with a filter on `creatorId`.
- **Decision:** trace from the entry point to the call site before believing any architecture claim. Documentation describes intent; the import graph describes behaviour.

## Selected work

- **[Command Hub](https://www.praveengeorgeryan.online/work/command-hub)**: Teamwork, HubSpot and BigQuery data and meeting transcripts in one client view. Sole author of the application codebase; v1.0.0 shipped in late August 2026 and is in production use.
- **[Team Hub](https://www.praveengeorgeryan.online/work/team-hub)**: migration lead on moving a team-operations app off a vendor AI platform: MySQL to PostgreSQL, Google sign-in, Pulumi, Cloud Run. A security pass first found paths where employees could read each other's performance reviews and one-to-one notes; most are closed, with two items still open. Live in staging since August 2026; production is next.
- **[Mail Copilot](https://github.com/PraveenGeorgeRyan/mail-copilot)** (public): a mail client where the assistant operates the interface instead of chatting beside it. One shared state store keeps the AI in sync with what you see; nothing is sent without confirmation. [Live demo](https://mail-copilot-red.vercel.app) (access granted per account while Google OAuth is in testing) · [Case study](https://www.praveengeorgeryan.online/work/mail-copilot)
- **[Neshama](https://www.praveengeorgeryan.online/work/neshama)**: sole engineer on a spiritual wellness app, from React Native to the retrieval pipeline. The app holds no model-provider keys; every AI call goes through a Supabase Edge Function.
- **[PalAsk](https://www.praveengeorgeryan.online/work/palask)**: one of three contributors, on the backend, integrations and RAG pipeline. The chat endpoints take the tenant from the session cookie, not the request body.

<details>
<summary>Two more projects</summary>

- **Effling**: a React Native app for young children, on Google Play as *Effling: Tracing, Hindi & Math*. I created the Toddler and Drawing Book canvases and the Hindi and Math quizzes, improved the subject canvases, and built kid profiles and the Parent Panel: 335 of about 509 commits, July 2024 to September 2025.
- **[Chalets in Blue Mountain](https://www.praveengeorgeryan.online/work/chalets-in-blue-mountain)**: sole engineer from August 2025 to January 2026, turning a hotel-booking codebase into a chalet booking site with a per-night pricing engine and Stripe Checkout. The browser never sends a price: the server re-runs the availability checks and prices the stay itself.

</details>

## Method

- Implementation logs record every failure and why, not just what shipped. Code comments carry the measurement behind a decision.
- No usage or performance figures the code doesn't measure. PalAsk had no automated test setup, so I wrote 13 scripted manual test guides with pass, fail and blocked states instead of claiming coverage.
- In AI features I care most about latency, failure modes and what happens after a wrong answer.

<sub>TypeScript · Next.js · React Native / Expo · Node.js · Postgres · Supabase · MongoDB · pgvector / Qdrant · Claude, OpenAI and Gemini APIs · GCP · Docker</sub>

---

I take on AI integration and LLM systems, full-stack web apps, React Native mobile apps and migrations off vendor platforms. Email is quickest: [praveengeorgeryan.info@gmail.com](mailto:praveengeorgeryan.info@gmail.com) · Hyderabad, India (IST) · English, German, Hindi, Telugu
