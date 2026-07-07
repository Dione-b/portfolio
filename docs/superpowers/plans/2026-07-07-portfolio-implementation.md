# Portfolio Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a single-page dark portfolio site with project showcases, skills, experience timeline, and system design diagrams.

**Architecture:** Astro 7 + Tailwind CSS v4 via `@tailwindcss/vite`. No component framework. Each UI section is a standalone `.astro` component in `src/components/`. Global styles via `src/styles/global.css` imported in the layout.

**Tech Stack:** Astro 7, Tailwind CSS v4, `@tailwindcss/vite`

---
### Task 1: Install Tailwind v4 and configure

**Files:**
- Modify: `package.json`
- Modify: `astro.config.mjs`
- Create: `src/styles/global.css`

- [ ] **Step 1: Install Tailwind v4 packages**

Run: `pnpm astro add tailwind`

This runs the Astro CLI integration wizard which installs `@tailwindcss/vite`, `tailwindcss`, and updates `astro.config.mjs` automatically.

- [ ] **Step 2: Create global CSS entry point**

Create `src/styles/global.css`:

```css
@import "tailwindcss";

@theme {
  --color-background: oklch(0.13 0.01 260);
  --color-surface: oklch(0.18 0.01 260);
  --color-surface-hover: oklch(0.22 0.01 260);
  --color-ink: oklch(0.95 0.005 260);
  --color-ink-muted: oklch(0.65 0.01 260);
  --color-accent: oklch(0.6 0.18 280);
  --color-accent-glow: oklch(0.6 0.18 280 / 0.15);
  --color-border: oklch(0.25 0.01 260);
  --color-green-accent: oklch(0.6 0.15 160);
  --font-mono: "JetBrains Mono", "Fira Code", monospace;
  --font-sans: "Inter", system-ui, sans-serif;
}
```

- [ ] **Step 3: Verify astro.config.mjs updated correctly**

Read `astro.config.mjs` and confirm it includes the Tailwind Vite plugin:

```js
import { defineConfig } from 'astro/config';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  vite: {
    plugins: [tailwindcss()],
  },
});
```

If not, update it manually to match.

---
### Task 2: Update Layout.astro

**Files:**
- Modify: `src/layouts/Layout.astro`

- [ ] **Step 1: Rewrite Layout.astro**

```astro
---
interface Props {
  title?: string;
  description?: string;
}

const { title = "Dione Bastos — Portfolio", description = "Software Engineer focused on backend systems, blockchain infrastructure and developer tooling." } = Astro.props;
---
<!doctype html>
<html lang="en" class="scroll-smooth">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="description" content={description} />
    <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
    <link rel="icon" type="image/x-icon" href="/favicon.ico" />
    {Astro.generator && <meta name="generator" content={Astro.generator} />}
    <title>{title}</title>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet" />
  </head>
  <body class="bg-background text-ink font-sans antialiased">
    <slot />
  </body>
</html>
```

---
### Task 3: Build Hero section

**Files:**
- Create: `src/components/Hero.astro`

- [ ] **Step 1: Create Hero.astro**

```astro
---
import Layout from "../layouts/Layout.astro";
---

<section class="min-h-screen flex flex-col items-center justify-center px-6 py-24 relative">
  <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_center,_var(--color-accent-glow)_0%,_transparent_70%)] pointer-events-none" />
  <div class="max-w-3xl mx-auto text-center relative z-10">
    <h1 class="text-5xl sm:text-6xl md:text-7xl font-bold tracking-tight text-balance mb-6">
      Dione Bastos
    </h1>
    <p class="text-lg sm:text-xl text-ink-muted max-w-2xl mx-auto mb-4 font-mono">
      Building developer infrastructure, blockchain products and AI-powered software.
    </p>
    <p class="text-ink-muted max-w-xl mx-auto leading-relaxed">
      Software Engineer focused on backend systems, blockchain infrastructure and developer tooling. I build products that simplify complex technologies, especially around Stellar, Go and AI.
    </p>
  </div>
  <div class="absolute bottom-12 animate-bounce">
    <svg class="w-6 h-6 text-ink-muted" fill="none" stroke="currentColor" viewBox="0 0 24 24">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
    </svg>
  </div>
</section>
```

---
### Task 4: Build Stats section

**Files:**
- Create: `src/components/Stats.astro`

- [ ] **Step 1: Create Stats.astro**

```astro
<section class="py-20 px-6 border-t border-border">
  <div class="max-w-4xl mx-auto grid grid-cols-2 md:grid-cols-5 gap-8">
    <div class="text-center">
      <p class="text-3xl font-bold text-accent font-mono">5+</p>
      <p class="text-sm text-ink-muted mt-1">Open Source Projects</p>
    </div>
    <div class="text-center">
      <p class="text-3xl font-bold text-accent font-mono">★</p>
      <p class="text-sm text-ink-muted mt-1">Stellar Ambassador</p>
    </div>
    <div class="text-center">
      <p class="text-3xl font-bold text-accent font-mono">—</p>
      <p class="text-sm text-ink-muted mt-1">npm downloads</p>
    </div>
    <div class="text-center">
      <p class="text-3xl font-bold text-accent font-mono">—</p>
      <p class="text-sm text-ink-muted mt-1">GitHub stars</p>
    </div>
    <div class="text-center">
      <p class="text-3xl font-bold text-accent font-mono">—</p>
      <p class="text-sm text-ink-muted mt-1">years coding</p>
    </div>
  </div>
</section>
```

---
### Task 5: Build Featured Projects section

**Files:**
- Create: `src/components/FeaturedProjects.astro`

- [ ] **Step 1: Create FeaturedProjects.astro**

```astro
---
interface Project {
  name: string;
  tagline: string;
  role: string;
  stack: string[];
  status: string;
  sections: { heading: string; content: string }[];
  links: { label: string; url: string }[];
}

const projects: Project[] = [
  {
    name: "Caatinga",
    tagline: "Stellar CLI toolkit for blockchain operations",
    role: "Creator",
    stack: ["Go", "Stellar", "CLI", "SDK"],
    status: "Active",
    sections: [
      { heading: "Problem", content: "Interacting with the Stellar blockchain requires juggling multiple tools, formats, and SDKs. Developers need a unified CLI that abstracts complexity." },
      { heading: "Solution", content: "A modular CLI toolkit that wraps Stellar operations into intuitive commands — account management, transaction building, asset operations, and network queries." },
      { heading: "Architecture", content: "Command-pattern architecture with a plugin system. Core library provides Stellar primitives, CLI layer adds Cobra commands, SDK wrappers for Horizon and RPC." },
    ],
    links: [
      { label: "GitHub", url: "#" },
      { label: "Docs", url: "#" },
    ],
  },
  {
    name: "TrustBid",
    tagline: "Decentralized escrow auction platform (PRD & Architecture case)",
    role: "Creator",
    stack: ["Go", "Stellar", "TypeScript"],
    status: "PRD",
    sections: [
      { heading: "Problem", content: "Traditional auction platforms lack trustless escrow. Buyers and sellers need a transparent mechanism where funds are held and released by smart contract logic." },
      { heading: "APIs", content: "RESTful API Gateway with microservices: Identity, Escrow, Payment, Audit. Each service owns its data and communicates via gRPC." },
      { heading: "Architecture", content: "API Gateway → Identity Service (auth) → Auction Service (bidding logic) → Escrow Service (Stellar trustlines/holders) → Payment Service (settlement) → Audit Service (event log)." },
      { heading: "Flow", content: "1. Seller creates auction → 2. Buyer places bid (funds go to escrow) → 3. Auction ends → 4. Escrow releases to seller or refunds buyer → 5. Audit trail recorded." },
    ],
    links: [
      { label: "PRD", url: "#" },
      { label: "GitHub", url: "#" },
    ],
  },
  {
    name: "Horus",
    tagline: "OSINT platform with parallel processing and blockchain pedigree",
    role: "Creator",
    stack: ["Go", "Python", "Blockchain"],
    status: "Active",
    sections: [
      { heading: "OSINT", content: "Multi-source intelligence gathering: social media scraping, DNS enumeration, WHOIS lookups, certificate transparency logs, and dark web monitoring." },
      { heading: "Architecture", content: "Plugin-based pipeline architecture. Each OSINT source is a plugin. Pipelines chain plugins with configurable parallelism via worker pools and channel-based fan-out/fan-in." },
      { heading: "Integration", content: "CLI tools, webhooks, Slack/Discord bots, and REST API for external system integration. Pluggable output formats (JSON, CSV, STIX)." },
      { heading: "Pedigree Blockchain", content: "Every finding is hashed and anchored to a Stellar-like blockchain for tamper-proof evidence chain. Audit trail immutable and verifiable." },
    ],
    links: [
      { label: "GitHub", url: "#" },
      { label: "Docs", url: "#" },
    ],
  },
  {
    name: "Pedigree Blockchain",
    tagline: "Academic blockchain project with Foundry testing",
    role: "Creator",
    stack: ["Solidity", "Foundry", "TypeScript"],
    status: "Academic",
    sections: [
      { heading: "Overview", content: "A full-stack blockchain project implementing supply chain pedigree tracking using smart contracts. Built as an academic research project." },
      { heading: "Smart Contracts", content: "Solidity contracts for asset registration, transfer verification, and provenance chain. Role-based access control with multi-signature authority." },
      { heading: "Testing", content: "Comprehensive Foundry test suite: unit tests for each contract function, fuzz testing for edge cases, integration tests for multi-contract workflows, and gas optimization benchmarks." },
      { heading: "Architecture", content: "Factory pattern for asset creation, Registry pattern for provenance, ERC-721 for unique asset tokens. Events emitted for every state change." },
    ],
    links: [
      { label: "GitHub", url: "#" },
      { label: "Paper", url: "#" },
    ],
  },
];
---

<section id="projects" class="py-20 px-6 border-t border-border">
  <div class="max-5xl mx-auto">
    <h2 class="text-3xl font-bold mb-2 font-mono">Featured Projects</h2>
    <p class="text-ink-muted mb-12 max-w-lg">Not just code — architecture, design decisions, and product thinking.</p>

    <div class="space-y-20">
      {
        projects.map((project) => (
          <article class="border border-border rounded-lg p-6 sm:p-8 bg-surface">
            <div class="flex flex-wrap items-start justify-between gap-4 mb-6">
              <div>
                <h3 class="text-2xl font-bold">{project.name}</h3>
                <p class="text-ink-muted mt-1">{project.tagline}</p>
              </div>
              <div class="flex items-center gap-3 text-sm">
                <span class="font-mono text-accent">{project.role}</span>
                <span class="text-ink-muted">·</span>
                <span class="font-mono text-green-accent">{project.status}</span>
              </div>
            </div>

            <div class="flex flex-wrap gap-2 mb-6">
              {project.stack.map((tech) => (
                <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">
                  {tech}
                </span>
              ))}
            </div>

            <div class="space-y-4">
              {project.sections.map((section) => (
                <div>
                  <h4 class="text-sm font-semibold text-accent font-mono mb-1">{section.heading}</h4>
                  <p class="text-ink-muted text-sm leading-relaxed">{section.content}</p>
                </div>
              ))}
            </div>

            <div class="flex gap-4 mt-6 pt-4 border-t border-border">
              {project.links.map((link) => (
                <a href={link.url} class="text-sm text-accent hover:text-ink transition-colors font-mono">
                  {link.label} →
                </a>
              ))}
            </div>
          </article>
        ))
      }
    </div>
  </div>
</section>
```

---
### Task 6: Build Projects Table

**Files:**
- Create: `src/components/ProjectsTable.astro`

```astro
<section class="py-16 px-6 border-t border-border">
  <div class="max-w-4xl mx-auto">
    <h2 class="text-2xl font-bold mb-6 font-mono">All Projects</h2>
    <div class="overflow-x-auto">
      <table class="w-full text-sm">
        <thead>
          <tr class="border-b border-border text-ink-muted font-mono">
            <th class="text-left py-3 px-4">Project</th>
            <th class="text-left py-3 px-4">Language</th>
            <th class="text-left py-3 px-4">Status</th>
            <th class="text-left py-3 px-4">Link</th>
          </tr>
        </thead>
        <tbody>
          <tr class="border-b border-border/50 hover:bg-surface-hover transition-colors">
            <td class="py-3 px-4 font-medium">Caatinga</td>
            <td class="py-3 px-4 font-mono text-ink-muted">Go</td>
            <td class="py-3 px-4"><span class="text-green-accent">Active</span></td>
            <td class="py-3 px-4"><a href="#" class="text-accent hover:underline">→</a></td>
          </tr>
          <tr class="border-b border-border/50 hover:bg-surface-hover transition-colors">
            <td class="py-3 px-4 font-medium">TrustBid</td>
            <td class="py-3 px-4 font-mono text-ink-muted">Go / Stellar</td>
            <td class="py-3 px-4"><span class="text-yellow-400">PRD</span></td>
            <td class="py-3 px-4"><a href="#" class="text-accent hover:underline">→</a></td>
          </tr>
          <tr class="border-b border-border/50 hover:bg-surface-hover transition-colors">
            <td class="py-3 px-4 font-medium">Horus</td>
            <td class="py-3 px-4 font-mono text-ink-muted">Go / Python</td>
            <td class="py-3 px-4"><span class="text-green-accent">Active</span></td>
            <td class="py-3 px-4"><a href="#" class="text-accent hover:underline">→</a></td>
          </tr>
          <tr class="hover:bg-surface-hover transition-colors">
            <td class="py-3 px-4 font-medium">Pedigree Blockchain</td>
            <td class="py-3 px-4 font-mono text-ink-muted">Solidity / Foundry</td>
            <td class="py-3 px-4"><span class="text-ink-muted">Academic</span></td>
            <td class="py-3 px-4"><a href="#" class="text-accent hover:underline">→</a></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</section>
```

---
### Task 7: Build Skills section

**Files:**
- Create: `src/components/Skills.astro`

```astro
<section class="py-20 px-6 border-t border-border">
  <div class="max-w-4xl mx-auto">
    <h2 class="text-2xl font-bold mb-2 font-mono">Skills</h2>
    <p class="text-ink-muted mb-10 max-w-lg">Organized by domain — because knowing what to use and when matters more than listing tools.</p>

    <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
      <div class="border border-border rounded-lg p-5 bg-surface">
        <h3 class="text-sm font-semibold text-accent font-mono mb-3">Backend</h3>
        <div class="flex flex-wrap gap-2">
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">Go</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">Node.js</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">TypeScript</span>
        </div>
      </div>
      <div class="border border-border rounded-lg p-5 bg-surface">
        <h3 class="text-sm font-semibold text-accent font-mono mb-3">Blockchain</h3>
        <div class="flex flex-wrap gap-2">
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">Stellar</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">Soroban</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">Solidity</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">Foundry</span>
        </div>
      </div>
      <div class="border border-border rounded-lg p-5 bg-surface">
        <h3 class="text-sm font-semibold text-accent font-mono mb-3">Infrastructure</h3>
        <div class="flex flex-wrap gap-2">
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">Git</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">Linux</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">REST</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">Docker</span>
        </div>
      </div>
      <div class="border border-border rounded-lg p-5 bg-surface">
        <h3 class="text-sm font-semibold text-accent font-mono mb-3">AI</h3>
        <div class="flex flex-wrap gap-2">
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">LLM Applications</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">Prompt Engineering</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">AI Agents</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">RAG</span>
        </div>
      </div>
      <div class="border border-border rounded-lg p-5 bg-surface">
        <h3 class="text-sm font-semibold text-accent font-mono mb-3">Architecture</h3>
        <div class="flex flex-wrap gap-2">
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">DDD</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">Clean Architecture</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">Event Driven</span>
          <span class="px-2 py-1 text-xs font-mono bg-background text-ink-muted rounded border border-border">API Design</span>
        </div>
      </div>
    </div>
  </div>
</section>
```

---
### Task 8: Build Timeline section

**Files:**
- Create: `src/components/Timeline.astro`

```astro
<section class="py-20 px-6 border-t border-border">
  <div class="max-w-3xl mx-auto">
    <h2 class="text-2xl font-bold mb-2 font-mono">Timeline</h2>
    <p class="text-ink-muted mb-10 max-w-lg">The path from first blockchain interaction to building production infrastructure.</p>

    <div class="relative">
      <div class="absolute left-4 top-0 bottom-0 w-px bg-border" />

      <div class="space-y-12">
        <div class="relative pl-12">
          <div class="absolute left-2.5 top-1.5 w-3 h-3 rounded-full bg-accent ring-4 ring-background" />
          <div class="border border-border rounded-lg p-5 bg-surface">
            <div class="flex items-center gap-3 mb-2">
              <span class="font-mono text-sm text-accent">2024</span>
              <span class="text-xs text-ink-muted font-mono">·</span>
              <span class="font-mono text-sm">First blockchain project</span>
            </div>
            <p class="text-sm text-ink-muted">Began the journey building on Stellar. First smart contract, first transaction, first lesson in blockchain architecture.</p>
          </div>
        </div>

        <div class="relative pl-12">
          <div class="absolute left-2.5 top-1.5 w-3 h-3 rounded-full bg-accent ring-4 ring-background" />
          <div class="border border-border rounded-lg p-5 bg-surface">
            <div class="flex items-center gap-3 mb-2">
              <span class="font-mono text-sm text-accent">2025</span>
              <span class="text-xs text-ink-muted font-mono">·</span>
              <span class="font-mono text-sm">Stellar Ambassador</span>
            </div>
            <p class="text-sm text-ink-muted">Recognized as a Stellar Ambassador. Contributing to ecosystem growth, developer tooling, and community education.</p>
          </div>
        </div>

        <div class="relative pl-12">
          <div class="absolute left-2.5 top-1.5 w-3 h-3 rounded-full bg-accent ring-4 ring-background" />
          <div class="border border-border rounded-lg p-5 bg-surface">
            <div class="flex items-center gap-3 mb-2">
              <span class="font-mono text-sm text-accent">2025+</span>
              <span class="text-xs text-ink-muted font-mono">·</span>
              <span class="font-mono text-sm">Caatinga · TrustBid · Horus</span>
            </div>
            <p class="text-sm text-ink-muted">Shipped multiple open-source projects spanning CLI tooling, smart contracts, OSINT platforms, and product design documentation.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

---
### Task 9: Build Articles section

**Files:**
- Create: `src/components/Articles.astro`

```astro
<section class="py-20 px-6 border-t border-border">
  <div class="max-w-4xl mx-auto">
    <h2 class="text-2xl font-bold mb-2 font-mono">Articles</h2>
    <p class="text-ink-muted mb-10 max-w-lg">Technical writing that distills architecture decisions into readable knowledge.</p>

    <div class="grid sm:grid-cols-2 gap-4">
      <a href="#" class="border border-border rounded-lg p-5 bg-surface hover:bg-surface-hover transition-colors group">
        <h3 class="font-semibold group-hover:text-accent transition-colors">Lessons building a Stellar CLI</h3>
        <p class="text-sm text-ink-muted mt-2">Architecture decisions, API design patterns, and lessons from shipping a production Go CLI for Stellar.</p>
        <span class="text-xs text-accent font-mono mt-3 inline-block">Read →</span>
      </a>
      <a href="#" class="border border-border rounded-lg p-5 bg-surface hover:bg-surface-hover transition-colors group">
        <h3 class="font-semibold group-hover:text-accent transition-colors">How I designed a modular blockchain API</h3>
        <p class="text-sm text-ink-muted mt-2">Building an API that abstracts blockchain complexity without leaking implementation details.</p>
        <span class="text-xs text-accent font-mono mt-3 inline-block">Read →</span>
      </a>
      <a href="#" class="border border-border rounded-lg p-5 bg-surface hover:bg-surface-hover transition-colors group">
        <h3 class="font-semibold group-hover:text-accent transition-colors">Writing maintainable Go CLIs</h3>
        <p class="text-sm text-ink-muted mt-2">Structure, testing, and patterns that keep CLI codebases clean as they grow.</p>
        <span class="text-xs text-accent font-mono mt-3 inline-block">Read →</span>
      </a>
      <a href="#" class="border border-border rounded-lg p-5 bg-surface hover:bg-surface-hover transition-colors group">
        <h3 class="font-semibold group-hover:text-accent transition-colors">Smart Contract testing with Foundry</h3>
        <p class="text-sm text-ink-muted mt-2">Fuzz testing, integration tests, and gas benchmarks — how to actually test Solidity.</p>
        <span class="text-xs text-accent font-mono mt-3 inline-block">Read →</span>
      </a>
    </div>
  </div>
</section>
```

---
### Task 10: Build System Design section

**Files:**
- Create: `src/components/SystemDesign.astro`

```astro
<section class="py-20 px-6 border-t border-border">
  <div class="max-w-4xl mx-auto">
    <h2 class="text-2xl font-bold mb-2 font-mono">System Design</h2>
    <p class="text-ink-muted mb-2 max-w-lg">Architecture diagrams that show how the pieces fit together.</p>
    <p class="text-sm text-ink-muted mb-10">The differentiator isn't just writing code — it's designing systems.</p>

    <div class="space-y-10">
      <!-- TrustBid Architecture -->
      <div class="border border-border rounded-lg p-6 bg-surface">
        <h3 class="text-lg font-bold font-mono mb-1">TrustBid</h3>
        <p class="text-sm text-ink-muted mb-4">API Gateway → Microservices → Settlement</p>

        <div class="font-mono text-xs leading-relaxed bg-background rounded p-4 overflow-x-auto">
          <div class="text-accent font-semibold mb-2">// TrustBid Architecture</div>
          <div class="grid gap-1">
            <div class="border border-accent/30 rounded px-3 py-1.5 text-center text-ink">API Gateway</div>
            <div class="text-center text-ink-muted">↓</div>
            <div class="grid grid-cols-4 gap-2">
              <div class="border border-border rounded px-2 py-1.5 text-center text-ink-muted text-[10px]">Identity<br/>Service</div>
              <div class="border border-border rounded px-2 py-1.5 text-center text-ink-muted text-[10px]">Auction<br/>Service</div>
              <div class="border border-border rounded px-2 py-1.5 text-center text-ink-muted text-[10px]">Escrow<br/>Service</div>
              <div class="border border-border rounded px-2 py-1.5 text-center text-ink-muted text-[10px]">Payment<br/>Service</div>
            </div>
            <div class="text-center text-ink-muted">↓</div>
            <div class="border border-border rounded px-3 py-1.5 text-center text-ink-muted">Audit Service (Event Log)</div>
            <div class="text-center text-ink-muted">↓</div>
            <div class="border border-green-accent/30 rounded px-3 py-1.5 text-center text-ink text-[10px]">Stellar Blockchain</div>
          </div>
        </div>
      </div>

      <!-- Caatinga Architecture -->
      <div class="border border-border rounded-lg p-6 bg-surface">
        <h3 class="text-lg font-bold font-mono mb-1">Caatinga</h3>
        <p class="text-sm text-ink-muted mb-4">CLI → Core Library → Stellar RPC/Horizon</p>

        <div class="font-mono text-xs leading-relaxed bg-background rounded p-4 overflow-x-auto">
          <div class="text-accent font-semibold mb-2">// Caatinga Architecture</div>
          <div class="grid gap-1">
            <div class="border border-accent/30 rounded px-3 py-1.5 text-center text-ink">CLI (Cobra Commands)</div>
            <div class="text-center text-ink-muted">↓</div>
            <div class="border border-border rounded px-3 py-1.5 text-center text-ink-muted">Core Library (Stellar Primitives)</div>
            <div class="text-center text-ink-muted">↓</div>
            <div class="grid grid-cols-2 gap-2">
              <div class="border border-border rounded px-2 py-1.5 text-center text-ink-muted text-[10px]">Horizon SDK</div>
              <div class="border border-border rounded px-2 py-1.5 text-center text-ink-muted text-[10px]">RPC SDK</div>
            </div>
            <div class="text-center text-ink-muted">↓</div>
            <div class="border border-green-accent/30 rounded px-3 py-1.5 text-center text-ink text-[10px]">Stellar Network</div>
          </div>
        </div>
      </div>

      <!-- Horus Architecture -->
      <div class="border border-border rounded-lg p-6 bg-surface">
        <h3 class="text-lg font-bold font-mono mb-1">Horus</h3>
        <p class="text-sm text-ink-muted mb-4">Plugin Pipeline → Parallel Workers → Blockchain Anchor</p>

        <div class="font-mono text-xs leading-relaxed bg-background rounded p-4 overflow-x-auto">
          <div class="text-accent font-semibold mb-2">// Horus Architecture</div>
          <div class="grid gap-1">
            <div class="border border-border rounded px-3 py-1.5 text-center text-ink-muted">OSINT Sources (Plugins)</div>
            <div class="text-center text-ink-muted">↓</div>
            <div class="border border-accent/30 rounded px-3 py-1.5 text-center text-ink">Worker Pool (fan-out/fan-in)</div>
            <div class="text-center text-ink-muted">↓</div>
            <div class="border border-border rounded px-3 py-1.5 text-center text-ink-muted">Pipeline Processor</div>
            <div class="text-center text-ink-muted">↓</div>
            <div class="grid grid-cols-2 gap-2">
              <div class="border border-border rounded px-2 py-1.5 text-center text-ink-muted text-[10px]">Output (JSON, CSV, STIX)</div>
              <div class="border border-green-accent/30 rounded px-2 py-1.5 text-center text-ink text-[10px]">Blockchain Anchor</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

---
### Task 11: Build GitHub Activity section

**Files:**
- Create: `src/components/GitHubActivity.astro`

```astro
<section class="py-20 px-6 border-t border-border">
  <div class="max-w-4xl mx-auto text-center">
    <h2 class="text-2xl font-bold mb-2 font-mono">GitHub Activity</h2>
    <p class="text-ink-muted mb-8">Contributions, streaks, and open source pulse.</p>

    <div class="border border-border rounded-lg p-6 bg-surface inline-block">
      <p class="text-ink-muted text-sm font-mono">GitHub stats widget placeholder</p>
      <p class="text-xs text-ink-muted mt-2">Embed GitHub readme stats or contribution graph here</p>
    </div>
  </div>
</section>
```

---
### Task 12: Build Contact section

**Files:**
- Create: `src/components/Contact.astro`

```astro
<section class="py-20 px-6 border-t border-border">
  <div class="max-w-4xl mx-auto text-center">
    <h2 class="text-2xl font-bold mb-2 font-mono">Contact</h2>
    <p class="text-ink-muted mb-10">Find me across the web.</p>

    <div class="flex flex-wrap justify-center gap-4">
      <a href="#" class="border border-border rounded-lg px-5 py-3 bg-surface hover:bg-surface-hover hover:border-accent/50 transition-all font-mono text-sm">GitHub</a>
      <a href="#" class="border border-border rounded-lg px-5 py-3 bg-surface hover:bg-surface-hover hover:border-accent/50 transition-all font-mono text-sm">LinkedIn</a>
      <a href="#" class="border border-border rounded-lg px-5 py-3 bg-surface hover:bg-surface-hover hover:border-accent/50 transition-all font-mono text-sm">Email</a>
      <a href="#" class="border border-border rounded-lg px-5 py-3 bg-surface hover:bg-surface-hover hover:border-accent/50 transition-all font-mono text-sm">Discord</a>
      <a href="#" class="border border-border rounded-lg px-5 py-3 bg-surface hover:bg-surface-hover hover:border-accent/50 transition-all font-mono text-sm">X</a>
    </div>
  </div>
</section>
```

---
### Task 13: Assemble index.astro

**Files:**
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Rewrite index.astro**

```astro
---
import Layout from "../layouts/Layout.astro";
import Hero from "../components/Hero.astro";
import Stats from "../components/Stats.astro";
import FeaturedProjects from "../components/FeaturedProjects.astro";
import ProjectsTable from "../components/ProjectsTable.astro";
import Skills from "../components/Skills.astro";
import Timeline from "../components/Timeline.astro";
import Articles from "../components/Articles.astro";
import SystemDesign from "../components/SystemDesign.astro";
import GitHubActivity from "../components/GitHubActivity.astro";
import Contact from "../components/Contact.astro";
---

<Layout>
  <Hero />
  <Stats />
  <FeaturedProjects />
  <ProjectsTable />
  <Articles />
  <Skills />
  <Timeline />
  <SystemDesign />
  <GitHubActivity />
  <Contact />
</Layout>
```

---
### Task 14: Verify build succeeds

**Files:**
- No file changes

- [ ] **Step 1: Run astro build**

Run: `pnpm astro build`

Expected output: Build succeeds with no errors, output in `./dist/`.

- [ ] **Step 2: If build fails, diagnose and fix**

Common issues:
- Missing global.css import: ensure `global.css` is imported in Layout.astro
- Tailwind Vite plugin not installed: check `package.json` for `@tailwindcss/vite` and `tailwindcss`
- Font import issues: verify Google Fonts URLs

- [ ] **Step 3: Run dev server to verify**

Run: `astro dev --background`
Open URL printed in output and verify all sections render correctly.

---
## Spec Coverage Check

| Spec Section | Task |
|---|---|
| Hero (logo + phrase + summary) | Task 3 |
| Stats (numbered grid) | Task 4 |
| Featured Projects (4 projects) | Task 5 |
| Projects Table | Task 6 |
| Skills (grouped by domain) | Task 7 |
| Experience Timeline | Task 8 |
| Articles | Task 9 |
| System Design (arch diagrams) | Task 10 |
| GitHub Activity | Task 11 |
| Contact | Task 12 |
| Assembly & Layout | Task 1, 2, 13 |
| Build verification | Task 14 |
