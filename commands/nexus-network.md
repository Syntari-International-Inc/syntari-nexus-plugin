---
name: nexus-network
description: Search relationship network, find warm intro paths via Neptune + LeadDelta, score relationship health, enrich contacts, and draft personalized intro messages
---

# /nexus-network

Network intelligence command powered by Neptune graph paths and LeadDelta LinkedIn relationship AI.

## Usage

```
/nexus-network [target company or person]
/nexus-network score [contact_id]
/nexus-network enrich [name] [company]
/nexus-network paths [from_person_id] [to_person_id]
/nexus-network import
```

## Behavior

### Default: `/nexus-network [target]`
1. Search relationship network for the target company or person
2. Find warm intro paths (Neptune multi-hop + LeadDelta Warm Intro AI)
3. Score relationship strength across 6 dimensions
4. Draft personalized intro message for the best path
5. Show LeadDelta LinkedIn paths alongside internal graph paths

**Rule**: Always runs warm intro finder before suggesting cold outreach. If warm paths exist, cold outreach is never recommended.

### Score: `/nexus-network score [contact_id]`
Returns multi-dimensional relationship health score (0-100):
- **Recency** (30%) — Exponential decay from last interaction
- **Frequency** (20%) — 90-day rolling interaction count
- **Depth** (20%) — Meeting > call > email > LinkedIn weight
- **Mutual Connections** (12%) — Shared network density
- **Employment Overlap** (10%) — Overlapping tenures
- **Geographic Proximity** (8%) — City/region bonus

Grade: A+(85+) / A(70-85) / B(55-70) / C(40-55) / D(25-40) / F(<25)
Health: growing / stable / declining / dormant + recommended actions

### Enrich: `/nexus-network enrich [name] [company]`
1. Resolve contact identity (email → LinkedIn → phone → fuzzy)
2. Pull enriched data from LeadDelta (LinkedIn-native)
3. Update contact profile with verified fields + confidence scores
4. Returns which fields were updated and from which source

### Paths: `/nexus-network paths [from] [to]`
Find all relationship paths between any two people in the network.
Maps co-investor relationships, LP networks, board connections.
Returns edges with strength, relationship type, and overlap years.

### Import: `/nexus-network import`
Import LinkedIn connections from CSV export.
Deduplicates against existing contacts, triggers enrichment pipeline.

## MCP Tools Used

| Tool | Purpose |
|------|---------|
| `nexus_search_network` | Search people/companies (token-optimized minimal results) |
| `nexus_find_warm_intro` | Neptune + LeadDelta combined warm intro paths |
| `nexus_resolve_contact` | Identity resolution via confidence waterfall |
| `nexus_relationship_score` | 6-dimension relationship health score |
| `nexus_import_connections` | LinkedIn CSV import with dedup |
| `nexus_get_intro_paths_between` | Graph paths between any two people |
| `nexus_enrich_contact` | LeadDelta + external source enrichment |
| `leaddelta_search_connections` | Direct LinkedIn network search |
| `leaddelta_warm_intro_ai` | LeadDelta Warm Intro AI (10+ signals) |

## Examples

```
/nexus-network "Blackstone"
→ Warm intro paths to Blackstone via Neptune + LeadDelta
→ Best connector with suggested intro message

/nexus-network "Sarah Chen" "KKR"
→ Network search + relationship path + LinkedIn context

/nexus-network score contact_abc123
→ Relationship score: 72/100 (A) — stable
→ Actions: "Last touch 18 days ago — cadence is healthy"

/nexus-network enrich "John Smith" "Apollo Global"
→ Enriched: email (LeadDelta, 0.94), title (LinkedIn, 0.99)
→ 2 fields updated

/nexus-network paths person_123 person_456
→ 3 paths found (1-hop via Goldman, 2-hop via Harvard)
```

## Invoke Skill

This command activates the `relationship-graph` agent.
