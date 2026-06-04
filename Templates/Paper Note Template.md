---
<%*
const bibtex = await tp.system.prompt("Paste BibTeX (or leave blank to fill manually)")

const cleanLatex = (str) => {
  const accents = {
    "'a": "á", "'e": "é", "'i": "í", "'o": "ó", "'u": "ú",
    "'A": "Á", "'E": "É", "'I": "Í", "'O": "Ó", "'U": "Ú",
    "`a": "à", "`e": "è", "`i": "ì", "`o": "ò", "`u": "ù",
    "`A": "À", "`E": "È", "`I": "Ì", "`O": "Ò", "`U": "Ù",
    '"a': "ä", '"e': "ë", '"i': "ï", '"o': "ö", '"u': "ü",
    '"A': "Ä", '"E': "Ë", '"I': "Ï", '"O': "Ö", '"U': "Ü",
    "^a": "â", "^e": "ê", "^i": "î", "^o": "ô", "^u": "û",
    "^A": "Â", "^E": "Ê", "^I": "Î", "^O": "Ô", "^U": "Û",
    "~n": "ñ", "~N": "Ñ", "~a": "ã", "~A": "Ã",
    "ca": "ç", "cA": "Ç",
    "ss": "ß",
  }

  return str
    // Accent commands: {\'{e}}, {\'e}, \'e
    .replace(/\{?\\(['"`^~c])\{?([a-zA-Z])\}?\}?/g, (_, cmd, char) => {
      return accents[cmd + char] || char
    })
    // Formatting commands: {\it text}, {\bf text}, etc.
    .replace(/\{\\(?:it|bf|em|rm|tt|sc)\s+([^}]+)\}/g, "$1")
    // Remaining bare braces
    .replace(/[{}]/g, "")
    .trim()
}

const extractField = (field) => {
  // Match field = "..." or field = {...} including nested braces
  const match = bibtex.match(
    new RegExp(`${field}\\s*=\\s*(?:"((?:[^"\\\\]|\\\\.)*)"|\\{((?:[^{}]|\\{[^{}]*\\})*)\\})`, "is")
  )
  if (!match) return ""
  const raw = (match[1] || match[2] || "").trim()
  return cleanLatex(raw)
}

const extractFieldOrBare = (field) => {
  const quoted = extractField(field)
  if (quoted) return quoted
  const bare = bibtex.match(new RegExp(`${field}\\s*=\\s*([^,}\\s]+)`, "is"))
  return bare ? bare[1].trim() : ""
}
const sanitizeFilename = (str) => {
  return str
    .replace(/[\\/:*?"<>|#^[\]]/g, "")
    .replace(/\s+/g, " ")
    .trim()
}

const formatAuthors = (raw) => {
  return raw
    .split(/\s+and\s+/i)
    .map(a => cleanLatex(a.trim()))
    .join("; ")
}

const hasData = bibtex && bibtex.trim().startsWith("@")

const rawAuthors = hasData ? bibtex.match(/author\s*=\s*"([^"]+)"/is)?.[1] || bibtex.match(/author\s*=\s*\{([^}]+)\}/is)?.[1] || "" : ""

const title   = hasData ? extractField("title")                                  : await tp.system.prompt("Title")
const authors = hasData ? formatAuthors(rawAuthors)                              : await tp.system.prompt("Authors")
const year    = hasData ? extractFieldOrBare("year")                             : await tp.system.prompt("Year")
const journal = hasData ? (extractField("journal") || extractField("booktitle")) : await tp.system.prompt("Journal / Venue")
const doi     = hasData ? extractField("doi")                                    : await tp.system.prompt("DOI")

await tp.file.rename(sanitizeFilename(title))
-%>
date_read: <% tp.date.now("YYYY-MM-DD") %>
authors: <% authors %>
year: <% year %>
journal: <% journal %>
doi: <% doi %>
rating: 
status: unread
project: 
tags: []
comment: 
---
summary::

# <% title %>

## Key Findings


## Methods Notes


## Relevance to My Work


## Figures / Data Worth Noting


## Questions & Follow-ups


## Quotes / Passages

