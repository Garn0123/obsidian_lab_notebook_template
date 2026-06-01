---
date: <% tp.date.now("YYYY-MM-DD") %>
project: 
task_type: 
status: active
target: 
method: 
software: 
version: 
tags: []
---
<%*
const taskName = await tp.system.prompt("Task / experiment name")
await tp.file.rename(tp.date.now("YYYY-MM-DD") + " - " + taskName)
%>
daily:: [[Daily Notes/<% tp.date.now("YYYY-MM-DD") %> - Daily Note]] 
summary:: 

# <% tp.date.now("YYYY-MM-DD") %> — <% taskName %>

## Setup
<!-- Objectives, parameters, software versions, input data, config files, etc. -->


## Implementation / Protocol


## Results & Output


## Issues & Notes


## Next Steps

