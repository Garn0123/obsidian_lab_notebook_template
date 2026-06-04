# Obsidian E-Lab Notebook Template

A structured Obsidian vault for scientific record-keeping, designed for researchers, graduate students, and their mentees. Built around daily notes, experiment logs, literature tracking, and project dashboards — all connected through a consistent metadata system.

A DOI -> BibTex converter can be found at: https://www.bibtex.com/c/doi-to-bibtex-converter/

---

## Table of Contents

1. [Required Setup](#required-setup)
2. [Vault Structure](#vault-structure)
3. [Template Reference](#template-reference)
4. [Dashboards](#dashboards)
5. [How Everything Connects](#how-everything-connects)
6. [Day-to-Day Workflow](#day-to-day-workflow)
7. [Obsidian Gotchas & Tips](#obsidian-gotchas--tips)

---

## Required Setup

### Plugins

This vault requires one community plugin and one built-in Obsidian feature:

#### 1. Templater (Community Plugin)

Templater powers all template automation — file renaming, date stamping, and interactive prompts.

1. Open **Settings → Community plugins → Browse**
2. Search for **Templater** and install it
3. Enable it, then open **Settings → Templater**
4. Set **Template folder location** to `Templates`
5. Enable **Trigger Templater on new file creation** — this allows templates to run automatically when you create a note from a template

#### 2. Bases (Built-in, Obsidian v1.8+)

The `.base` dashboard files and the `base` code blocks embedded in Daily Notes and Project Overviews use Obsidian's native **Bases** feature. This is built into Obsidian — no plugin install needed — but requires **Obsidian v1.8 or later**. Update Obsidian if the `.base` files appear as raw text or the embedded tables don't render.

### Folder Structure

The vault ships with these folders. **Do not rename them** — the Base filters depend on exact folder names:

```
Daily Notes/
Dashboards/
Experiments/
Images/
Papers/
Templates/
```

You must also **manually create** one additional folder before using the Ideas template:

```
Ideas/
```

The Project Overview's Ideas dashboard queries `file.inFolder("Ideas")`, so this folder must exist for that section to populate.

If you plan to keep meeting notes and method notes organized, it is also recommended to create:

```
Meetings/
Methods/
```

These folders are not queried by any Base filter currently, but keeping them consistent will make the vault easier to navigate.

---

## Vault Structure

| Folder | Purpose |
|---|---|
| `Daily Notes/` | One note per day, auto-named `YYYY-MM-DD - Daily Note` |
| `Experiments/` | Individual experiment/task logs |
| `Papers/` | Literature notes, one per paper |
| `Ideas/` | Hypothesis and idea seeds (create this manually) |
| `Meetings/` | Meeting notes (create this manually, optional) |
| `Methods/` | Reusable protocol and method documentation (create this manually, optional) |
| `Images/` | Figures and images to embed in notes |
| `Templates/` | All Templater templates — do not create notes here |
| `Dashboards/` | Global Base views (All Papers, Experiment Tracker) |

---

## Template Reference

All templates are accessed via **Templates → Insert template** or by creating a new note and selecting a template. Each template prompts you for a name, sets the filename automatically, and fills in today's date.

---

### Daily Note Template

**File:** `Templates/Daily Note Template.md`  
**Where to save:** `Daily Notes/`  
**Filename format:** `YYYY-MM-DD - Daily Note` (set automatically)

The anchor note for each day. All other note types link back to the daily note they were created on via the `daily::` inline field. The embedded Base table at the bottom auto-populates with every note that links to this daily note, giving you a summary of everything created that day.

**Sections:**
- **Goals** — intentions for the day
- **Notes & Observations** — freeform log space
- **Today's Pages** — auto-populated Base table of all notes linking to this daily note
- **End of Day** — wins, blockers, and plans for tomorrow

**Tip:** Create this note first each morning before starting any other work. The `daily::` links in other templates expect a note at `Daily Notes/YYYY-MM-DD - Daily Note` to exist.

---

### Experiment Note Template

**File:** `Templates/Experiment Note Template.md`  
**Where to save:** `Experiments/`  
**Filename format:** `YYYY-MM-DD - <experiment name>` (set automatically)

The core record of a single experiment, analysis run, or computational task. Templater will prompt you for a task/experiment name when you create the note.

**Frontmatter fields:**

| Field | Description |
|---|---|
| `date` | Auto-filled with today's date |
| `project` | Project name — must match exactly across notes for the Project Overview dashboards to work |
| `task_type` | E.g., `analysis`, `wet-lab`, `computation`, `QC` |
| `status` | `active`, `complete`, `failed`, `on-hold` |
| `target` | The biological target, dataset, or subject of the experiment |
| `method` | Link to a Method note or name the method used |
| `software` | Primary software or pipeline used |
| `version` | Software/pipeline version (critical for reproducibility) |
| `tags` | Free-form tags |

**Inline fields:**
- `daily::` — links back to today's daily note
- `summary::` — a one-line description, shown in dashboard tables

**Sections:** Setup → Implementation/Protocol → Results & Output → Issues & Notes → Next Steps

---

### Paper Note Template

**File:** `Templates/Paper Note Template.md`  
**Where to save:** `Papers/`  
**Filename format:** Paper title (sanitized, set automatically)

Paste a BibTeX entry when prompted and the template will auto-extract the title, authors, year, journal, and DOI — including conversion of LaTeX accent commands (e.g., `\'e` → `é`). Leave the prompt blank to fill fields manually.

**Frontmatter fields:**

| Field | Description |
|---|---|
| `date_read` | Auto-filled |
| `authors` | Semicolon-separated from BibTeX, or entered manually |
| `year` | Publication year |
| `journal` | Journal or conference venue |
| `doi` | Used by the Project Overview Papers filter to identify paper notes |
| `rating` | Your rating (e.g., 1–5 stars, or `high/medium/low`) |
| `status` | `unread`, `reading`, `read`, `skimmed` |
| `project` | Project this paper is relevant to |
| `tags` | Topics, methods, organisms, etc. |
| `summary` | One-line summary |

**Sections:** Key Findings → Methods Notes → Relevance to My Work → Figures/Data → Questions & Follow-ups → Quotes/Passages

**Note:** The BibTeX parser handles the most common LaTeX accent and formatting commands, but complex or unusual LaTeX macros may not parse correctly. Check the auto-filled fields before saving.

---

### Idea Note Template

**File:** `Templates/Idea Note Template.md`  
**Where to save:** `Ideas/`  
**Filename format:** Idea name (set automatically)

A structured space to develop a hypothesis or research idea before it becomes a formal experiment. The `became_experiment` field lets you link an idea to the experiment note it eventually produced, preserving the intellectual lineage.

**Frontmatter fields:**

| Field | Description |
|---|---|
| `date` | Auto-filled |
| `project` | Project this idea belongs to |
| `status` | `seedling`, `developing`, `ready-to-test`, `abandoned`, `promoted` |
| `tags` | Free-form |
| `became_experiment` | Link to the Experiment Note if this idea was pursued |

**Sections:** Core Hypothesis → Motivation/Problem → Supporting Evidence → Open Questions → Potential Approaches → Risks/Weaknesses → Next Step to Validate

---

### Meeting Note Template

**File:** `Templates/Meeting Note Template.md`  
**Where to save:** `Meetings/`  
**Filename format:** `YYYY-MM-DD - <meeting title>` (set automatically)

**Frontmatter fields:**

| Field | Description |
|---|---|
| `date` | Auto-filled |
| `meeting_type` | E.g., `one-on-one`, `lab-meeting`, `committee`, `collaboration` |
| `project` | Project discussed |
| `attendees` | List of attendees |
| `tags` | Free-form |

**Sections:** Context/Agenda → Discussion → Decisions Made → Action Items (checkbox list) → Related Notes

---

### Method Note Template

**File:** `Templates/Method Note Template.md`  
**Where to save:** `Methods/`  
**Filename format:** `<method name> - Method` (set automatically)

A living protocol document for a reusable technique or pipeline. Unlike an experiment note (which records a single run), a method note documents the general procedure so it can be linked from many experiment notes.

**Frontmatter fields:**

| Field | Description |
|---|---|
| `date_created` | Auto-filled |
| `date_updated` | Update this manually when the protocol changes |
| `version` | Protocol version (starts at `v1.0`) |
| `software` | List of software dependencies |
| `tags` | Free-form |

**Sections:** Overview → Requirements → Protocol (numbered steps) → Parameters & Configuration → Known Issues & Gotchas → Validation/Benchmarks → Experiments Using This Method → References

The "Experiments Using This Method" section will accumulate backlinks automatically as experiment notes reference this method note.

---

### Project Entry Template

**File:** `Templates/Project Entry Template.md`  
**Where to save:** Inside a project subfolder, or `Experiments/`  
**Filename format:** `YYYY-MM-DD - <project name>` (set automatically)

A daily or session-level log entry scoped to a specific project. Lighter-weight than an experiment note — use this for days when you're doing project-level planning, writing, or coordination rather than running a specific experiment.

**Frontmatter fields:**

| Field | Description |
|---|---|
| `date` | Auto-filled |
| `project` | Project name — must match exactly |
| `note_type` | Fixed as `project-entry` — do not change, required by the Project Overview Base filter |
| `tags` | Free-form |

**Sections:** Goals (checklist) → Observations & Notes → Experiments (links) → Next Steps (checklist)

---

### Project Overview Template

**File:** `Templates/Project Overview Template.md`  
**Where to save:** Anywhere convenient (e.g., a top-level `Projects/` folder or the project subfolder itself)  
**Filename format:** `<project name> - Overview` (set automatically)

The hub for a single project. Four embedded Base tables auto-populate based on the `project` frontmatter field, pulling in project entries, experiments, papers, and ideas that share the same project name.

**Frontmatter fields:**

| Field | Description |
|---|---|
| `project` | Project name — the anchor for all four dashboard queries |
| `date_started` | Auto-filled |
| `status` | `active`, `complete`, `on-hold` |
| `tags` | Free-form |

**Embedded dashboards:**
- **Project Entries** — all notes with `note_type == "project-entry"` and matching `project`
- **Experiments & Tasks** — all notes in `Experiments/` with matching `project`
- **Papers** — all notes in `Papers/` with a `doi` field and matching `project`
- **Ideas & Hypotheses** — all notes in `Ideas/` with matching `project`

---

## Dashboards

### Experiment Tracker

**File:** `Experiments/Experiment Tracker.base`

A global table of every note in the `Experiments/` folder, sorted by date descending. Displays: date, project, task\_type, method, target, software, version, status, and summary. Use this for a lab-wide view of all experiments across all projects.

### All Papers

**File:** `Dashboards/All Papers.base`

A global table of every note in the `Papers/` folder, grouped by project. Displays: authors, year, journal, project, tags, status, and rating. Use this to browse the full literature library.

---

## How Everything Connects

The vault uses two mechanisms to link notes together: **YAML frontmatter** (for Base queries) and **inline fields** (for backlinks and daily summaries).

```
Daily Note
  └── Today's Pages table  ← populated by notes with daily:: link pointing here

Project Overview
  ├── Project Entries table  ← notes with note_type == "project-entry" and matching project
  ├── Experiments table      ← notes in Experiments/ with matching project
  ├── Papers table           ← notes in Papers/ with matching project + doi
  └── Ideas table            ← notes in Ideas/ with matching project

Experiment Note
  ├── daily:: → Daily Note
  ├── project: → Project Overview (via matching string)
  └── method: → Method Note (by link or name)

Idea Note
  ├── daily:: → Daily Note
  ├── project: → Project Overview
  └── became_experiment: → Experiment Note
```

**The `project` field is the connective tissue.** For the Project Overview dashboards to work, the `project` field must be spelled identically across all related notes. A mismatch in capitalization or spacing will silently exclude a note from the dashboard. Consider maintaining a reference list of your project names and copy-pasting them.

---

## Day-to-Day Workflow

1. **Start the day:** Create a Daily Note from the template. It becomes today's anchor.
2. **Run an experiment:** Create an Experiment Note. Fill in `project`, `task_type`, `method`, `status`, and `summary`. The `daily::` field links it back automatically.
3. **Read a paper:** Create a Paper Note. Paste the BibTeX entry at the prompt. Tag with the relevant `project`.
4. **Capture an idea:** Create an Idea Note. Flesh out the hypothesis and mark `status: seedling`. When it becomes an experiment, fill in `became_experiment`.
5. **Log a meeting:** Create a Meeting Note. Fill in action items as checkboxes.
6. **End the day:** Return to the Daily Note. Fill in Wins, Blockers, and Tomorrow. The Today's Pages table shows everything you created.
7. **Review a project:** Open the Project Overview. All four tables populate automatically from the `project` field on your notes.

---

## Obsidian Gotchas & Tips

### Templater must run before you see the rendered note

Templater processes `<% ... %>` syntax when a template is inserted. If you see raw template code in a new note, Templater either didn't run or isn't enabled. Check that **Trigger Templater on new file creation** is on in Templater settings.

### The `daily::` link requires the daily note to already exist

The `daily::` inline field uses a wikilink in the format `[[Daily Notes/YYYY-MM-DD - Daily Note]]`. If you haven't created today's daily note yet, this link will be red/unresolved, and the note won't appear in the daily note's Today's Pages table. Create the Daily Note first each morning.

### Base filters are case-sensitive and exact-match

The queries `project == this.project` and `task_type != ""` are exact string comparisons. A note with `project: CRISPR Screen` will not match a project overview with `project: crispr screen`. Be consistent with capitalization — pick a convention for each project name and stick to it.

### The `base` code blocks only render inside Obsidian

The Base syntax inside code fences (the `today's pages` table in the Daily Note, and the four tables in the Project Overview) is Obsidian-specific and requires v1.8+. These blocks appear as raw YAML in any other Markdown editor, on GitHub, or in exported PDFs.

### `file.inFolder()` vs `file.path.contains()`

The Project Overview uses both filter styles. `file.inFolder("Ideas")` matches files directly inside the `Ideas/` folder. `file.path.contains("Experiments/")` matches any file whose path contains that string, including subfolders. If you organize experiments into subfolders like `Experiments/ProjectA/`, they will still appear in the Experiment Tracker but `file.inFolder("Experiments")` queries would miss them — be aware of which style a given filter uses.

### Inline fields (`summary::`, `daily::`) must use the double-colon syntax

The `summary::` and `daily::` fields in note bodies are inline metadata, read by the Base engine. They are distinct from the YAML frontmatter block. Do not confuse them with normal text or move them inside the `---` frontmatter — they must appear in the note body. Obsidian renders them as normal text but indexes the value.

### Paper BibTeX parsing has limits

The Paper Note template parses common LaTeX accent commands and formatting macros, but it will not handle:
- Custom macros (e.g., `\mycustomcmd`)
- Nested or multi-level brace structures in some edge cases
- Fields spread across multiple lines in unusual ways

Always review the auto-filled frontmatter before moving on. The `title`, `authors`, `year`, `journal`, and `doi` fields are the most important to verify.

### Updating `date_updated` in Method Notes is manual

The Method Note template pre-fills `date_updated` with today's date at creation time. Obsidian has no hook to auto-update this field when you edit a note. When you revise a protocol, manually update the `date_updated` field and increment the `version`.

### Images should go in the `Images/` folder

Obsidian embeds images with `![[filename]]` wikilinks. Store all images in `Images/` to keep the vault organized and to avoid Obsidian scattering attachments across folders. Set this as the default attachment location in **Settings → Files & Links → Default location for new attachments → In the folder specified below → `Images`**.

### Avoid spaces in tag values

Tags in the `tags: []` frontmatter list work best without spaces. Use hyphens or underscores: `multi-omics` not `multi omics`. Obsidian's tag system will treat spaced tags inconsistently.

### The `status` field is not enforced

The templates suggest specific values for `status` (e.g., `active`, `complete`, `seedling`), but Obsidian does not enforce a controlled vocabulary. Decide on standard values as a lab and document them somewhere so everyone uses the same terms — otherwise filtering and grouping by status in Base views will fragment across variants.

### Sync and version control

Obsidian vaults are plain Markdown files. You can track your notebook in Git for version history and backup. Note that `.DS_Store` files (macOS) and the `.obsidian/` folder (plugin settings, workspace state) should generally be in `.gitignore` unless you want to share your exact Obsidian configuration. The `.obsidian/` folder contains your Templater settings, so sharing it can help onboard labmates to the same setup.
