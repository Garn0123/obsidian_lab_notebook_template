---
<%*
const meetingTitle = await tp.system.prompt("Meeting title")
await tp.file.rename(tp.date.now("YYYY-MM-DD") + " - " + meetingTitle)
-%>
date: <% tp.date.now("YYYY-MM-DD") %>
meeting_type: 
project: 
attendees: []
tags: []
---

daily:: [[Daily Notes/<% tp.date.now("YYYY-MM-DD") %> - Daily Note]]
summary:: 

# <% meetingTitle %>

## Context / Agenda


## Discussion


## Decisions Made


## Action Items
- [ ] 

## Related Notes
<!-- Links to experiments, papers, or ideas discussed -->

