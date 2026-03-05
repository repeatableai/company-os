# Company OS™ | Intelligent Venture Engine

A single-file HTML application for AI-first venture planning. Built for Repeatable AI.

## Overview

Company OS guides users through a 6-phase workflow to create AI-first venture plans with deliverable-based org architecture.

## Phases

| Phase | Name | Description | Status |
|-------|------|-------------|--------|
| 1 | Venture Brief | Company foundation - identity, AI stack, team, moat | Live |
| 2 | Deliverable Map | Master output library by department | Live |
| 3 | AI/Human Assignment | 3-way ownership + cost delta calculation | Live |
| 4 | Org Architecture | Roles derived from deliverables + JD generation | Live |
| 5 | SOP Generator | 20 seed SOPs + custom generation | Live |
| 6 | Voice Partner | AI Voice Partner specs per role | Live |

## Tech Stack

- **Frontend**: Single HTML file with embedded CSS/JS
- **AI**: Claude API (claude-sonnet-4-5-20250514)
- **Styling**: CSS custom properties with light/dark theme
- **No build step required**

## Key Features

- **Deliverable-First Org Design**: Roles derived from deliverable clusters, not traditional org charts
- **AI/Human Cost Delta**: Real-time calculation of traditional vs AI-first staffing costs
- **3-Way Assignment**: AI-Owned, Human-Owned, or Fractional+AI per deliverable
- **JD Generation**: Claude-powered job descriptions from deliverable clusters
- **SOP Library**: 20 pre-built SOPs + custom generation
- **Voice Partner Specs**: Implementation-ready specs for AI voice integration

## State Structure

```javascript
const state = {
  theme: 'light',
  currentPage: 'p1',
  venture: {},           // Phase 1 data
  selectedDepts: Set,    // Phase 2 department selection
  deliverableMap: [],    // Phase 2 output
  phase3: null,          // Phase 3 assignment data
  phase4Roles: [],       // Phase 4 role clusters
  phase5Sops: [],        // Phase 5 SOP library
  phase6Specs: [],       // Phase 6 Voice Partner specs
  progress: 0
};
```

## Integration Notes

### For IOTD-Reskin Integration

This app is designed to be integrated into the Venture OS module:

1. **Target Route**: `/venture-os/risk-mitigation` or new `/venture-os/company-os`
2. **Data Source**: Connect to `ideas` table for venture context
3. **Pre-fill Phase 1** from idea fields:
   - `idea.title` → `venture.name`
   - `idea.type` → `venture.industry`
   - `idea.description` → `venture.value`
   - `idea.targetAudience` → `venture.customer`
   - `idea.revenuePotential` → `venture.revenue`

4. **Save Outputs**: Add `companyOsData` JSONB column to ideas table or create linked table

### API Requirements

- Anthropic API key for Claude calls
- Headers required:
  ```javascript
  {
    'x-api-key': API_KEY,
    'anthropic-version': '2023-06-01',
    'anthropic-dangerous-direct-browser-access': 'true'
  }
  ```

## Running Locally

```bash
# Start a local server (Python)
python3 -m http.server 8888

# Open in browser
open http://localhost:8888/company-os.html
```

## Demo Data

Each phase includes demo data loaders:
- Phase 1: ClearPath AI (Healthcare RCM)
- Phase 4: 18 deliverables across 7 departments
- Phase 5: 20 seed SOPs across 10 departments
- Phase 6: 3 demo roles for Voice Partner specs

---

*Built by Repeatable AI*
