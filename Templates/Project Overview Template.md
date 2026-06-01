<%*
const projectName = await tp.system.prompt("Project name")
await tp.file.rename(projectName + " - Overview")
-%>
---
project: <% projectName %>
date_started: <% tp.date.now("YYYY-MM-DD") %>
status: active
tags: []
---
# <% projectName %>

## Summary


## Goals

---

## Project Entries

```base
filters:
  and:
    - 'project == this.project'
    - 'note_type == "project-entry"'
    - 'file.path.contains("<% projectName %>")'
    - 'file.ext == "md"'
views:
  - type: table
    name: Project Entries
    order:
      - file.name
      - date
      - summary
      - tags
```

---

## Experiments & Tasks

```base
filters:
  and:
    - 'project == this.project'
    - 'task_type != ""'
    - 'file.path.contains("Experiments/")'
    - 'file.ext == "md"'
views:
  - type: table
    name: Experiments & Tasks
    order:
      - file.name
      - date
      - task_type
      - method
      - software
      - version
      - status
      - summary
    columnSize:
      file.name: 167
```

---

## Papers

```base
filters:
  and:
    - 'project == this.project'
    - 'file.path.contains("Papers/")'
    - 'doi != ""'
views:
  - type: table
    name: Papers
    order:
      - file.name
      - authors
      - year
      - status
      - rating
      - summary
```


## Ideas & Hypotheses
```base
filters:
  and:
    - file.ext == "md"
    - project == this.project
    - file.inFolder("Ideas")
views:
  - type: table
    name: Ideas
    groupBy:
      property: project
      direction: ASC
    order:
      - file.name
      - date
      - status
      - summary
    columnSize:
      file.name: 89

```

