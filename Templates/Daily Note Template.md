<%* await tp.file.rename(tp.date.now("YYYY-MM-DD") + " - Daily Note") %>
# <% tp.date.now("YYYY-MM-DD") %> — Daily Note

## Goals
- 

## Notes & Observations


---

## Today's Pages

```base
filters:
  and:
    - 'file.hasLink(this.file)'
    - 'file.ext == "md"'
views:
  - type: table
    name: "Today's Notes"
    order:
      - summary
      - tags
```

---

## End of Day

**Wins:**

**Blockers:**

**Tomorrow:**
