# CHARACTER DATA TEMPLATE

This document specifies the JSON schema for character entries in The Harvester's Sky project.

---

## FILE ORGANIZATION

- `historical-figures.json` - Real historical figures from the 13th century and earlier
- `fictional-characters.json` - Original characters created for the game (to be created)

---

## JSON SCHEMA

Each character is represented as a JSON object with the following structure:

```json
{
  "id": "unique-kebab-case-identifier",
  "name": {
    "primary": "Primary Name",
    "alternates": ["Alternate spellings", "Other names"]
  },
  "dates": {
    "birth": "YYYY or 'c. YYYY' or 'unknown'",
    "death": "YYYY or 'c. YYYY' or 'unknown' or 'alive-1274'",
    "reign": {
      "start": "YYYY",
      "end": "YYYY"
    }
  },
  "titles": [
    {
      "title": "Official Title",
      "description": "What this title means",
      "period": "YYYY-YYYY"
    }
  ],
  "category": "Primary category",
  "gameRelevance": {
    "role": "Brief role in game context",
    "description": "Detailed relevance to the narrative",
    "narrative": "Optional: specific narrative hooks"
  },
  "relationships": [
    {
      "figureId": "other-character-id",
      "type": "father|mother|spouse|son|daughter|ally|enemy|mentor|servant|etc"
    }
  ],
  "historical": {
    "summary": "Key historical facts and context",
    "significance": "Why this person matters historically",
    "sources": ["Primary sources", "Historical texts"]
  },
  "tags": ["searchable", "keywords", "for", "filtering"],
  "meta": {
    "addedDate": "YYYY-MM-DD",
    "lastModified": "YYYY-MM-DD"
  }
}
```

---

## FIELD DEFINITIONS

### Required Fields

**id** (string)
- Unique identifier in kebab-case
- Used for cross-referencing between characters
- Example: `"genghis-khan"`, `"pope-innocent-iv"`

**name.primary** (string)
- The most commonly used name for the character
- How they should be referred to in game materials

**category** (string)
- Primary classification of the character
- Examples: `"Mongol Rulers"`, `"Papal Envoys"`, `"Mamluk Leaders"`, `"Fictional - Player Character"`

**gameRelevance** (object)
- **description**: Why this character matters to the game

**tags** (array of strings)
- Searchable keywords for filtering and organization
- Include: cultural background, time period, role type, allegiances

---

### Optional Fields

**name.alternates** (array)
- Alternate spellings, translations, or names
- Example: Dokuz Khatun might also be "Doquz Khatun"

**dates** (object)
- Can be partial: just birth, just death, just reign
- Use `"c. YYYY"` for approximate dates
- Use `"unknown"` when dates are unclear
- Use `"alive-1274"` for characters alive during game setting

**titles** (array)
- Multiple titles with time periods
- Useful for characters who held different positions over time

**gameRelevance.role** (string)
- Brief one-line summary of their function in the game

**gameRelevance.narrative** (string)
- Specific story hooks, plot connections, dramatic potential

**relationships** (array)
- Links to other characters by their `id`
- Types can be familial, political, religious, antagonistic, etc.

**historical.summary** (string)
- Condensed historical biography

**historical.significance** (string)
- Why they matter in the broader historical context

**historical.sources** (array)
- Primary sources, historical texts, scholarly works
- Helps with research and fact-checking

**meta** (object)
- Administrative tracking for when entries were added or modified

---

## CATEGORIES

### For Historical Figures
- `"Mongol Rulers & Nobility"`
- `"Papal Envoys & Friars"`
- `"European Leaders"`
- `"Mamluk Leaders"`
- `"Travelers & Merchants"`
- `"Islamic Scholars"`
- `"Nestorian Christians"`
- `"Ancient Sources"`
- `"Scythian Figures"`

### For Fictional Characters (Future)
- `"Fictional - Player Character"`
- `"Fictional - NPC"`
- `"Fictional - Victim"`
- `"Fictional - Antagonist"`
- `"Fictional - The Harvesters Cult"`
- `"Fictional - Supporting Cast"`

---

## RELATIONSHIP TYPES

### Familial
`father`, `mother`, `son`, `daughter`, `spouse`, `sibling`, `grandfather`, `grandmother`

### Political
`ally`, `enemy`, `rival`, `vassal`, `overlord`, `ambassador`, `diplomat`

### Religious
`coreligionist`, `religious-rival`, `patron`, `convert`

### Social
`mentor`, `student`, `friend`, `servant`, `master`, `traveling-companion`

### Narrative (for fictional characters)
`victim`, `suspect`, `accuser`, `conspirator`, `protector`, `hunter`

---

## TAG CONVENTIONS

### Culture/Ethnicity
`mongol`, `european`, `arab`, `persian`, `scythian`, `nestorian`, `buddhist`, `muslim`, `christian`

### Role
`ruler`, `envoy`, `merchant`, `scholar`, `warrior`, `priest`, `diplomat`, `spy`

### Time Period
`pre-1200`, `1200-1250`, `1250-1274`, `1274-present`, `post-1274`, `ancient`

### Allegiance
`ilkhanate`, `golden-horde`, `papacy`, `mamluk`, `crusader-states`, `yuan-dynasty`

### Narrative
`alliance-seeker`, `christian-connections`, `kurgan-disturber`, `witness`, `cult-member`

---

## USAGE EXAMPLES

### Minimal Entry (Background Character)
```json
{
  "id": "ogodei-khan",
  "name": {
    "primary": "Ögödei Khan"
  },
  "dates": {
    "reign": {
      "start": "1229",
      "end": "1241"
    }
  },
  "category": "Mongol Rulers & Nobility",
  "gameRelevance": {
    "description": "Historical context: Genghis Khan's successor, continued expansion"
  },
  "tags": ["mongol", "khan", "pre-1250"],
  "meta": {
    "addedDate": "2026-01-07"
  }
}
```

### Full Entry (Central Character)
```json
{
  "id": "abaqa-khan",
  "name": {
    "primary": "Abaqa Khan",
    "alternates": ["Abagha"]
  },
  "dates": {
    "birth": "1234",
    "death": "1282",
    "reign": {
      "start": "1265",
      "end": "1282"
    }
  },
  "titles": [
    {
      "title": "Ilkhan",
      "description": "Ruler of the Mongol Persian realm",
      "period": "1265-1282"
    }
  ],
  "category": "Mongol Rulers & Nobility",
  "gameRelevance": {
    "role": "Host of the Tabriz court",
    "description": "Second Ilkhan, son of Hulagu Khan who sacked Baghdad. The court setting in 1274 is HIS court.",
    "narrative": "The khan whose court forms the physical and political setting of the game. His tolerance of multiple religions creates the unique atmosphere."
  },
  "relationships": [
    {
      "figureId": "hulagu-khan",
      "type": "father"
    },
    {
      "figureId": "dokuz-khatun",
      "type": "spouse"
    },
    {
      "figureId": "arghun-khan",
      "type": "son"
    },
    {
      "figureId": "philip-iv-france",
      "type": "potential-ally"
    }
  ],
  "historical": {
    "summary": "Second Ilkhan of the Persian Mongol realm. Maintained his father's policies of religious tolerance and sought alliances with European Christian powers against the Mamluks.",
    "significance": "Key figure in Franco-Mongol alliance attempts. His court at Tabriz was a crossroads of civilizations.",
    "sources": ["Rashid al-Din's Jami' al-tawarikh", "Bar Hebraeus Chronicle"]
  },
  "tags": ["mongol", "ilkhan", "1274-present", "alliance-seeker", "christian-connections", "tabriz-court"],
  "meta": {
    "addedDate": "2026-01-07",
    "lastModified": "2026-01-07"
  }
}
```

---

## MAINTENANCE NOTES

- When adding relationships, ensure both characters have reciprocal entries
- Date formats should remain consistent (use ISO format YYYY for years)
- Tags should be lowercase kebab-case
- Update `lastModified` date when making significant changes
- Keep descriptions concise but informative
- Cross-reference with `story/lore/historical-setting.md` for consistency
