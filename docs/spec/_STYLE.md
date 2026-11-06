# Spec writing rules

Applies to every file in `docs/spec/`. Rules 5 and 7 apply to the `System` and `When` fields of a use case. Rule 11 applies to the whole use case.

**Why:** each sentence must have one meaning, so one system response becomes one
testable requirement. Everyday words do both.

## Rules

| # | Rule | Don't write | Write |
|---|---|---|---|
| 1 | **One thing, one name.** Use the exact word from the glossary. Never swap in a synonym. | "carrier balance" and "money held" for the same thing | "carrier balance" everywhere |
| 2 | **Use plain words.** show, keep, use, start, end, before, after | display, maintain, initialize, terminate, prior, subsequent | "The system shows the carrier balance." |
| 3 | **No idioms or flowery phrases.** | "green-light", "seal the deal", "U-turn" | "agree", "end", "change its mind" |
| 4 | **No vague verbs.** Banned: handle, manage, support, ensure, process, carry out, appropriate, properly, smoothly. | "The system handles errors smoothly." | "The system reports it could not read the file and keeps the last imported statement." |
| 5 | **No "can", "should", "might", "may" in a system response.** State what the system does. Use **"is allowed to"** only for a user permission. | "The system can show a message." | "The system shows a message." |
| 6 | **Short, active sentences.** One action per sentence. A `[BR-xxx]` citation does not count. | "A message is shown that the import has stopped and how many rows are done." | "The system shows a message that the import has stopped. The message states how many rows were read." |
| 7 | **Conditions go in the When field.** A system response has no "if". When behavior differs by step, open with a label: "At S3:", "On re-import:". | "If the file is invalid, the system rejects it." | When: "The file does not match a known statement format [BR-?]." System: "State the reason." |
| 8 | **One action per line. At most 7 lines per field.** | One cell of 110 words | One line per thing the user can observe |
| 9 | **Minimal bold.** Bold one glossary word on its first use in a line. At most 2 per line. | Bold a whole phrase | "Show the **discrepancy**." |
| 10 | **Evidence on its own line.** One tag per claim. Never mid-sentence. | "…the carrier balance stays at the old value `[observed: …]`, and does not include the new transfer." | `- **Evidence:** [observed: ghn-dashboard (balance unchanged after a transfer)]` |
| 11 | **Intent and response, not interface.** The user side says what the user wants. The system side says what the system reports, keeps, changes, or creates. Never name a widget, gesture, position, style, or label. Name a place only by region (see Regions). If an interface detail carries a requirement, write the requirement. | "The user opens the menu and picks a carrier statement." "Open the discrepancy view in the bottom corner." "Show a card with a retry button." | "The user picks a carrier statement." "Open the discrepancy view. The open discrepancies stay unchanged." "Let the user retry the import." |

Rules 4 to 7 keep a response testable. Rules 1 to 3 and 6 keep it readable. Rule 11 keeps the spec correct when the design changes.

## Evidence tags

One tag per claim. Keys stay in English so they are greppable; the source content is
written in prose:

- `[observed: <source> (<what it shows>)]` — seen in a transcript or product
- `[inferred: <source>]` — inferred from observed facts
- `[assumed]` or `[assumed: <what>]` — no evidence yet

In a list (usage context, knowledge, …), the last line can be a single `- **Evidence:** [assumed]`. It counts for every item above it without its own Evidence line.

## Regions

A region is a place that holds one kind of information. It is defined by what it holds, never by where it is or what it looks like. The list is closed; each product declares its own regions in the glossary. The project has no settled regions yet.

A use case may say something is shown, kept, or changed in a region. It must not say how a region is laid out or navigated to. To add a region, add a row to the glossary and say what it holds.

## Glossary

Use these words for these things. Add a row when a new word is needed. Do not add a synonym. A word never names a widget, gesture, position, or style. This table starts empty; each project declares its own terms and adds to them as it learns.

| Term | Meaning |
|---|---|
| **account** | The user's identity for access and for keeping their own data |
| _(add a row)_ | _(describe the meaning, do not name a widget or position)_ |

## How to check

There is no tool yet, so review does this. There are two groups of checks.

**Wording.** Run on the `System` and `When` fields, and on `Situation and goal`. Each hit is fixed or given a recorded reason.

```
handle|manage|support|ensure|process|carry out|appropriate|properly|smoothly|can|could|should|might|may
```

**Interface (rule 11).** Run on the whole use case, except the frontmatter, the generated block, and the `Research link` line. Each hit is rewritten as intent or response. A hit that is not interface language (e.g. "right" in "right-to-left text") gets a recorded reason.

```
button|click|tap|swipe|scroll|menu|dropdown|dialog|popup|tab|sidebar|toolbar|card|chip|icon|toggle|checkbox|screen|page|corner|above|below|left|right|label|input field
```

Then apply the **swap test** to each sentence: imagine the same product with a different interface, e.g. touch-only or voice-only. If the sentence is still true, it passes. If not, it describes the interface and is rewritten.
