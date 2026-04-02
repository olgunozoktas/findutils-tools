# npm Supply Chain Attacks: How to Secure npm install With Docker Sandboxing

The axios RAT attack proved npm install is broken. Learn how Docker sandboxing with 12 security layers protects your machine from supply chain attacks.

**Read time:** 6 min | **Published:** 2026-04-01

---

In April 2026, compromised versions of axios (1.14.1 and 0.30.4) were published to the npm registry with a remote access trojan embedded in a postinstall script. Every developer who ran `npm install` gave the malware full access to their SSH keys, environment variables, AWS credentials, and entire filesystem. The attack was silent, persistent, and survived package removal.

This was not an isolated event. npm supply chain attacks have been escalating for years -- event-stream (2018), ua-parser-js (2021), colors and faker (2022), and now axios. The pattern is always the same: a trusted package gets compromised, a postinstall script runs arbitrary code, and npm provides zero isolation.

The fix is not better scanning. It is sandboxing. Run `npm install` inside a hardened Docker container so that even if malicious code executes, it cannot reach your host system. FindUtils' [dnpm Configurator](/en/tools/dnpm-configurator) generates this exact setup -- a complete Docker-based npm wrapper with 12 security layers -- for free.

---

**[Read the full post on FindUtils](https://findutils.com/en/blog/npm-supply-chain-attacks-how-to-secure-npm-install-with-docker)**


*Tags: NPM Security, Docker, Supply Chain, Developer Tools, Node.js*
