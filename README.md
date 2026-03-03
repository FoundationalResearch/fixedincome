# @foundationalresearch/fixedincome

[![npm version](https://img.shields.io/npm/v/@foundationalresearch/fixedincome.svg)](https://www.npmjs.com/package/@foundationalresearch/fixedincome)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![AI Skill](https://img.shields.io/badge/AI%20Skill-Fixed%20Income-green.svg)]()
[![Financial Analysis](https://img.shields.io/badge/Domain-Financial%20Analysis-orange.svg)]()

**Fixed income analysis skill for AI-powered financial agents.** Provides a structured 7-step methodology for analyzing bonds, yield curves, duration and convexity, credit spreads, relative value, portfolio construction, and scenario analysis.

This is a standalone agent skill -- a plain Markdown file that any LLM agent can use as instructions. It works with Claude Code, Cursor, Codex, Windsurf, and any tool that supports prompt files or system instructions.

---

## What This Skill Does

When a user asks about bonds, treasuries, interest rates, or fixed income investments, this skill guides the agent through a comprehensive, institutional-grade analysis framework:

1. **Market Environment Assessment** -- Evaluate yield curve shape and level, spread environment, rate expectations, and inflation expectations
2. **Bond Fundamentals** -- Analyze pricing (YTM, YTW, YTC, current yield, spread to benchmark), structure (coupon, maturity, call/put, covenants), and credit (rating, outlook, fundamentals, recovery)
3. **Duration and Convexity Analysis** -- Measure interest rate sensitivity using Macaulay, modified, effective, and key rate duration; assess positive/negative convexity with the price change approximation formula
4. **Relative Value Analysis** -- Compare bonds via spread analysis, spread per unit of duration, carry, roll-down return, and total return estimation across sectors
5. **Portfolio Construction** -- Build fixed income portfolios using an allocation framework table mapped to objectives (capital preservation, income generation, total return, liability matching)
6. **Risk Assessment** -- Evaluate seven key risk factors (interest rate, credit, reinvestment, liquidity, inflation, call, currency) with specific measures and mitigations
7. **Scenario Analysis** -- Model outcomes under bull flattening, bear steepening, parallel shifts, and spread widening/tightening scenarios

The skill activates when users ask about bonds, yields, duration, credit spreads, fixed income portfolios, yield curves, or interest rate risk.

---

## Yield Curve Reference Guide

The `references/yield-curve-guide.md` file provides a comprehensive reference for yield curve analysis, including:

- **Yield Curve Shapes** -- Normal, flat, inverted, and humped curves with economic interpretation
- **Key Spread Measures** -- Table covering 2y-10y, 3m-10y, 5y-30y, TED spread, IG OAS, HY OAS, and breakeven inflation with definitions and signals
- **Yield Curve Movements** -- Parallel shifts, steepening (bull/bear), flattening (bull/bear), and twist/butterfly movements with causes and positioning implications
- **Term Premium** -- Formula decomposition and the five factors that drive term premium (inflation uncertainty, supply/demand, central bank balance sheet, safe haven demand, volatility regime)
- **Yield Curve Strategies** -- Table of five strategies (bullet, barbell, ladder, roll-down, curve trade) with market views and implementation
- **Historical Yield Curve Benchmarks** -- Table of long-term averages and ranges for key metrics (2y-10y spread, 3m-10y spread, 10y Treasury, IG OAS, HY OAS, 10y breakeven)

This reference is available to the agent during analysis and ensures yield curve interpretation follows institutional best practices.

---

## Risk Assessment Framework

Every fixed income analysis produced by this skill includes a structured risk evaluation covering seven categories:

| Risk | Measure | Mitigation |
|------|---------|------------|
| Interest rate risk | Duration, key rate duration | Duration matching, hedging |
| Credit risk | Credit rating, spreads | Diversification, credit analysis |
| Reinvestment risk | Coupon rate vs market rate | Laddering, zero-coupon bonds |
| Liquidity risk | Bid-ask spread, issue size | Stick to benchmark issues |
| Inflation risk | Real yield, breakeven | TIPS, floating rate |
| Call risk | Yield to worst vs YTM | Avoid callable at premium |
| Currency risk | FX volatility | Hedging, domestic focus |

This ensures that every bond or portfolio recommendation is accompanied by a clear accounting of risks and how to manage them.

---

## Installation

```bash
npm install @foundationalresearch/fixedincome
```

The package contains the `SKILL.md` file with the complete methodology and the `references/` directory with the yield curve guide. No runtime dependencies -- this is a pure knowledge package.

---

## Usage

### Claude Code

Copy or symlink the skill into your project's Claude Code commands directory:

```bash
# Create the commands directory if it doesn't exist
mkdir -p .claude/commands

# Copy the skill file
cp node_modules/@foundationalresearch/fixedincome/SKILL.md .claude/commands/fixed-income.md
```

Then invoke it in Claude Code with `/fixed-income`.

Alternatively, reference it in your `CLAUDE.md` project instructions:

```markdown
For fixed income analysis, follow the methodology in:
node_modules/@foundationalresearch/fixedincome/SKILL.md

Yield curve reference data is available at:
node_modules/@foundationalresearch/fixedincome/references/yield-curve-guide.md
```

### Cursor

Copy the skill into your Cursor rules directory:

```bash
mkdir -p .cursor/rules
cp node_modules/@foundationalresearch/fixedincome/SKILL.md .cursor/rules/fixed-income.md
```

Cursor will automatically include it as context when relevant queries are detected.

### OpenAI Codex

Include the skill content in your Codex agent instructions:

```bash
# Add to your codex configuration
cp node_modules/@foundationalresearch/fixedincome/SKILL.md codex-instructions/fixed-income.md
```

Reference the file in your Codex agent setup so it is loaded as part of the system prompt.

### Windsurf

Add the skill to your Windsurf rules:

```bash
mkdir -p .windsurf/rules
cp node_modules/@foundationalresearch/fixedincome/SKILL.md .windsurf/rules/fixed-income.md
```

### Any LLM Agent

The `SKILL.md` file is plain Markdown. You can include it in any LLM agent's system prompt, instructions file, or context window. Just read the file and prepend it to your prompt:

```javascript
import { readFileSync } from 'fs';

const skill = readFileSync(
  'node_modules/@foundationalresearch/fixedincome/SKILL.md',
  'utf-8'
);

const yieldCurveRef = readFileSync(
  'node_modules/@foundationalresearch/fixedincome/references/yield-curve-guide.md',
  'utf-8'
);

const systemPrompt = `${skill}\n\n${yieldCurveRef}\n\nUser query: ${userQuery}`;
```

---

## Output Format

When the agent uses this skill, it produces a structured analysis containing:

1. **Market Environment Summary** -- Yield curve shape, spread levels, rate outlook
2. **Bond/Portfolio Analysis** -- Key metrics table with pricing, structure, and credit details
3. **Duration and Convexity Profile** -- Interest rate sensitivity measures
4. **Relative Value Assessment** -- Spread analysis, carry, roll-down, total return comparison
5. **Risk Factor Analysis** -- Seven-category risk table with measures and mitigations
6. **Scenario Analysis Table** -- Portfolio impact under six rate and spread scenarios
7. **Recommendations and Key Considerations** -- Actionable takeaways with risk-adjusted perspective

---

## Example Queries

This skill activates for questions like:

- "What's the current yield curve telling us about the economy?"
- "Analyze the duration risk in my bond portfolio"
- "Compare investment grade vs high yield spreads"
- "Build me a fixed income portfolio for income generation"
- "What happens to my bond holdings if rates rise 100bp?"
- "Is the 10-year Treasury fairly valued right now?"
- "Explain the difference between modified and effective duration"
- "What's the roll-down return on the 5-year part of the curve?"
- "How should I position for a bear steepening scenario?"
- "What are the risks of holding callable bonds in this rate environment?"

---

## Related Skills

Build a complete financial analysis toolkit with other `@foundationalresearch` skill packages:

| Package | Description |
|---------|-------------|
| [@foundationalresearch/creditanalysis](https://www.npmjs.com/package/@foundationalresearch/creditanalysis) | Credit analysis, rating methodology, default risk assessment |
| [@foundationalresearch/macroenvironment](https://www.npmjs.com/package/@foundationalresearch/macroenvironment) | Macro environment analysis, economic indicators, Fed policy |
| [@foundationalresearch/dcfvaluation](https://www.npmjs.com/package/@foundationalresearch/dcfvaluation) | Discounted cash flow valuation with WACC and scenario modeling |
| [@foundationalresearch/technicalanalysis](https://www.npmjs.com/package/@foundationalresearch/technicalanalysis) | Chart patterns, technical indicators, trend analysis |
| [@foundationalresearch/optionsderivatives](https://www.npmjs.com/package/@foundationalresearch/optionsderivatives) | Options pricing, Greeks, strategy evaluation, volatility trading |
| [@foundationalresearch/esgscreening](https://www.npmjs.com/package/@foundationalresearch/esgscreening) | ESG screening, sustainability frameworks, impact assessment |

---

## How It Works

This package ships a `SKILL.md` file and a `references/` directory -- structured Markdown documents with YAML frontmatter. The frontmatter declares the skill name and description. The body contains the complete methodology, decision frameworks, reference tables, and output format specification.

There is no code to execute. The skill is consumed by LLM agents as context/instructions. The agent reads the methodology and applies it when answering user questions about fixed income topics. The yield curve reference guide provides additional depth that the agent can consult for spread measures, curve strategies, and historical benchmarks.

This approach is:
- **Model-agnostic** -- works with Claude, GPT, Gemini, Llama, or any capable LLM
- **Agent-agnostic** -- works with any tool that can read a Markdown file
- **Zero dependencies** -- no runtime code, no API keys, no configuration
- **Version-controlled** -- update the methodology by bumping the package version

---

## Contributing

Contributions are welcome. If you have improvements to the fixed income analysis methodology, additional yield curve frameworks, or better risk assessment tables, please open an issue or pull request at [github.com/FoundationalResearch/fixedincome](https://github.com/FoundationalResearch/fixedincome).

---

## License

MIT -- see [LICENSE](./LICENSE) for details.
