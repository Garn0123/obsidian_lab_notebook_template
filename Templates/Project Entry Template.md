<%*
const projectName = await tp.system.prompt("Project name")
await tp.file.rename(tp.date.now("YYYY-MM-DD") + " - " + projectName)
-%>
---
date: <% tp.date.now("YYYY-MM-DD") %>
project: <% projectName %>
note_type: project-entry
tags: []
---

daily:: [[Daily Notes/<% tp.date.now("YYYY-MM-DD") %> - Daily Note]] 
summary:: 

# <% tp.date.now("YYYY-MM-DD") %> — <% projectName %>

## Goals
- [ ] 

## Observations & Notes


## Experiments
<!-- Link to experiment pages created today -->
- 

## Next Steps
- [ ] 
