# Talking Points — What is OpenClaw?

Quick reference for each slide. Don't read these verbatim — they're anchors for what to say.

---

## Slide 1: Title
- Welcome, introduce yourself
- "I'm going to give you a tour of what OpenClaw is, where it fits, how it works, and how to get started"
- "I assume most of you have used AI tools but maybe haven't set up OpenClaw yet — that's totally fine, that's who this talk is for"

## Slide 2: The AI Tool Landscape
- Walk through each row quickly — "you've probably used some of these"
- Chat UIs: "This is where most people start. You go to a website, ask a question."
- Coding agents: "These are huge right now — Claude Code, Codex, Cursor. They read and write code in your repo."
- Automation: "Zapier, Make, n8n — trigger-based workflows. They've bolted on AI steps now, but it's still rigid pipelines with AI as an afterthought."
- Agent frameworks: "LangChain, CrewAI — these are for *building* agents. You write the code."
- **Land on OpenClaw**: "And then there's this new category — personal AI agents. An always-on AI that lives on your machine and integrates into your life."

## Slide 3: The Key Shift
- "The fundamental difference is reactive vs proactive"
- Left side: "With ChatGPT, *you* go to the AI. You ask, you get an answer, you close the tab."
- Right side: "With OpenClaw, the AI is always running. It can check things, schedule tasks, and *reach out to you* when something matters."
- "It's the difference between a search engine and a personal assistant."

## Slide 4: How It Works
- Keep it simple — three pieces
- **Channels**: "Your messaging apps. WhatsApp, Telegram, Discord, iMessage, Slack. This is how you talk to it."
- **Gateway**: "A daemon — a background process — running on your machine. This is the brain. It handles the agent loop, sessions, cron jobs."
- **Tools & Models**: "On the other side, it connects to LLM providers — Claude, GPT, Gemini — and has access to tools: your filesystem, shell commands, web search, browser, sub-agents."
- "Message comes in from WhatsApp → Gateway runs an agent turn → model thinks, uses tools → response goes back out to WhatsApp. That's the loop."

## Slide 5: The Workspace
- "This is what makes your agent *yours*"
- Walk through the files: "SOUL.md is personality. AGENTS.md is operating instructions. USER.md is who *you* are."
- "MEMORY.md is interesting — the agent maintains this itself. It writes down things it learns about you."
- **Key point**: "Two people running the exact same model with the exact same version of OpenClaw will have *completely different* agents. Because the workspace is different. The files are different. The context is different."

## Slide 6: Context Is Everything
- "This is the most important concept to understand"
- Walk through the progression: "With zero context, you get generic answers. The model knows nothing."
- "As you chat, conversation context builds up. But it resets."
- "ChatGPT has started doing light personalization — a few bullet points about you. Claude has projects. But it's shallow."
- "OpenClaw does full context injection. Before the model sees your message, it's already loaded with your personality file, your preferences, your conversation history, your tools."
- **Key insight**: "The model isn't smarter. It just knows more about you before it starts thinking. Context is the only thing that separates your experience from someone else's with the same model."
- "Think of it like hiring two equally smart employees and giving them completely different onboarding docs."

## Slide 7: OpenClaw vs Coding Agents
- "This is a question I get a lot — isn't this just Claude Code?"
- "Claude Code is amazing for coding. But you open it, use it, close it. It lives in your terminal."
- "OpenClaw is always running. It messages you. It has memory. It has cron jobs."
- "Claude Code knows your repo. OpenClaw knows your *life*."
- **Punchline**: "They're complementary, not competing. You can literally run Claude Code *inside* OpenClaw as a sub-agent. I do this all the time."

## Slide 8: What Can You Do With It?
- Quick hit on each card — don't dwell
- Multi-channel: "Talk to it on WhatsApp from your phone, continue on Discord from desktop"
- Proactive: "It can check your calendar, monitor services, send you reminders — without you asking"
- Memory: "Remembers your preferences, past decisions, context from weeks ago"
- Sub-agents: "Spin up a coding agent for a task, a research agent for something else — orchestrate multiple workers"
- Mobile nodes: "Connect your phone as a node — agent can use your camera, get your location"
- Skills: "Modular capabilities you install from ClawHub — like npm packages but for agent skills"

## Slide 9: What I'm Doing With It
- "Let me get concrete. Here's what I'm actually using this for day to day."
- **Game Database**: "I play a game called Arc Raiders — I built a full database with my agent. Items, weapons, crafting recipes, enemies. We iterated on it over weeks. It writes Playwright tests. It's a real ongoing project." (point at screenshot)
- **Gender Reveal**: "My wife and I are having a baby — I needed a voting site for our gender reveal party. My agent built the entire thing in one session. Live voting, AI-generated images, photo gallery, bilingual Thai and English. 56 people voted. Someone even tried prompt injection in their name." (get a laugh)
- **Calendar**: "It proactively checks my Google Calendar and sends me alerts in Discord. I don't have to ask."
- **Daily Reports**: "Automated system health summaries every day."
- **Bot-to-Bot**: "This is a fun one — my agent and my friend Daniel's agent actually talk to each other on a shared Discord server. They've collaborated on system designs together."
- **This Slide Deck**: "And yes — these slides were built by chatting with my agent in a Discord thread. It wrote the HTML, took screenshots to verify the layout, pushed to GitHub."
- **Memory**: "I'll talk more about this in my next talk — but the memory system is three layers of observation, reflection, and consolidation."

## Slide 10: Getting Started
- "If you want to try this, it's about 5 minutes to get started"
- Walk through the 4 steps
- "You need Node.js, an API key from Anthropic or OpenAI or whoever you prefer"
- "openclaw setup creates your config and workspace files"
- "Connect a channel — scan a QR for WhatsApp, paste a token for Discord"
- "Start the gateway and you're live"
- "It runs on Mac, Linux, WSL2, Raspberry Pi — basically anything with Node"

## Slide 11: What Could Go Wrong
- "I want to be honest about the risks. This isn't a toy."
- **Shell commands**: "The agent has real access to your machine. If it misunderstands you, it can run destructive commands. I've had to add rules like 'use trash instead of rm' because recovery matters."
- **Messaging**: "If it's connected to your WhatsApp, it can message your contacts. Imagine the agent getting confused and sending something weird to your boss."
- **Context to LLM**: "Everything in your workspace — memory, preferences, conversation history — gets sent to the LLM provider with every request. Your personal data is leaving your machine in prompts."
- **Prompt injection**: "This is real. Someone can send your agent a message designed to override your instructions. Group chats are the biggest risk surface. I actually had someone try this at my gender reveal party."
- **Token costs**: "Always-on means always-spending. Heartbeats, cron jobs, long conversations — each one is an API call. Monitor your usage."
- **Codebase trust**: "OpenClaw is 430K+ lines of code updating frequently. You're trusting code you haven't read. This is open source, which helps, but it's still a lot of trust."

## Slide 12: How You Stay Safe
- "The good news is there are solid controls"
- **allowFrom**: "Whitelist who can talk to your agent. Never run it open to the world."
- **Tool policies**: "You can restrict what commands the agent can run. Sandbox mode is available."
- **Gateway auth**: "Protect your WebSocket endpoint, especially if you're exposing it remotely."
- **Dedicated machine**: "Don't run this on your daily driver laptop. Use a VM, a VPS, an old laptop, a Raspberry Pi. Isolate the blast radius."
- **Separate phone number**: "For WhatsApp — use a dedicated SIM. Don't link your personal WhatsApp."
- **Trust gradient**: "This is the big one. Start locked down. Heartbeats off, strict allowlists, read-only tools. Gradually give more access as you understand how the agent behaves. Think of it like giving a new employee gradually more responsibility."

## Slide 13: The Real Point
- Closing statement — let it breathe
- "OpenClaw is infrastructure for a personal AI agent that actually integrates into your life"
- "Not another chat UI. Not another coding tool. An always-on assistant."
- "The workspace files — your SOUL.md, your MEMORY.md — that's what makes it yours. The model is the engine. You're writing the onboarding docs."

## Slide 14: Q&A
- "Happy to take questions"
- "I'll be giving another talk later about the memory system — how to build long-term context that grows over time"
- Keep answers concise, offer to chat 1-on-1 after for deep questions
