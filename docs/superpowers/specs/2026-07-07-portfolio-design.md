# Portfolio Design Spec

## Overview

Single-page dark portfolio for Dione Bastos (Software Engineer). Built with Astro 7 + Tailwind CSS. Emphasizes system architecture thinking — the core differentiator is the System Design section with architectural diagrams.

## Sections (in order)

### 1. Hero
- Logo + tagline: "Building developer infrastructure, blockchain products and AI-powered software."
- Resume: "Software Engineer focused on backend systems, blockchain infrastructure and developer tooling. I build products that simplify complex technologies, especially around Stellar, Go and AI."
- Clean typographic layout, minimal decoration.

### 2. Stats
- Grid of numbers: 5+ Open Source Projects, Stellar Ambassador, X npm downloads, X GitHub stars, X years coding
- Each stat as a simple number + label pair.

### 3. Featured Projects (4 projects)

#### Caatinga
**Problem → Solution → Architecture → Tech → Screenshots → GitHub → Docs**
- Stack: Go, Stellar, CLI, SDK
- Status: Active
- Role: Creator

#### TrustBid
**Problem → APIs → Architecture → Flow**
- Product design case. Shows API gateway + microservices architecture.
- Role: Creator

#### Horus
**OSINT → Architecture → Tool Integration → Parallel Processing → Pedigree Blockchain**
- Stack: Solidity, Foundry
- Architecture-focused case.

#### Pedigree Blockchain
**Solidity → Foundry → Tests → Architecture → Open Source**
- Academic project. Full testing and architecture documentation.

### 4. Projects Table
Compact table: Project | Language | Status | Link

### 5. Articles
- "Lessons building a Stellar CLI"
- "How I designed a modular blockchain API"
- "Writing maintainable Go CLIs"
- "Smart Contract testing with Foundry"

### 6. Skills (grouped by domain, not logos)

| Domain | Skills |
|--------|--------|
| Backend | Go, Node.js, TypeScript |
| Blockchain | Stellar, Soroban, Solidity, Foundry |
| Infrastructure | Git, Linux, REST, Docker |
| AI | LLM Applications, Prompt Engineering, AI Agents, RAG |
| Architecture | DDD, Clean Architecture, Event Driven, API Design |

### 7. Experience Timeline

```
2024 → First blockchain project
2025 → Stellar Ambassador
   ↓
Caatinga → TrustBid → Horus
```

### 8. GitHub Activity
Contributions, streak, charts embedded from GitHub.

### 9. System Design (key differentiator)
Architectural diagrams for:
- TrustBid: API Gateway → Identity → Escrow → Payment → Audit
- Caatinga
- Horus

Shows architectural thinking process.

### 10. Contact
GitHub, LinkedIn, Email, Discord, X

## Design System

- **Theme:** Dark (OKLCH)
- **Background:** Near-black (`oklch(0.13 0.01 260)`)
- **Surface:** Dark gray (`oklch(0.18 0.01 260)`)
- **Text:** High-contrast cool white (`oklch(0.95 0.005 260)`)
- **Accent:** Blue-violet (`oklch(0.6 0.18 280)`) for links, highlights
- **Typography:** Monospace-heavy for technical feel (JetBrains Mono for code, Inter for body)
- **Font sizes:** Clamp-based responsive scale

## What to AVOID
- No progress bars (e.g. "Go 95%")
- No huge tech logo lists
- No tutorial/CRUD projects
- No certificates as main element
- No long text blocks
- Max 4-5 projects, not 10 small ones
- No side-stripe borders, gradient text, glassmorphism as default
- No eyebrow text (tiny uppercase tracked above every section)
- No numbered section markers (01/02/03)

## Tech Stack
- Astro 7
- @astrojs/tailwind
- Tailwind CSS v4 (or v3, compatible with Astro 7)
- No component framework (vanilla Astro)
- Icons: lucide (via astro-icon or inline SVG)
