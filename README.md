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
| **Opportunity Synthesizer** | Combines all findings into draft report |
| **Source Verifier** | Verifies every source and flags unsupported claims |

## Research Waves

```
Wave 1: Community Mapper + Local Context (parallel)
Wave 2: Voice Miner + Competitor Profiler + Pricing Intel (parallel)
Wave 3: Trend Detector
Wave 4: Opportunity Synthesizer → Draft Report
Wave 5: Source Verifier → Verified Final Report
```

## Output

- **Professional Word document (.docx)** - formatted with proper headings, styles, and structure
- **Markdown source (.md)** - for version control and easy editing
- **Source verification report** - every claim checked, confidence score provided
- **15-30 page report** with executive summary, customer deep dive, competitive analysis, pricing recommendations, and go-to-market strategy
- **Raw data files** saved to project folder for reference
- **Verbatim quotes** with clickable source URLs for every claim

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

> "I'm building a productivity app for freelance designers. I want to understand who would actually pay for this, what features matter most, and what the pricing should be."

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
    ├── opportunity-synthesizer.md  # Wave 4
    ├── source-verifier.md          # Wave 5
    └── convert_to_docx.py          # Report formatter
```

## Research Output Structure

```
~/research/[project-slug]/
├── brief.md                    # Research question and parameters
├── reports/
│   ├── YYYY-MM-DD-*.md         # Final report (markdown)
│   ├── YYYY-MM-DD-*.docx       # Final report (Word)
│   └── source-verification.md  # Verification report with confidence score
├── raw/
│   ├── communities-found.md
│   ├── voice-quotes.md
│   ├── competitor-data.md
│   ├── pricing-data.md
│   ├── local-context.md
│   └── trends-data.md
└── notes.md                    # Follow-up questions
```

## Requirements

- Claude Code CLI
- Web search capability enabled
- Python 3 with `python-docx` (`pip install python-docx`)

## License

MIT
