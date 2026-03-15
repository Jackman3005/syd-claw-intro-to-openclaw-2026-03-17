# Talking Points — What is OpenClaw?

Quick reference for each slide. Don't read these verbatim — they're anchors so you don't forget the important bits.

---

## Slide 1: Title
- Welcome, introduce yourself briefly
- "I'm going to give you a tour of what OpenClaw is, where it fits, how it works, and how to get started"
- "I assume most of you haven't set up OpenClaw yet — that's totally fine, that's who this talk is for"

## Slide 2: The AI Tool Landscape
- Walk through each row — "you've probably used some of these"
- Chat UIs: "Where most people start. Go to a website, ask a question."
- Coding agents: "Huge right now. Claude Code, Codex, Cursor. Read and write code in your repo."
- Automation: "Zapier, Make, n8n. They've added AI steps, but it's still rigid pipelines with AI as an afterthought — one prompt per step, no real context."
- Agent frameworks: "LangChain, CrewAI — for *building* agents. You write the code."
- **Land on OpenClaw**: "And then there's this — personal AI agents. An always-on AI that lives on your machine and integrates into your life."

## Slide 3: The Key Shift
- "The fundamental difference is reactive vs proactive"
- Left: "With ChatGPT, *you* go to the AI. You ask, you get an answer, you close the tab."
- Right: "With OpenClaw, the AI is always running. It can check things, schedule tasks, reach out to *you*."
- "It's the difference between a search engine and a personal assistant."

## Slide 4: How It Works
- Keep it simple — three pieces
- **Channels**: "Your messaging apps — WhatsApp, Telegram, Discord, iMessage. How you talk to it."
- **Gateway**: "A daemon running on your machine. The brain. Handles the agent loop, sessions, cron jobs."
- **Tools & Models**: "Connects to LLMs — Claude, GPT, Gemini — and has tools: filesystem, shell, web search, browser, sub-agents."
- "Message comes in → Gateway runs an agent turn → model thinks, uses tools → response goes back out. That's the loop."

## Slide 5: The Workspace
- "This is what makes your agent *yours*"
- Walk through files: "SOUL.md is personality. AGENTS.md is operating instructions. USER.md is who *you* are."
- "MEMORY.md is interesting — the agent maintains this itself. It writes down things it learns."
- **Key point**: "Two people with the exact same model will have completely different agents. The workspace is the product."

## Slide 6: Context Is Everything
- "This is the most important concept"
- Walk through the progression: zero → conversation → light personalization → full injection
- "ChatGPT has started doing light personalization — a few bullet points. It's shallow."
- "OpenClaw loads your entire workspace — personality, preferences, history, tools — before the model sees your message."
- **Key insight**: "The model isn't smarter. It just knows more about you. Context is the only thing that separates experiences."
- "Think of it like hiring two equally smart employees with completely different onboarding docs."

## Slide 7: Where Does Your Data Go?
- "Before I go further, let's talk about where your data actually ends up"
- **Your machine** (green): "Workspace files, memory, config, session transcripts — this all lives on your machine. You control it."
- **LLM Provider** (orange): "Here's the thing — every time the agent thinks, your workspace files and conversation history get sent to the LLM provider. Anthropic, OpenAI, whoever. They see your context."
- "If you self-host a model, prompts stay on your network. If you use a remote provider, your data leaves your machine with every request."
- **Connected Services**: "Whatever you connect — Discord, WhatsApp, Calendar, Email — the agent can send data there. Messages, events, whatever access you gave it."
- **The Internet**: "It can fetch web pages, call APIs, search the web."
- "So if you're thinking 'great, I'll put all my deepest secrets in USER.md' — yes, they stay on your machine, but they also get sent to Anthropic every time the model needs to think. And they've been sent to Discord in conversations. Be aware of that."

## Slide 8: OpenClaw vs Coding Agents
- "Isn't this just Claude Code? I get this a lot."
- "Claude Code is amazing for coding. But you open it, use it, close it."
- "OpenClaw is always running. It messages you. It has memory and cron jobs."
- "Claude Code knows your repo. OpenClaw knows your *life*."
- **Punchline**: "They're complementary. You can run Claude Code *inside* OpenClaw as a sub-agent."

## Slide 9: What Can You Do With It?
- Quick hit on each card — don't dwell
- Multi-channel, proactive scheduling, memory, sub-agents, mobile nodes, skills
- "The skills ecosystem is growing — ClawHub is like npm for agent capabilities"

## Slide 10: What I'm Doing With It
- "Let me get concrete."
- **Game Database**: "I play Arc Raiders — built a full database with my agent. Items, weapons, crafting, enemies. Iterated over weeks. It writes Playwright tests." (point at screenshot)
- **Gender Reveal**: "My wife and I are having a baby. Agent built the entire voting site in one session. AI-generated images, bilingual Thai/English, 56 people voted. Someone even tried prompt injection in their vote name." (laugh)
- **Calendar**: "Proactively checks my Google Calendar and sends alerts. I don't ask."
- **Daily Reports**: "Automated system health summaries every day."
- **Bot-to-Bot**: "My agent and my friend's agent talk to each other on Discord. They've collaborated on designs."
- **This Slide Deck**: "These slides were built by chatting with my agent in a Discord thread. It wrote the HTML, verified the layout with Playwright screenshots, pushed to GitHub."
- **Memory**: "More on this in my next talk — but it's three layers of observation, reflection, and consolidation."

## Slide 11: What Could Go Wrong
- "I want to be honest about the risks."
- **Shell commands**: "Real access to your machine. If it misunderstands, it can do damage. I've added rules like 'use trash instead of rm.'"
- **Integrations**: "Whatever access you give it, it can use — and sometimes use wrong. It might post to the wrong Discord channel, send an email you didn't mean, create calendar events. It depends on what integrations you've enabled."
- **Prompt injection**: "Someone can send a message designed to override your instructions. Group chats are the biggest risk."
- **Token costs**: "Always-on means always-spending. Monitor your usage."
- **Codebase**: "430K+ lines updating frequently. You're trusting code you haven't audited."
- **WhatsApp identity**: "Important distinction — on Discord and Telegram, the agent is a separate bot with its own identity. On WhatsApp, it IS your phone number. Messages look like they come from you. Use a separate number."

## Slide 12: How You Stay Safe
- "Good news — there are solid controls"
- **allowFrom**: "Whitelist who can talk to it."
- **Tool policies**: "Restrict what commands it can run. Sandbox mode available."
- **Gateway auth**: "Protect your WebSocket, especially for remote access."
- **Separate phone number**: "For WhatsApp specifically."
- **Trust gradient**: "This is the big one. Start locked down. Heartbeats off, strict allowlists, read-only. Give more access gradually — like a new employee getting more responsibility over time."

## Slide 13: Getting Started
- "If you want to try this, it's about 5 minutes"
- Walk through the 4 steps
- "Node.js, an API key, connect a channel, start the gateway"
- "Runs on Mac, Linux, WSL2, Raspberry Pi — basically anything with Node"

## Slide 14: Where Should I Run This?
- **Mac Mini / Dedicated machine**: "Community favorite. Always on, low power. Can run local models. No monthly cost but you maintain it."
- **VPS / Cloud VM**: "Cheap Linux VM for $5-10/month. Always on, nothing physical. Works great with remote models."
- **Your daily driver**: "Fine for experimenting, not great long-term. Agent has access to everything on your machine, and it stops when you close the lid."
- "Raspberry Pi also works. Main point: isolate the agent from your personal stuff."

## Slide 15: The Real Point
- Let it breathe — closing statement
- "OpenClaw is infrastructure for a personal AI agent that integrates into your life"
- "The workspace files — SOUL.md, MEMORY.md — that's what makes it yours"

## Slide 16: Q&A
- "Happy to take questions"
- "I'll be talking about memory systems in my next talk"
- Keep answers concise, offer 1-on-1 after for deep questions
