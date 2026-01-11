# Market Research Agent

A Claude Code skill that produces professional-grade market research reports (15-30 pages) by orchestrating specialized sub-agents in parallel.

## What It Does

Invoke `/market-research` in Claude Code to run comprehensive market research on any topic. The agent:

1. **Scopes your research question** through conversational Q&A
2. **Dispatches 7 specialized sub-agents** in parallel waves
3. **Produces a professional report** worth $25K from a consulting firm

## Specialized Sub-Agents

| Agent | Mission |
|-------|---------|
| **Community Mapper** | Finds where your target audience hangs out online |
| **Voice Miner** | Extracts verbatim quotes, pain points, and language patterns |
| **Pricing Intel** | Researches competitive pricing and willingness-to-pay |
| **Competitor Profiler** | Deep-dives on competitor offerings and gaps |
| **Local Context** | Geography-specific factors (payments, infrastructure, culture) |
| **Trend Detector** | Search trends, momentum signals, timing analysis |
| **Opportunity Synthesizer** | Combines all findings into final report |

## Research Waves

```
Wave 1: Community Mapper + Local Context (parallel)
Wave 2: Voice Miner + Competitor Profiler + Pricing Intel (parallel)
Wave 3: Trend Detector
Wave 4: Opportunity Synthesizer → Final Report
```

## Output

- **15-30 page professional report** with executive summary, customer deep dive, competitive analysis, pricing recommendations, and go-to-market strategy
- **Raw data files** saved to project folder for reference
- **Verbatim quotes** and sources for every claim

## Installation

Copy to your Claude Code commands folder:

```bash
# Copy main skill file
cp market-research.md ~/.claude/commands/

# Copy sub-agent prompts
cp -r market-research/ ~/.claude/commands/
```

## Usage

```
/market-research
```

Then describe what you want to research. Example:

> "I want to understand the ICP for AI workshops targeting Nigeria and Ghana. What do they want from AI training, and what's their willingness to pay?"

## Project Structure

```
~/.claude/commands/
├── market-research.md              # Main orchestrator skill
└── market-research/
    ├── community-mapper.md         # Wave 1
    ├── local-context.md            # Wave 1
    ├── voice-miner.md              # Wave 2
    ├── competitor-profiler.md      # Wave 2
    ├── pricing-intel.md            # Wave 2
    ├── trend-detector.md           # Wave 3
    └── opportunity-synthesizer.md  # Wave 4
```

## Research Output Structure

```
~/research/[project-slug]/
├── brief.md              # Research question and parameters
├── reports/
│   └── YYYY-MM-DD-*.md   # Final report
├── raw/
│   ├── communities-found.md
│   ├── voice-quotes.md
│   ├── competitor-data.md
│   ├── pricing-data.md
│   ├── local-context.md
│   └── trends-data.md
└── notes.md              # Follow-up questions
```

## Requirements

- Claude Code CLI
- Web search capability enabled

## License

MIT
