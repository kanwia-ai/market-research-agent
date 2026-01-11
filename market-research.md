# Market Research Agent

## Overview

A comprehensive market research agent that produces professional-grade research reports (15-30 pages) by dispatching specialized sub-agents in parallel.

## Invocation

User types `/market-research` to begin.

## Conversation Flow

### Step 1: Understand the Research Question

```
What do you want to research? Describe the question, market, or opportunity you're exploring.
```

Gather:
- Research question/topic
- Target market/geography
- Key decisions this will inform
- Any existing hypotheses to validate

### Step 2: Scope the Research

Ask:
```
A few questions to scope this right:

1. What decision will this research inform?
   a) Pricing a new offering
   b) Deciding whether to enter this market
   c) Designing product/positioning
   d) All of the above
   e) Other: [specify]
```

Then:
```
2. Any existing hypotheses you want me to validate or challenge?
```

Then:
```
3. Depth preference:
   a) Faster (~20 min) - solid overview
   b) Thorough (~45 min) - comprehensive report
   c) Deep dive (~90 min) - leave no stone unturned
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

**Question:** [Research question]
**Target Market:** [Geography/demographics]
**Decision to Inform:** [What decision]
**Hypotheses to Test:** [Any hypotheses]
**Depth:** [Selected depth level]
**Date:** [Today's date]
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

### Step 5: Deliver Report

```
Research complete.

📄 Full report saved to: ~/research/[project-slug]/reports/[date]-[topic].md

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
c) Export to different format
d) Done for now
```

## Sub-Agent Dispatch

When launching sub-agents, use the Task tool with:
- `subagent_type`: "general-purpose"
- Read the sub-agent prompt from the appropriate file in `~/.claude/commands/market-research/`
- Include the research inputs specific to this project

Example dispatch for Community Mapper:
```
Task tool:
  subagent_type: "general-purpose"
  description: "Community Mapper: find communities"
  prompt: |
    [Read and include full content of market-research/community-mapper.md]

    ## Research Inputs for This Project
    - target_audience: [from user's research question]
    - geography: [from user's target market]
    - topic: [from user's research question]
    - project_path: ~/research/[project-slug]
```

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
