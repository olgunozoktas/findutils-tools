# Yolobox Configurator: Generate AI Sandbox Configs in Seconds

Build .yolobox.toml configs and CLI commands for running Claude Code, Codex, and Gemini inside isolated containers. Free visual configurator.

**Read time:** 7 min | **Category:** developer

---

Yolobox is an open-source CLI that runs AI coding agents (Claude Code, OpenAI Codex, Gemini, Copilot) inside isolated Docker containers. The AI gets full sudo access, auto-approval mode, and complete freedom to install packages and write files, while your home directory stays completely inaccessible. Generate your configuration visually with the free [Yolobox Configurator](/en/tools/yolobox-configurator) instead of memorizing dozens of CLI flags.

AI coding agents work best when they can run without permission prompts. But giving an AI unrestricted access to your entire machine means one bad command like `rm -rf ~` could wipe your home directory. Yolobox solves this by mounting your project at its real path inside a container while keeping everything else sealed off. The tagline says it all: "Let your AI go full send. Your home directory stays home."

Modern AI coding agents like Claude Code, OpenAI Codex, and Google Gemini work dramatically better in "yolo mode," where they can execute commands without asking for permission on every step. But that freedom comes with real risk.

---

**[Read the full guide on FindUtils](https://findutils.com/en/guides/yolobox-ai-sandbox-configurator-guide)**


*Tags: AI Sandbox, Docker, Developer Tools, Claude Code, DevOps*
