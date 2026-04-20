---
tags: []
date_created: {{date:YYYY-MM-DD}} {{time:HH:mm}}
status: MOC
---

_Contains table of seminar/lecture notes._

# Overview 
# Concepts
# Gaps in the field
# Linked Topics

# Literature
This section is for papers that are directly linked to the topic. This also helps to link the ideas linked to those papers to this topic MOC.

```dataview
TABLE title as "Title", authors AS "Authors", year AS "Year", summary AS "Summary", URL
FROM "Reference Notes" 
WHERE contains(file.outlinks, [[]]) 
SORT file.cday DESC
```

# Seminars

```dataview
TABLE date_created AS "Date", summary AS "Summary"
FROM "000 Zettelkasten"
WHERE part_of = this.file.link
  AND source_type = "seminar"
SORT file.cday DESC
```

# References
