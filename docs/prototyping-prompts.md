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
```

---

### 1.3 Google AI Studio Prototyping & Prompt Iteration Cycles

This step-by-step walkthrough demonstrates how the core tracking engine was prototyped, tested, and iterated within the Google AI Studio Prompt Panel—evolving from a cold-start prompt to a production-ready, schema-enforced API prompt.

#### 🟢 Initial Base Prompt (Iteration 0 — Cold Start Prototype)
**Objective**
Test Gemini's base search capabilities and real-time retrieval across major AI ecosystems relevant to content creators.

Prompt:
> Create a dashboard that tracks the latest updates in the past 48 hrs for AI tools that can be used for content creation. Focus on the Google/Gemini ecosystem, Claude, ChatGPT, and tools like Manus, GenSpark, and other viral tools. Include links to the official announcement for each item if applicable.

**Evaluation & Limitations (Iteration 0 Output):**
- The **Refresh** button was visually difficult to locate among other page elements.
- The update feed was limited to a fixed **48-hour window**.
- Given the high velocity of AI product releases, users needed more control over how recent the displayed updates were.

#### 🟡 Iteration 1 — Minor Redesign to Refresh Updates and Filter Updates
**Product Decision & Objective**
- Improve the visibility and placement of the **Refresh** control.
- Introduce a **24-hour / 48-hour toggle** so users can switch between a more focused, recent view and a broader update window.

**Prompt Change**
> Move the Refresh button all the way to the right of the div. Add a toggle between 24 hrs and 48 hrs to display the list results accordingly. Make sure it pulls the 48 hrs news first and the toggle will act as a filter.
> Apply style changes to the selected element(s).

**Result**
- Refresh action easier to identify.
- Greater user control over update recency.
- Better alignment between the product experience and the rapidly changing AI landscape.

**Evaluation & Limitations (Iteration 1 Output):**
* Lacks relevance score.
* Fails to categorize tool updates based on type of update

#### 🟡  Iteration 2 — Redesign to Add Elements for Each Update Card
> Display these for each card:
> 
> relevance score (0-100): based on popularity, publicity, and impact.
> 
> category: Model, Feature, Funding, Viral, or Other

---

## 2. Structured Outputs & Search Grounding API Call
This configuration uses Structured Outputs and Google Search grounding to return a validated JSON array of categorized updates, pairing each entry with its source URL, relevance score, timestamp, and metadata.
```javascript
const response = await ai.models.generateContent({
  model: modelGemini, // variable for Gemini model
  contents: prompt, // const for system instructions
  config: {
    tools: [{ googleSearch: {} }],
    responseMimeType: "application/json",
    responseSchema: {
      type: Type.ARRAY,
      items: {
        type: Type.OBJECT,
        properties: {
          title: { type: Type.STRING },
          description: { type: Type.STRING },
          tool: { type: Type.STRING },
          url: { type: Type.STRING },
          score: { type: Type.INTEGER },
          timestamp: { type: Type.STRING },
          category: { 
            type: Type.STRING, 
            enum: ["Model", "Feature", "Funding", "Viral", "Other"] 
          }
        },
        required: ["title", "description", "tool", "url", "score", "category", "timestamp"],
      },
    },
  },
});
```

---

## 3. Quality Benchmarking & Evaluation Framework

Use this prompt to score and refine outputs generated by the AI model:

Act as a Senior Content Editor evaluating the content draft below.

Evaluate the draft against these 4 metrics on a scale of 1 to 5:
1. **Retention Potential**: Does it hook the reader immediately without fluff?
2. **Brand Voice Authenticity**: Does it sound human, natural, and relatable?
3. **Clarity & Conciseness**: Are sentences tight, active, and free of redundant words?
4. **Actionability**: Can the target user immediately apply the insights provided?

Output Matrix:
- **Scores**: [Score per metric + brief justification]
- **Weak Point Identification**: Identify specific sentences or sections that feel weak, robotic, or slow.
- **Revised Draft**: Provide a fully rewritten version incorporating improvements for any area scoring below 4.
