# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

`C:\vault` is a personal Obsidian vault, not a codebase. There is no build, lint, or test process — work here means creating, organizing, and linking Markdown notes.

## Structure (PARA + Zettelkasten)

- `00-Inbox/` — unsorted new notes, triage later
- `01-Projects/` — notes tied to an active project with a concrete goal/deadline
- `02-Areas/` — ongoing responsibilities with no end date (health, work role, etc.)
- `03-Resources/` — reference material and topics of ongoing interest
- `04-Archive/` — inactive items moved out of Projects/Areas/Resources
- `05-Zettelkasten/` — flat pool of atomic, permanent idea notes that cut across all PARA categories (see below)

Folder and tag names stay in English (for structure and portability); note **content** is written in Korean. This split avoids cross-platform filename-encoding issues (macOS NFD vs Windows NFC) while keeping notes in the user's working language.

## Note conventions

- PARA notes (`00`–`04`): filename format `YYYY-MM-DD 제목.md` (date prefix + Korean title), e.g. `2026-08-18 프로젝트 킥오프.md`
- Zettelkasten notes (`05-Zettelkasten/`): filename is the claim itself, no date prefix, e.g. `습관은 마찰력처럼 작동한다.md` (see below — the title has to carry the idea, not the capture date)
- New notes start in `00-Inbox/` and get moved into the appropriate PARA folder (or distilled into Zettelkasten) once triaged
- Use `[[wikilinks]]` to connect related notes rather than duplicating content

## PARA vs. Zettelkasten: where a note goes

PARA (folders 00–04) organizes material by *actionability* — where you'll need it and by when. Zettelkasten (`05-Zettelkasten/`) organizes ideas by *connection* — a flat pool with no subfolders, browsed and discovered through links (and tags for filtering) rather than through folder hierarchy. The two layers coexist:

- If a note is project/task-bound reference material or action items → file it under the relevant `01-Projects`/`02-Areas`/`03-Resources` folder, as before.
- If a note captures a single, reusable idea you expect to reference from multiple contexts later → don't just move the raw capture. **Rewrite it in your own words as a self-contained claim**, then save it into `05-Zettelkasten/`. One note = one idea, and it has to be understandable without reading anything else.

### Zettelkasten note rules

- **Title = a claim, not a topic.** "습관은 마찰력처럼 작동한다" instead of "습관". A good title is a sentence someone could agree or disagree with.
- **Body is a rewrite, not a summary or copy-paste.** If you're transcribing a source, that belongs in a literature note (a regular Resources note tagged with its source) — the Zettelkasten note only gets created once you've distilled it into your own thought.
- **Tags, not subfolders.** Every permanent note gets `#type/permanent`; add a topic tag like `#domain/생산성` for filtering. The folder itself stays flat — tags do the categorization, not directory placement.
- **Link to at least one or two related notes** via `[[wikilinks]]` — no orphan notes. Discovery happens through the link graph (and Obsidian's automatic backlinks), not through folders.
- **MOC (Map of Content) notes**: when a topic accumulates enough permanent notes to need an entry point, create `MOC - 주제명.md` inside `05-Zettelkasten/` — just a list of links to the relevant notes, tagged `#type/moc`.
- PARA notes (especially project notes) `[[link]]` out to relevant Zettelkasten notes rather than duplicating the idea inline; the reverse direction shows up automatically via Obsidian's backlinks panel.
