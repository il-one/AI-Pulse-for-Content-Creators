# AI Interaction Specs & Prompt Prototyping

## 1. Automated Pulse Synthesis & Niche Tagging (Dashboard Feed)

### 1.1 Overview & Product Intent
* **Goal:** Deliver an instant, noise-free digest of emerging AI/tech shifts to creators the moment they open the dashboard or receive the weekly newsletter.
* **Core Job to Be Done (JTBD):** *"When new model updates or generative AI features drop, I want actionable creator-specific takeaways categorized by my discipline (Video, Copy, Design), so I can adapt my workflow without reading 20-page research papers."*
* **Trigger:** App initialization (cold start / scheduled background refresh).

---

### 1.2 Orchestration Flow

```text
┌─────────────────────────┐     ┌──────────────────────────────┐     ┌────────────────────────────┐
│   Gemini API Search     │ ──► │  Gemini API Synthesis        │ ──► │  Dashboard / Newsletter    │
│   Tool (Grounding)      │     │  & Niche Tagging Engine      │     │  Output Feed               │
└─────────────────────────┘     └──────────────────────────────┘     └────────────────────────────┘
         ▲                                     ▲                                    ▲
         │                                     │                                    │
  Crawls Tech Vectors                  Extracts Actionable                  Renders Structured
  (LLMs, Video AI, Audio,              Insights & Applies Niche             Cards & Digest
  Image Gen, Editing Tools)            Taxonomy (Video/Copy/Design)         Blocks

### 1.3 System & Production Prompt Templates

System Prompt:
