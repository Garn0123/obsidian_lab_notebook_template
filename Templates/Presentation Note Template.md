<%*
const venue = await tp.system.prompt("Venue / event name")
const kind = await tp.system.suggester(
  ["Poster", "Talk", "Invited Talk", "Seminar", "Abstract Only"],
  ["poster", "talk", "invited-talk", "seminar", "abstract-only"],
  false,
  "Presentation type"
)
await tp.file.rename(tp.date.now("YYYY") + " - " + venue)
-%>
---
date: <% tp.date.now("YYYY-MM-DD") %>
project: 
note_type: presentation
venue: <% venue %>
presentation_type: <% kind %>
status: drafting
location: 
authors: 
date_submitted: 
date_decision: 
date_presented: 
url: 
tags: []
---

daily:: [[Daily Notes/<% tp.date.now("YYYY-MM-DD") %> - Daily Note]]
summary:: 

# <% tp.date.now("YYYY") %> — <% venue %>

## Deadlines & Logistics
<!-- Submission deadline, decision date, presentation date/time, format limits -->
- **Abstract deadline:** 
- **Word / character limit:** 
- **Presented on:** 

## Abstract
<!-- The submitted text, verbatim -->


## Talking Points / Narrative
<!-- The story being told and the order it's told in -->


## Figures & Data Used
<!-- Link the experiment or project pages each figure came from -->
- 

## Source Notes
<!-- Experiments, project entries, and papers this draws from -->
- 

## Feedback & Questions Received


## Follow-ups
- [ ] 
