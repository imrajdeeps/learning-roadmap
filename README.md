# Roadmaps

**Two people, eight weeks, one production stack — plus the interview grind and the product it's all pointing at.**

Four self-contained HTML pages. No build step, no `node_modules`, no framework to install. Open `index.html` and everything is there.

**[→ Open the shelf](https://imrajdeeps.github.io/learning-roadmap/)**

---

## What's inside

### 🛠 Aeria Stack — 8-Week Roadmap

A full-time track for **Raj** (strong JS, good React, zero backend) and **Sakshi** (strong C++, new to JS, zero backend), working the same material in sync at 40 hrs/week each. It ends in a faithful mini-version of the real Aeria architecture — three services and two frontends, wired together.

The eight weeks, in order:

| #   | Week                                               |
| --- | -------------------------------------------------- |
| 1   | Language level-set & the tooling floor             |
| 2   | React 19 + the server-state layer                  |
| 3   | The two build families: Vite SPA + Next App Router |
| 4   | NestJS core                                        |
| 5   | PostgreSQL + Hasura v2                             |
| 6   | The signature pattern: Hasura inside the service   |
| 7   | Auth end to end & the cross-cutting library        |
| 8   | Integrate, test, ship                              |

It also covers the parts nobody writes down: a **C++ → TypeScript** primer aimed squarely at Sakshi, how to actually pair without one person driving all week, **the six things that make this codebase hard**, and the traps to sidestep on the way in.

Tick items off as you go — progress is saved to **IndexedDB** and survives reloads, with a `localStorage` fallback for when the page is opened straight off disk. → [`aeriaroadmap.html`](aeriaroadmap.html)

### 📗 DSA Roadmap & Interview Handbook

**29 topics across 8 phases, zero to offer.** Every topic ships with written documentation, the questions interviewers actually ask, worked solutions, and a notes pad that saves in your browser.

Arrays and hashing → two pointers and sliding window → binary search → recursion and backtracking → linked lists, stacks, queues → trees, BSTs, heaps, tries → graphs, topological sort, shortest paths, union-find → greedy and DP → segment trees, advanced strings, advanced graphs.

Counters at the top tally topics cleared, Q&A read, problems practised, and topics you've left notes on. → [`dsa-roadmap-handbook.html`](dsa-roadmap-handbook.html)

### 💅 GlowServe — platform service prototype

A working three-role prototype: **customer**, **professional**, and **admin**, all in one app. Browse a category, pick a slot, pay, track the job live — then flip roles and watch the same booking arrive from the professional's side, or from the admin's.

Two iterations, both included:

|                                            | Screens | Design system | Notable                                                                |
| ------------------------------------------ | ------- | ------------- | ---------------------------------------------------------------------- |
| **[v2](prototype/GlowServe%20v2.dc.html)** | 17      | `nocturne`    | Live order tracking, admin overview, separate desktop & mobile layouts |
| **[v1](prototype/GlowServe.dc.html)**      | 12      | `modernist`   | The first pass at the same three-role flow                             |

---

## Running it locally

Open `index.html` in a browser. That's the whole setup — everything is relative-linked and dependency-free.

If your browser is fussy about local files, serve the folder:

```bash
python3 -m http.server 8000
# → http://localhost:8000
```

## Layout

```
index.html                    the shelf — links to all four pages
aeriaroadmap.html             8-week stack roadmap
dsa-roadmap-handbook.html     29-topic DSA handbook
prototype/
  GlowServe v2.dc.html        three-role prototype, latest
  GlowServe.dc.html           three-role prototype, first pass
  support.js                  shared runtime (React, bundled)
  _ds/                        design-system CSS + bundles per theme
.nojekyll                     keep GitHub Pages from eating _ds/
```

### Where your progress lives

Both trackers persist locally — nothing is sent anywhere, and there's no account.

| Page          | Store                                               | Key                                               |
| ------------- | --------------------------------------------------- | ------------------------------------------------- |
| Aeria roadmap | IndexedDB `aeria-roadmap` → `localStorage` fallback | `aeria_roadmap_progress_v1`                       |
| DSA handbook  | `localStorage`                                      | `dsa_roadmap_progress_v1`, `dsa_roadmap_notes_v1` |

It's per-browser, per-device. The DSA handbook can **export progress + notes as JSON** and import it back — use that to move between machines. The Aeria roadmap has a **Reset** control next to its progress bar.

### Two things to leave alone

- **`prototype/` travels as a unit.** Both `.dc.html` files load `./support.js` and their `_ds/<theme>/` folder by relative path. Flatten the folder and the prototypes render unstyled.
- **`.nojekyll` is load-bearing.** GitHub Pages runs Jekyll by default, and Jekyll silently drops anything starting with `_` — which is the entire `_ds/` tree. Delete this file and the prototypes deploy with no CSS and no bundle, while the two roadmaps still look fine. It is a genuinely confusing way to break.
