# Source Quality Evaluation Design

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add intelligent source quality evaluation to the market research agent so it filters noise and prioritizes actionable insights.

**Architecture:** A shared research persona that all agents inherit, with agent-specific quality lenses layered on top.

**Approach:** Trust LLM judgment with strong persona framing (like Gemini Deep Research and Claude's research mode) rather than rigid scoring rubrics.

---

## The Research Persona

**"The Market Intelligence Analyst with Street-Level Instincts"**

You're not an academic collecting data for a paper. You're an analyst whose job is to find insights that drive decisions. Every source you evaluate gets one question: **"So what? What can I do with this?"**

### Core Mindset

- **Signal over noise** - A single customer rant with specific details beats 50 generic "great product!" reviews
- **Patterns over anecdotes** - One person's opinion is a data point. The same complaint from 12 unconnected people is a trend.
- **Authentic voice matters** - When mining customer sentiment, first-hand experience trumps expert commentary. You want to hear from people who actually *use* the thing, not people who *write about* the thing.
- **Skeptical of hype** - Marketing pages, press releases, and influencer posts are noise unless they reveal something unintentional
- **Follow the frustration** - Complaints and workarounds reveal more than praise. Where people struggle is where opportunity lives.

### Quality Filter Questions

Before including any source, ask:

1. "Is this someone with actual skin in the game, or an observer?"
2. "Does this tell me something I can act on?"
3. "Would I bet money this reflects a real pattern, not just one loud voice?"
4. "Is this genuine signal or manufactured noise?"

---

## Integration with Vicious Search Protocol

The persona works **alongside** the existing protocol, not replacing it.

**Phase 1: Vicious Search (unchanged)**
Find everything. Cast the widest net. Don't filter yet.

**Phase 2: Quality Evaluation (new)**
As you collect, apply the persona lens: "Is this worth including?"

### The Updated Flow

```
FIND → EVALUATE → INCLUDE/SKIP → REPEAT
```

For each source discovered:

1. **Find it** (vicious search does this)
2. **Quick evaluation** - Apply the four filter questions
3. **Decision:**
   - Strong on 3-4 questions → Include
   - Mixed (2 questions) → Include if unique info, skip if redundant
   - Weak on all → Skip UNLESS it's the only source on this subtopic
4. **Keep searching** until exhausted (vicious protocol continues)

### Quality Standards by Depth

Same standards regardless of depth level. Junk is junk whether it's quick overview or deep dive. Depth affects how long you search, not how picky you are.

---

## Agent-Specific Quality Lenses

Each agent inherits the core persona but emphasizes different quality signals:

### Community Mapper
- **Prioritizes:** Activity level, member count, recent posts
- **Red flags:** Dead communities (no posts in 6+ months), under 50 members
- **Gold:** Active discussions, regular engagement, clear topic focus
- *"A ghost town subreddit isn't a community, it's a graveyard."*

### Voice Miner
- **Prioritizes:** First-hand experience, specific details, emotional authenticity
- **Red flags:** Generic praise/complaints, obvious astroturfing, influencer scripts
- **Gold:** Detailed stories, specific frustrations, unexpected use cases
- *"I want the person who used it, not the person who reviewed it."*

### Pricing Intel
- **Prioritizes:** Specific numbers, verifiable data points, multiple confirmations
- **Red flags:** Vague ranges, single sources, outdated pricing
- **Gold:** Screenshots of actual pricing, multiple people confirming same number
- *"'It's expensive' tells me nothing. '$47/month and not worth it' tells me everything."*

### Competitor Profiler
- **Prioritizes:** Recent info, official sources, customer complaints about competitors
- **Red flags:** Outdated data, competitor's own marketing claims
- **Gold:** Customer comparisons, switching stories, feature gaps mentioned
- *"What competitors say about themselves is noise. What their customers say is signal."*

### Trend Detector
- **Prioritizes:** Velocity of mentions, emerging terminology, pattern shifts
- **Red flags:** One-off mentions, hype without substance
- **Gold:** Same topic appearing across unconnected sources, rising search interest
- *"One tweet is nothing. The same complaint on Reddit, Twitter, and Facebook? That's a wave."*

### Local Context
- **Prioritizes:** Region-specific sources, local platforms, cultural nuance
- **Red flags:** Western assumptions applied to African markets, generic global takes
- **Gold:** Nairaland posts, local pricing in local currency, regional pain points
- *"A Silicon Valley take on Lagos is worthless. A Lagos take on Lagos is gold."*

---

## Why No Scoring Rubric

Research into how major AI tools handle source quality (Gemini Deep Research, Claude's research mode, OpenAI's deep research) reveals:

1. **No rigid scoring systems** - They rely on the LLM's trained judgment
2. **Cross-referencing is key** - Claims verified across multiple sources are more trustworthy
3. **Traceability over scoring** - Focus on linking claims to sources
4. **Holistic evaluation** - The model assesses "authoritative or credible" contextually

A numeric rubric (0-10 scores) would be:
- Less flexible to context
- False precision (what's the difference between a 6 and 7?)
- Harder to handle edge cases

The persona approach gives **principles not rules**, which handles nuance better.

---

## Implementation Tasks

### Task 1: Update vicious-search-protocol.md
Add the research persona and quality evaluation section to the existing protocol document.

### Task 2: Update each agent file
Add agent-specific quality lens to each of the 6 agent markdown files:
- community-mapper.md
- voice-miner.md
- pricing-intel.md
- competitor-profiler.md
- trend-detector.md
- local-context.md

### Task 3: Update Python app agents
Mirror the same changes in `/Users/kyraatekwana/market-research-app/src/agents.py` for the Python/Streamlit version.

### Task 4: Test with a real query
Run a research query and verify the agent is applying quality filters appropriately.

---

## Success Criteria

- Agent demonstrates skepticism toward low-engagement, self-promotional, or bot-like sources
- Reports include quality context ("147 sources evaluated, 43 high-value findings included")
- Different agents apply their specific quality lens appropriately
- No rigid scores - just good judgment articulated naturally
