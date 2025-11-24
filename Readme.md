DevChuck – Complete Concept & Architecture Document
The Open-Source Desk Companion for Developers
 Author: Kartik
 Status: Planning & Architecture Draft (v1.0)

1. What is DevChuck?
DevChuck is an open-source, physical desk companion designed for developers.
 A tiny expressive bot that sits on your desk, listens, reacts, talks, and helps you code — like an AI pair programmer with a personality.
It combines:
A small hardware unit with a face, mic, speaker, and WiFi


A local companion app that does speech-to-text, LLM inference, TTS


A powerful IDE extension that gives DevChuck deep knowledge of your codebase


LLM CLIs like Claude Code to provide high-quality, real coding intelligence


Optional cloud fallbacks for users who prefer hosted power instead of local compute


The result is:
A real-time, emotionally expressive coding partner that feels alive, helpful, and deeply aware of your work.

2. The Core Vision
Developers today have:
ChatGPT on the browser


Claude in another tab


IDE assistants inside VS Code


A lonely desk 😅


But nothing combines these worlds.
DevChuck's goal:
Bring emotional presence + dev utility + hardware charm into one cohesive experience.
It is:
Open-source hardware


Local-first for privacy


LLM-agnostic (Claude CLI, Gemini CLI, Qwen CLI, Ollama, APIs)


Customizable personality, voices, reactions


Contextual — understands your repo, logs, tasks, errors


Expressive — animated eyes, mouth-sync TTS, moods, reactions



3. Core Architecture (Three-Layer Design)
DevChuck operates as a tri-layer system, each handling distinct responsibilities.
Layer 1 — Hardware Device (The Body)
A tiny physical device with:
Small IPS/OLED display for face animations


Microphone


Speaker


Buttons/sensors (optional)


WiFi/WebSocket client


Key Role:
 Capture audio → show animations → play TTS → respond instantly.
It does not run the LLM locally.
 It’s the expressive, real-time puppet driven by the brain (Companion App).

Layer 2 — Local Companion App (The Brain)
Runs on the developer’s machine.
Responsibilities:
Speech-to-Text (STT) — Whisper.cpp or cloud


LLM inference


Text-to-Speech (TTS) — Piper/OpenVoice


Device communication (WebSockets)


Claude Code CLI execution


Routing engine for:


local LLMs (Ollama)


local CLIs (Claude Code, Gemini CLI, Qwen CLI)


cloud APIs


Security + privacy layer


User settings & preferences


Animation timing & expression generation


This app is the orchestrator.

Layer 3 — IDE Extension (The Workspace Link)
This is the newest addition — and the missing superpower.
The IDE extension (VS Code / JetBrains) provides deep access to:
Repo file tree


Open editor tabs


Error list / diagnostics


Terminal logs


Build/test outputs


Version control


Local tasks


Developer activity signals


It creates:
A context file (e.g., .devchuck/context.md) to maintain memory


A task state (like Claude Code’s workspace)


A safe command execution environment


A patch and diff preview system


This is what makes DevChuck a true dev partner and not just a “cute box that talks.”

4. Why We Use Claude Code CLI
Claude Code is the ideal coding engine for DevChuck because:
Built specifically for deep repository-level coding


Models have high reasoning & code accuracy


CLI-first design is easy to integrate with Companion App


Supports streaming for real-time answers


Works well with external context files


Provides patch creation, test-writing, file editing suggestions, etc.


The Companion App:
Calls Claude Code CLI via subprocess


Streams tokens in real time


Generates TTS and face movements as tokens arrive


Combines context from the IDE extension with user speech


Claude Code becomes the engine, DevChuck becomes the interface.

5. Real-Time Experience Design
To feel “alive”:
Instant Reaction (<100ms)
Hardware animates eyes on wakeword


Starts streaming audio immediately


Early Partial STT (<300ms)
Partial speech transcripts guide the Companion App to prep context


LLM Partial Tokens (<600ms)
Claude Code streams tokens → DevChuck animates mouth and eyes


Early TTS (<1s)
Start speaking after first few tokens


Interruptibility
If dev says “stop”:
Chuck stops speaking


Shows playful expression


Cancels underlying CLI processes


This makes the assistant feel:
responsive


conversational


emotionally present



6. Hardware Plan (Prototype Stage)
Prototype (v0.1) Components
Raspberry Pi Zero 2 W


1.3″ IPS TFT Display (ST7789)


USB Microphone


USB/3.5mm Speaker


Power supply


Breadboard + wires


What this prototype achieves
Animations


Audio capture


Audio playback


WiFi connection


Basic integration with Companion App


Future Plan — Custom PCB
After prototype success:
Design ESP32-S3-based PCB


Add built-in mic + amp + speaker driver


Simple SPI display connector


Battery options


Small footprint



7. IDE Extension — Detailed Breakdown
The extension is crucial for deep developer support.
Capabilities:
Repo Access
 Read & summarize files, code structure, dependencies.


IDE State Access
 Knows what files are open, cursor position, active error.


Terminal Access
 Reads logs, errors, outputs — without unsafe write access unless confirmed.


Build/Test Integration
 DevChuck reacts to failing builds or tests:


“Tests failed, buddy. Wanna check the traceback together?”


Project Memory File
 .devchuck/context.md stores:


ongoing tasks


project notes


problem summaries


dev preferences


Patch Engine
 Claude Code CLI produces:


diffs


code edits


new file suggestions
 Extension displays them for confirm/apply.


Voice ↔ IDE Linking
 When DevChuck hears:


 “Fix that error in utils.py”


 The extension:


fetches the specific file


sends relevant snippet to LLM


opens the file after patch applied


This makes DevChuck truly repo-aware and action-capable.

8. LLM Routing Strategy
Priority Order
Local Claude Code CLI (preferred)


Other local CLIs (Gemini CLI, Qwen CLI, etc.)


Local lightweight LLMs (Ollama)


Cloud inference (only if user opts in)


Why this approach works
Keeps project private


Provides high quality coding ability


Adaptable to low or high compute machines


Future-proof


Developer-friendly



9. DevChuck Personality Engine
DevChuck is not a robotic assistant — he’s a developer buddy.
Personality Modes:
Sarcastic → “Bro… that error? Really?”


Mentor → “Let’s break this down logically.”


Zen → “Deep breath. This bug is temporary.”


Hyper → “SHIP IT 🚀 !!!”


Emotions:
Happy


Confused


Thinking


Smug


Sleepy


Panicked (when CI fails)


Dynamic Behavior:
Smiles when tests pass


Cries when build breaks


Watches you type and comments on patterns


“High-fives” via animation when you finish a task


This personality differentiates DevChuck from purely functional AI tools.

10. Privacy & Security
Defaults:
Local-only


No automatic cloud uploads


All repo access is explicit and permissioned


Features:
Allowlist/denylist of folders


Confirmation before patch application


Tokenized communication over TLS


Local histories stored locally only



11. Monetization Model (If we Want to Build a Business)
Options:
Cloud convenience subscription


Premium voice/personality packs


Plugin marketplace


Hardware kits


Enterprise DevChuck Fleet


Sponsored integrations (GitHub, Notion, Linear)


But monetization is optional — DevChuck can also just be a beloved open-source ecosystem.

12. Roadmap (High-level)
v0.1–v0.2 (Now)
Prototype hardware


Basic display + audio


Local Companion App skeleton


v0.3
Claude Code CLI integration


Audio → STT → LLM → TTS loop


v0.4
IDE extension with context access


v0.5
Personality engine


Reaction system


Patch preview & commands


v1.0
Public open-source release


Builder community launch


DIY kits


v2.0
Custom PCB


Full ecosystem


Marketplace & cloud service



13. Final Summary
DevChuck is:
A cute desk companion


A real AI coding partner


A context-aware agent


A hardware/software hybrid


A developer engagement layer


A deeply open and community-driven project


Its power comes from three elements:
The physical presence


The local + LLM intelligence


The IDE extension that connects everything to your real code


Together, these make DevChuck not just useful — but emotionally powerful and genuinely delightful.


