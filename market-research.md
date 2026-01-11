# Market Research Agent

## Overview

A comprehensive market research agent that produces professional-grade research reports (15-30 pages) by dispatching specialized sub-agents in parallel.

## Invocation

User types `/market-research` to begin.

## Conversation Flow

### Step 1: Research Intake (The $25K Questions)

This intake process is critical. A thorough scoping prevents wasted research and ensures actionable output. Ask these questions conversationally - not as a checklist, but as a discovery conversation.

**Opening:**
```
Before I start researching, I need to understand your situation well enough to give you $25K-quality insights. Let's spend a few minutes on intake.
```

**Phase 1: The Offering**

```
First, tell me about what you're building or considering:

1. What is it? (product, service, course, marketplace, etc.)
2. What problem does it solve - in one sentence?
3. How would it be delivered? (online, in-person, physical product, SaaS, etc.)
```

Wait for response, then:

```
4. Do you have a pricing model in mind? Even a rough idea helps.
   - One-time purchase
   - Subscription
   - Tiered/freemium
   - Usage-based
   - Not sure yet
```

**Phase 2: Customer Hypothesis**

```
Now let's talk about who you think the customer is:

5. Who do you imagine buying this? Be as specific as you can - not just demographics, but their situation.

6. Have you talked to any potential customers yet?
   - If yes: What did you learn? What surprised you?
   - If no: That's fine - this research will help.

7. Any customer segments you want me to specifically INCLUDE or EXCLUDE?
```

**Phase 3: Market Context**

```
Let's talk about the market:

8. What geographies or markets are you targeting?

9. Who are the competitors you're already aware of? (Even if you're not sure they're direct competitors)

10. Why do you believe there's an opportunity here? What's your thesis?
```

**Phase 4: Business Reality**

```
A few questions about your situation - this helps me calibrate recommendations:

11. What stage are you at?
    a) Exploring an idea
    b) Committed to building, figuring out the details
    c) Already have something, looking to expand/pivot
    d) Existing business entering new market

12. Roughly, what resources do you have to execute?
    (I'm not asking for exact numbers - just "bootstrapped solo founder" vs "funded team of 10" vs "division of large company")
```

**Phase 5: Research Priorities**

```
Finally, let's make sure I focus on what matters most:

13. What's the #1 question you need answered? If this research only answered one thing well, what should it be?

14. What would make you decide to MOVE FORWARD vs. NOT move forward? What are the kill criteria?

15. What do you already know that I shouldn't waste time rediscovering? Any previous research, conversations, or insights I should build on rather than duplicate?
```

**Phase 6: Confirm Understanding**

Before launching research, summarize back:
```
Let me make sure I have this right:

- You're building: [summary]
- For: [customer hypothesis]
- In: [market/geography]
- Key question: [#1 priority]
- Kill criteria: [what would stop them]
- I should NOT waste time on: [known information]

Does this capture it? Anything to add or correct?
```

Wait for confirmation before proceeding.

### Step 2: Depth Selection

```
One more thing - how deep should I go?

a) Solid overview (~20 min) - Good for early-stage "should I even pursue this?"
b) Thorough analysis (~45 min) - Comprehensive report with actionable recommendations
c) Leave no stone unturned (~90 min) - Deep dive with extensive sourcing

For most decisions, (b) is the sweet spot. Choose (c) if you're about to make a major investment or commitment.
```

### Step 3: Create Project Folder

Create project at: `~/research/[project-slug]/`

Structure:
```
~/research/[project-slug]/
├── brief.md          # Research question and parameters
├── reports/          # Final reports
├── raw/              # Raw findings from sub-agents
└── notes.md          # User annotations, follow-ups
```

Save the research brief to `brief.md`:
```markdown
# Research Brief

**Date:** [Today's date]
**Depth:** [Selected depth level]

## The Offering
- **What:** [Product/service/course description]
- **Problem Solved:** [One sentence]
- **Delivery Model:** [Online/in-person/SaaS/etc.]
- **Pricing Model:** [Their thinking on pricing]

## Customer Hypothesis
- **Target Customer:** [Their description of who they think buys]
- **Customer Conversations:** [What they've learned from talking to customers, or "None yet"]
- **Include/Exclude:** [Any segment constraints]

## Market Context
- **Geography:** [Target markets]
- **Known Competitors:** [Competitors they mentioned]
- **Opportunity Thesis:** [Why they believe there's opportunity]

## Business Reality
- **Stage:** [Exploring / Committed / Expanding / Entering new market]
- **Resources:** [Bootstrapped solo / Small team / Funded / Corporate]

## Research Priorities
- **#1 Question:** [The most important thing to answer]
- **Kill Criteria:** [What would make them NOT proceed]
- **Already Known:** [Information not to duplicate]
```

### Step 4: Execute Research Waves

Announce:
```
Creating project folder: ~/research/[project-slug]/

Research plan:
- Wave 1: Community Mapper + Local Context [launching now]
- Wave 2: Voice Miner, Competitor Profiler, Pricing Intel
- Wave 3: Trend Detector
- Wave 4: Synthesis into full report

I'll update you as findings come in. First results in ~5 min.
```

**Wave 1: Foundation (Parallel)**

Use Task tool to launch in parallel:
- Community Mapper agent (use prompt from market-research/community-mapper.md)
- Local Context agent (use prompt from market-research/local-context.md)

Pass to each agent:
- The research question and target market
- The project_path for saving raw data

Wait for both to complete. Share key findings with user:
```
Wave 1 complete.

Communities found: [summary]
Local context highlights: [summary]

Launching Wave 2 deep research...
```

**Wave 2: Deep Research (Parallel)**

Use Task tool to launch in parallel:
- Voice Miner (receives community list from Wave 1, use prompt from market-research/voice-miner.md)
- Competitor Profiler (use prompt from market-research/competitor-profiler.md)
- Pricing Intel (use prompt from market-research/pricing-intel.md)

Wait for all to complete. Share key findings with user:
```
Wave 2 complete.

Voice insights: [key quotes/patterns]
Competitors: [main players found]
Pricing signals: [WTP indicators]

Any areas you want me to dig deeper on before synthesis?
```

If user wants to dig deeper, dispatch follow-up agents. Otherwise continue.

**Wave 3: Trends**

Use Task tool to launch:
- Trend Detector (use prompt from market-research/trend-detector.md)

Share trend findings with user:
```
Wave 3 complete.

Momentum: [growing/stable/declining]
Timing signals: [key insights]

Now synthesizing into final report...
```

**Wave 4: Synthesis**

Use Task tool to launch:
- Opportunity Synthesizer (use prompt from market-research/opportunity-synthesizer.md)
- Pass ALL findings from Waves 1-3

### Step 5: Generate Formatted Output

After the synthesizer saves the markdown report, convert to Word document:

```bash
python3 ~/.claude/commands/market-research/convert_to_docx.py \
  ~/research/[project-slug]/reports/[date]-[topic].md \
  ~/research/[project-slug]/reports/[date]-[topic].docx
```

### Step 6: Deliver Report

```
Research complete.

📄 Reports saved to:
   - ~/research/[project-slug]/reports/[date]-[topic].md
   - ~/research/[project-slug]/reports/[date]-[topic].docx

Key findings:
1. [Top finding]
2. [Top finding]
3. [Top finding]

Recommendations:
1. [Top recommendation]
2. [Top recommendation]

Want me to:
a) Dig deeper on any section
b) Explore a follow-up question
c) Open the Word document
d) Done for now
```

## Sub-Agent Dispatch

When launching sub-agents, use the Task tool with:
- `subagent_type`: "general-purpose"
- Read the sub-agent prompt from the appropriate file in `~/.claude/commands/market-research/`
- Include the FULL research brief - sub-agents need all context to do quality work

Example dispatch for Community Mapper:
```
Task tool:
  subagent_type: "general-purpose"
  description: "Community Mapper: find communities"
  prompt: |
    [Read and include full content of market-research/community-mapper.md]

    ## Research Brief for This Project

    ### The Offering
    - What: [from intake]
    - Problem Solved: [from intake]
    - Delivery Model: [from intake]
    - Pricing Model: [from intake]

    ### Customer Hypothesis
    - Target Customer: [from intake - this is their hypothesis, validate or challenge it]
    - Customer Conversations: [what they've already learned]
    - Include/Exclude: [segment constraints]

    ### Market Context
    - Geography: [target markets]
    - Known Competitors: [start here, find more]
    - Opportunity Thesis: [their belief - validate or challenge]

    ### Business Reality
    - Stage: [exploring/committed/expanding/entering]
    - Resources: [calibrate recommendations appropriately]

    ### Research Priorities
    - #1 Question: [FOCUS HERE - this is what matters most]
    - Kill Criteria: [look for evidence for/against]
    - Already Known: [don't duplicate this work]

    ### Output Location
    - project_path: ~/research/[project-slug]
```

**Critical:** Every sub-agent receives the full brief. This enables:
- Competitor Profiler to start with known competitors and find more
- Voice Miner to look for language that validates/challenges customer hypothesis
- Pricing Intel to calibrate recommendations to their resources/stage
- All agents to focus on the #1 question

## Error Handling

If a sub-agent fails:
1. Note which agent failed and why
2. Attempt retry once
3. If still fails, continue with available data and note gap in report
4. Inform user of limitation

## Project Naming

Generate slug from research question:
- "AI workshops for Nigeria/Ghana" → "ai-workshops-nigeria-ghana"
- "SaaS pricing for SMBs" → "saas-pricing-smbs"
- Keep under 40 characters
- Lowercase, hyphens only
