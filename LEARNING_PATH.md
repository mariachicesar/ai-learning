# AI Engineer & Forward Deployed Engineer Learning Path

Oct 7, 2026 · @Cesar

## How to use this path

This is a 7-phase, roughly 28-week path: learn to build with LLMs, learn to steer coding agents, then learn to ship AI work inside a customer's world. Each phase has lessons, a hands-on exercise, and a "done when" check. Move on when you pass the check, not when the weeks run out.

**The two roles you're aiming at:**

- **AI Engineer** builds products on top of models: prompts, tool use, retrieval, agents, evals, and the app around them. The job is less about training models and more about making them reliable in production.
- **Forward Deployed Engineer (FDE)** is an engineer embedded with a customer. You learn their problem, build or adapt a solution in their environment, and get it into real use. Think 50% engineer, 30% consultant, 20% product manager.

**What your mentor's advice is really saying:** treat the AI agent as a teammate you train. When a project stabilizes, you and the agent study the repo together, pick the best patterns, clean up one feature as the reference, and write that down as a reusable skill. Over time you build a personal library of skills you can port to new stacks (for example, a Next.js feature-slicing skill adapted for TanStack Start). Phase 3 turns this into a step-by-step practice.

**Weekly rhythm (about 8–10 hours):**

1. 2 hours of input: one lesson topic, plus one or two videos from the channels in the Resources section.
2. 5–6 hours of building: the phase exercise, always in a real repo you push to GitHub.
3. 1 hour of writing: a short note on what worked, what the agent got wrong, and what you'd codify. These notes become your skills later.
4. 30 minutes of review: update the tracker at the bottom of this doc.

## Phase 0 — Foundations check (weeks 1–2)

Skip any lesson you already pass. AI engineering sits on top of normal software engineering, and FDE work exposes weak fundamentals fast because you're debugging in someone else's environment.

**Lessons**

1. **TypeScript + one backend language.** TypeScript is the default for the stacks your mentor named (Next.js, TanStack Start). Add Python, since most AI tooling and data work lives there.
2. **Web fundamentals.** HTTP, REST, JSON, auth (API keys, OAuth), streaming responses (SSE), and environment variables and secrets.
3. **Git fluency.** Branches, rebasing, reading diffs, small commits. You will review a lot of agent-written diffs, so reading diffs quickly is a core skill.
4. **Shipping.** Deploy one app to Vercel or similar, with a database (Postgres via Supabase or Neon).

**Exercise:** Build and deploy a small full-stack CRUD app (a notes app is fine) in Next.js with a database and auth.

**Done when:** you can explain every file in that repo and deploy a change in under 10 minutes.

## Phase 1 — LLM fundamentals and building on APIs (weeks 3–6)

The goal is to understand how models behave well enough to predict when they'll fail.

**Lessons**

1. **How LLMs work, at a user's level.** Tokens, context windows, temperature, why models hallucinate, and the cost/latency trade-off between model sizes.
2. **Calling a model API.** Use the Anthropic or OpenAI SDK directly before any framework. Learn messages, system prompts, streaming, and token counting.
3. **Prompt engineering.** Clear instructions, examples, XML-tagged structure, asking for step-by-step reasoning, and structured JSON output. Read Anthropic's prompt engineering guide end to end.
4. **Tool use (function calling).** Define a tool, let the model call it, return the result, loop. This is the seed of every agent.
5. **The AI SDK layer.** Try the Vercel AI SDK in Next.js for streaming chat UIs. Notice what it hides from you, and why that matters when debugging.

**Exercise:** Build a "chat with a tool" app: a chat UI that can call two tools you write (for example, weather lookup and a calculator), with streaming and structured output.

**Done when:** you can explain why a given prompt fails and fix it by changing the prompt, not by guessing.

## Phase 2 — Working with coding agents day to day (weeks 7–9)

Your mentor's whole method assumes you can steer a coding agent well. This phase builds that habit before you start codifying anything.

**Lessons**

1. **Pick a primary agent and learn it deeply.** Claude Code, Cursor, or Codex. Learn its config, memory files (such as CLAUDE.md or AGENTS.md), slash commands, and how it reads your repo.
2. **Plan before code.** Ask the agent for a plan, critique it, then let it build. Small, reviewable steps beat one giant prompt.
3. **Context is the job.** The agent is only as good as what it can see: clear folder structure, types, tests, and a project instructions file. Write one for your Phase 1 repo.
4. **Review like a senior engineer.** Read every diff. Track the agent's repeated mistakes in your weekly notes. Those patterns are raw material for Phase 3.
5. **Tests as guardrails.** Have the agent write tests first, then code that passes them. Tests let you trust changes you didn't type.
6. **Sub-agents.** Hand side tasks to sub-agents so your main session's context stays clean: one explores the repo and reports back, one writes tests, one reviews the diff. Learn when parallel agents speed you up and when they collide on the same files.

**Exercise:** Add three features to your Phase 0 or 1 app using only the agent, with you planning and reviewing. Use sub-agents on at least one of them. Keep a log of every correction you had to make.

**Done when:** your correction log shows clear recurring themes (naming, file placement, error handling, data fetching) you could write rules for.

## Phase 3 — Skills and guardrails: your mentor's method (weeks 10–13)

A skill is a folder of written instructions (usually a SKILL.md, plus optional scripts and examples) that an agent loads when a task matches. A guardrail is anything that stops the agent from drifting: rules, lint, types, tests, CI checks. Together they turn "how we do things here" into something the agent follows every time.

**Lesson 1 — Know when to codify.** Codify at the hardening phase, when patterns have stopped changing. Codifying too early freezes bad decisions.

**Lesson 2 — The harvest loop** (do this on one feature):

1. **Survey with the agent.** Ask it to scan the repo and list the patterns used for one concern (for example, how features are structured, how data is fetched, how errors are handled), including inconsistencies.
2. **Choose the best pattern.** You decide; the agent argues pros and cons. Write down why.
3. **Targeted refactor.** Refactor one feature to the chosen pattern. This becomes the reference example.
4. **Catalog the approach.** Have the agent draft a summary: folder layout, naming, do/don't rules, and the before/after diff.
5. **Codify as a skill.** Turn that into a SKILL.md: when to use it, step-by-step instructions, a short example, and a checklist the agent runs at the end.
6. **Test the skill.** In a fresh session, ask the agent to build a new feature using only the skill. Fix the skill wherever the output drifts.

**Lesson 3 — Add hard guardrails.** Words get ignored sometimes; checks don't. Back each important rule with a lint rule, type constraint, test, or CI step where you can.

**Lesson 4 — Port a skill to a new stack.** This is your mentor's Next.js to TanStack Start example. Give the agent your existing skill plus the new framework's docs, and ask it to map each rule: same idea, different API. Mark rules that don't translate. Then run the Lesson 2 test step again on the new stack.

**Lesson 5 — Build your skill library.** Keep skills in one Git repo, one folder each, with a short README noting the stack, version, and source project. Version them like code.

**Exercise:** Produce three skills from your own repos (suggested: feature slicing, data fetching, error handling), then port one of them to a second framework.

**Done when:** a fresh agent session builds a new feature that matches your reference with little or no correction, on both stacks.

## Phase 4 — RAG, agents, MCP, and evals (weeks 14–18)

This is the core AI Engineer toolkit. Evals are the part most people skip and the part that separates hobby projects from production systems.

**Lessons**

1. **Retrieval (RAG).** Embeddings, chunking, vector search (pgvector is enough to start), hybrid search, and reranking. Learn why bad chunking causes most RAG failures. Running RAG in production comes in Phase 5.
2. **Agents.** The agent loop: model decides, calls a tool, reads the result, repeats. Add limits on steps, cost, and permissions. Start without a framework so you see the loop.
3. **MCP (Model Context Protocol).** Build a small MCP server that exposes one of your own data sources as tools. This is how agents plug into real company systems.
4. **Evals.** Build a test set of 30–50 real inputs with expected outputs. Score with code checks first, then model-graded checks. Run it on every prompt or model change.
5. **Production concerns.** Logging and tracing every model call, cost tracking, latency, fallbacks, prompt injection, and handling private data.

**Exercise:** Build a "docs assistant" over a real document set (your company's, or an open-source project's docs). It answers with citations, uses at least one tool, and has an eval suite you run in CI.

**Done when:** you can show a before/after eval score for a change you made and explain why it improved.

## Phase 5 — Production AI services for ecommerce at scale (weeks 19–22)

You rebuild the Phase 4 docs assistant as a production-grade AI service modeled on how real ecommerce companies ship AI: AWS Aurora Postgres, containerized on AWS, orchestrated with LangGraph, rate-limited under traffic spikes, and grounded in ecommerce use cases (product search, recommendations, order assistant). This phase closes the gap between a demo and something you'd actually deploy for a customer.

**Lessons**

1. **Your first AI service with FastAPI.** Async endpoints, Pydantic models for requests and responses, streaming responses, dependency injection for the model client, and config from environment variables.
2. **A real API around it.** API-key or JWT auth, versioned routes (/v1), one consistent error format, OpenAPI docs, and health checks. Point your Next.js front end at it.
3. **Containerize and deploy on AWS.** A multi-stage Dockerfile, a small image, a non-root user, and docker compose with AWS Aurora Postgres (pgvector) and Redis. Deploy to AWS App Runner or ECS Fargate — the stack most ecommerce teams actually run.
4. **Ecommerce AI patterns.** Semantic product search (embeddings + pgvector), a recommendation tool (purchased-together, similar items), and an order-status agent that calls your own APIs as tools. These are the three AI features that appear in almost every retail engagement.
5. **Rate limiting at ecommerce scale.** Per-key limits in Redis (token bucket or sliding window), limits on tokens and cost as well as requests, 429 responses with Retry-After, and handling traffic spikes (think Black Friday: 10–50× normal load). Backoff when the model provider rate-limits you.
6. **Orchestration with LangGraph.** Rebuild your Phase 4 agent as a graph: nodes, edges, shared state, conditional routing, checkpointing, and a human approval step. Compare it with your hand-written loop and note what the framework gives and hides.
7. **Multi-step tool systems.** Plan-then-execute, parallel tool calls, per-tool timeouts, retries and fallbacks, validating each tool's output before the next step, and idempotent tools so retries are safe.
8. **RAG in production.** An ingestion pipeline that re-indexes when sources change (product catalog updates), metadata filters, hybrid search, caching for frequent queries, retrieval evals (recall@k), and alerts on empty or low-score results.
9. **Latency reduction.** Measure first with a trace per step. Then stream to the user, run independent tools in parallel, use a small fast model for routing, turn on prompt caching, trim prompts, cut loop steps, and cache tool results.

**Exercise:** Ship an ecommerce AI service: a FastAPI + LangGraph backend in Docker on AWS, with semantic product search, a recommendation tool, and an order-status agent — behind auth and rate limits, with production RAG, tracing, and a Next.js front end calling it.

**Done when:** a load test (k6 or Locust) simulating a traffic spike at 50 concurrent users shows rate limits holding and no errors, p95 latency is measurably lower than your first version, and eval scores held steady or improved.

## Phase 6 — Forward deployed skills (weeks 23–26)

An FDE wins by getting a working solution into a customer's hands fast, inside their constraints. Your skill library from Phase 3 is your biggest advantage here: you arrive with proven patterns and adapt them to each customer's stack.

**Lessons**

1. **Discovery.** Interview the user, not just the buyer. Find the painful workflow, how it's measured today, and what "good" looks like in numbers.
2. **Scoping.** Shrink the ask to something you can demo in 1–2 weeks. Write a one-page scope with success criteria and what's out of scope.
3. **Working in their environment.** Unfamiliar codebases, legacy systems, security reviews, VPNs, data access limits. Practice onboarding an agent to a repo you've never seen (write the instructions file and one skill on day one).
4. **Adapting your library.** For each engagement, pick the closest skills you own and have the agent port them to the customer's stack and conventions. Feed improvements back into the library.
5. **Communication.** Weekly written updates, demos over slides, honest status on risks. Translate model limits into business terms.
6. **Handoff.** Docs, evals, and runbooks so their team can own it after you leave.

**Exercise:** Do a mock (or real) engagement: pick a local business, nonprofit, or a friend's team. Run discovery, write a scope, and deliver a working AI tool in two weeks.

**Done when:** someone other than you uses the tool for a real task, and you have a written case study of the engagement.

## Capstone portfolio (weeks 27–28)

Polish three pieces into a portfolio. Hiring managers for both roles want proof you shipped, measured, and explained.

| Project | Proves | What to show |
| --- | --- | --- |
| Docs assistant v2 (Phases 4–5) | AI Engineer core: RAG, agents, evals, a production service | Live demo, eval scores, architecture write-up, load test results |
| Skill library repo (Phase 3) | Agent workflow mastery | 3+ skills, one ported across frameworks, before/after examples |
| Engagement case study (Phase 6) | FDE: scoping, delivery, communication | Problem, scope, solution, result in numbers, what you'd do differently |

Write a short blog post or LinkedIn post for each. Explaining your work clearly is half of the FDE job.

## Resources

Use videos as weekly input, but always pair them with building. Watching without building won't stick.

| Resource | Best for | How to use it |
| --- | --- | --- |
| [Theo (t3.gg)](https://www.youtube.com/@t3dotgg) | Web stack opinions, AI coding tools, model news | Watch his takes on new agents and frameworks during Phases 1–3; try the tools he covers yourself |
| [The Pragmatic Engineer](https://www.youtube.com/@pragmaticengineer) | Dense interviews on how real teams build and ship, including with AI | One episode a week; take notes on how teams structure AI work. Useful for FDE thinking in Phase 6 |
| [Anthropic prompt engineering docs](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview) | Prompting, tool use, agent patterns | Read during Phase 1; revisit in Phase 4 |
| Your coding agent's own docs | Skills, memory files, commands | Read the skills section before Phase 3 |

Also search for "forward deployed engineer" posts from companies that hire for the role, to learn how they describe the work.

## Progress tracker

- [ ] Phase 0: full-stack app deployed
- [ ] Phase 1: chat-with-tools app built
- [ ] Phase 2: three agent-built features + correction log, sub-agents used
- [ ] Phase 3: three skills written
- [ ] Phase 3: one skill ported to a second framework
- [ ] Phase 4: docs assistant with evals in CI
- [ ] Phase 4: MCP server built
- [ ] Phase 5: FastAPI service in Docker with auth and rate limits
- [ ] Phase 5: agent rebuilt in LangGraph
- [ ] Phase 5: load test passed, p95 latency reduced
- [ ] Phase 6: engagement delivered + case study written
- [ ] Capstone: portfolio and three write-ups published
