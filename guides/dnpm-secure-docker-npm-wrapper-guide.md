# dnpm: Secure Docker NPM Wrapper That Blocks Supply Chain Attacks

Generate a hardened Docker-based npm wrapper with 12 security layers. Blocks postinstall attacks, runs offline builds, drops capabilities. Free configurator.

**Read time:** 8 min | **Category:** developer

---

dnpm is a drop-in npm wrapper that runs every install, build, and dev command inside a hardened Docker container. It adds 12 security layers to your existing npm workflow without changing how you work. Configure your setup in seconds with the free [dnpm Configurator](/en/tools/dnpm-configurator) and download all files as a ZIP.

In April 2026, compromised versions of axios (1.14.1 and 0.30.4) were published to npm with a remote access trojan hidden in a postinstall script. Anyone who ran `npm install` on bare metal gave the malware full access to their filesystem, SSH keys, environment variables, and credentials. This was not the first npm supply chain attack, and it will not be the last.

dnpm exists because `npm install` should not be a security risk. Your package manager should not have unrestricted access to your entire machine.

---

**[Read the full guide on FindUtils](https://findutils.com/en/guides/dnpm-secure-docker-npm-wrapper-guide)**


*Tags: NPM Security, Docker, Supply Chain, Developer Tools, DevOps*
