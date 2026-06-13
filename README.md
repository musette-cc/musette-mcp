<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/icon-white.svg" />
  <img src="./assets/icon-black.svg" alt="" width="72" />
</picture>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/wordmark-white.svg" />
  <img src="./assets/wordmark-black.svg" alt="Musette" width="240" />
</picture>

# Musette MCP — the AI soigneur for Claude

**The first cycling nutrition you order from inside Claude — built on your real Strava data, validated by WorldTour soigneur Ien Vitse.**

**Real premium brands — [Amacx](https://www.musette.cc) and [Maurten](https://www.musette.cc) — delivered straight to your door. No white-label, no own-brand lock-in.**

[![MCP](https://img.shields.io/badge/Model_Context_Protocol-compatible-FF4900)](https://modelcontextprotocol.io)
[![Built for Claude](https://img.shields.io/badge/Built_for-Claude-1C1C1C)](https://claude.ai)
[![Registry](https://img.shields.io/badge/MCP_Registry-cc.musette%2Fde--soigneur-1C1C1C)](https://registry.modelcontextprotocol.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-D9D9D9.svg)](./LICENSE)

[**Connect to Claude →**](#-add-to-claude-30-seconds) · [What it does](#-what-it-does) · [Works with the Strava MCP](#-the-killer-combo-strava--musette) · [Validated by Ien Vitse](#-validated-by-a-worldtour-soigneur) · [Nederlands](#-nederlands)

</div>

---

<!-- DEMO ASSET (deliverable C): replace this line with the 30s hero GIF -->
<!-- ![Ask Claude what to eat on La Marmotte → validated plan → order](./assets/demo-mcp-musette.gif) -->
> 🎬 **30-second demo:** *"Claude, analyse my last 6 weeks and tell me what to eat on La Marmotte this Saturday."* → Strava pulls your real rides → Musette returns an Ien-Vitse-validated plan → *"build my musette"* → products, price and a one-click order link. Watch it on [musette.cc/mcp](https://www.musette.cc/mcp).

---

## ⚡ Add to Claude (30 seconds)

Musette is a [Model Context Protocol](https://modelcontextprotocol.io) server. Add it as a custom connector — **no account, no login, free to use.** You only pay if you decide to order the products.

1. Open **Claude → Settings → Connectors → "Add custom connector"**
2. Name it **`Musette`** and paste this URL:

   ```
   https://mcp.musette.cc
   ```
3. Done. The Musette tools now appear in your conversation. Ask: *"Wat moet ik eten op La Marmotte?"*

> 💡 **Even stronger with Strava.** Add [Strava's own MCP connector](https://www.strava.com) too, and Claude reads your real rides — so the plan is built on your actual form, not a guess. See [the killer combo](#-the-killer-combo-strava--musette).

---

## 🚴 What it does

Claude can already estimate carbs-per-hour. The gap Musette closes is the one between *a number* and *the right products, in the right amounts, in your bidon on Saturday morning* — validated by a real sports dietitian, and orderable in one click.

| Tool | What it does |
|------|--------------|
| `bereken_voedingsplan` | The Ien-Vitse-validated plan for one ride: carbs/hour, total, hydration, a timed feeding schedule, drink/gel/bar split and safety advice. |
| `stel_musette_samen` | Turns the plan into a ready-to-go musette: concrete products + quantities from **real premium brands (Amacx & Maurten), which Musette ships directly** — plus a direct order link with the cart pre-filled. |
| `zoek_evenement` | Looks up a cycling event or sportive by name and returns date, location and distances (km + elevation) to feed into the plan. |
| `musette_info` · `ping` | What Musette is, and a connectivity check. |

**Example prompts**

```
"Strava aan Claude gekoppeld? Analyseer m'n vorm en zeg wat ik moet eten op La Marmotte."
"160 km, 3000 hoogtemeters, tempo, 25 graden — wat neem ik mee?"
"Stel m'n musette samen voor de Amstel Gold Race toertocht."
```

Each output carries the moat: the validated plan, the source references, the concrete products — and a link you click yourself. You stay in control.

---

## 🔗 The killer combo: Strava + Musette

Two connectors, one Claude conversation, zero context-switching.

```
 You (in Claude, both connectors on)
   │
   │  "What should I eat on La Marmotte based on my training?"
   ▼
 ┌─────────────┐   real rides, FTP, volume   ┌──────────────────────────────┐
 │  Strava MCP │ ──────────────────────────► │  Claude summarises your form  │
 │ (data layer)│                             └───────────────┬──────────────┘
 └─────────────┘                                             │ distance / elevation / intensity
                                                             ▼
                                          ┌──────────────────────────────────┐
                                          │  Musette MCP  (action layer)      │
                                          │   bereken_voedingsplan  → plan     │
                                          │   stel_musette_samen    → products │
                                          └───────────────┬───────────────────┘
                                                          │ pre-filled cart link
                                                          ▼
                                          musette.cc checkout  →  delivered
```

**Strava gives you the data. Musette gives you the food. Both inside Claude.**

> 🔒 **Privacy by design.** The Musette tools only take plain numbers (distance, elevation, intensity, temperature). We never touch your Strava account — that stays between you and Strava's own connector. No PII and no payment ever pass through the chat; the order link lands you on musette.cc where the proven checkout takes over.

---

## ✅ Validated by a WorldTour soigneur

Every plan this server returns is built on a carbohydrate protocol **validated by Ien Vitse** — sports dietitian (UZ Gent) and former performance nutritionist at **Jumbo-Visma (2018–2023)**.

This is the difference between a generic AI guess (which can be *wrong* — too little fuel, hyponatremia, low energy availability) and advice you can trust for your A-goal. It is the same engine that powers [musette.cc](https://www.musette.cc) — one source of truth, grounded in the Jeukendrup protocol and Ien's WorldTour practice.

More on the science and the validation: [musette.cc/ien-vitse](https://www.musette.cc/ien-vitse).

---

## 🧱 How it's built

A small, stateless [MCP](https://modelcontextprotocol.io) server on the edge — cheap to run, nothing to break.

- **Transport:** Streamable HTTP via [`mcp-lite`](https://www.npmjs.com/package/mcp-lite) (Deno/edge-native, zero-dep)
- **Runtime:** Supabase Edge Function (Deno), stateless, `verify_jwt = false`
- **Engine:** the Ien-Vitse-validated `getCarbPlan()` carb engine (Jeukendrup protocol + Ien's corrections)
- **Cart hand-off:** stateless — the order link carries only product ids + quantities (`base64url`); real prices are looked up server-side and re-validated at checkout. No PII in the chat.

The carbohydrate math is public sports science — the moat is the validation, the product catalogue and the checkout, not the formula. That's why this is open: openness *is* the authority play.

```
Claude (connector) ──Streamable HTTP──► mcp-server (Supabase Edge, mcp-lite)
                                          ├─ bereken_voedingsplan → getCarbPlan()
                                          ├─ stel_musette_samen   → assembleMusette() → /m?c=<cart>
                                          └─ zoek_evenement       → lookup-cycling-event
```

---

## 🇳🇱 Nederlands

**De eerste sportvoeding die je vanuit Claude bestelt — op je échte Strava-data, gevalideerd door WorldTour-soigneur Ien Vitse.**

Musette is een MCP-connector voor Claude. Koppel 'm (Settings → Connectors → "Add custom connector", plak de URL hierboven) en vraag in gewone taal wat je moet eten op je volgende rit of toertocht. Claude rekent het Ien-gevalideerde plan uit, stelt je musette samen met concrete producten en geeft je een bestel-link met de winkelwagen al gevuld. **Echte premiummerken — Amacx en Maurten — die wij direct leveren** (geen white-label, geen eigen-merk). **Geen account, geen inlog, gratis** — je betaalt alleen als je daadwerkelijk bestelt.

Sterker mét de Strava-connector: dan leest Claude je werkelijke ritten en wordt je plan persoonlijk in plaats van algemeen. **Strava levert je data, Musette levert je voeding — allebei in Claude.**

Stappenplan en demo: **[musette.cc/mcp](https://www.musette.cc/mcp)**

---

## 📦 Publishing & directories

This repo is the source of truth for every MCP directory listing.

- **Anthropic MCP Registry** — published from [`server.json`](./server.json) via the `mcp-publisher` CLI. The namespace `cc.musette/de-soigneur` is DNS-verified against `musette.cc` (alternatively `io.github.<org>/musette-mcp` via GitHub auth).
- Also listed on: mcp.so · Smithery · PulseMCP · Glama · [`awesome-mcp-servers`](https://github.com/punkpeye/awesome-mcp-servers).

---

## 🔗 Links

- 🌐 Website & demo — [musette.cc/mcp](https://www.musette.cc/mcp)
- 🚴 Strava + Claude explained — [musette.cc/strava-mcp-claude](https://www.musette.cc/strava-mcp-claude)
- 🥤 Shop — [musette.cc](https://www.musette.cc)
- 🧪 The science & Ien Vitse — [musette.cc/ien-vitse](https://www.musette.cc/ien-vitse)
- 📜 [Model Context Protocol](https://modelcontextprotocol.io)

---

<div align="center">

**Musette** · Experts in fueling · Est. 2026
*Jouw rit. Jouw data. Jouw voeding.*

</div>
