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

- Filename format: `YYYY-MM-DD 제목.md` (date prefix + Korean title), e.g. `2026-08-18 프로젝트 킥오프.md` — applies to all notes, including Zettelkasten notes
- New notes start in `00-Inbox/` and get moved into the appropriate PARA folder (or Zettelkasten) once triaged
- Use `[[wikilinks]]` to connect related notes rather than duplicating content

## PARA vs. Zettelkasten: where a note goes

PARA (folders 00–04) organizes material by *actionability* — where you'll need it and by when. Zettelkasten (`05-Zettelkasten/`) organizes ideas by *connection* — a flat pool with no subfolders, browsed and discovered through links rather than through folder hierarchy. The two layers coexist:

- If a note is project/task-bound reference material or action items → file it under the relevant `01-Projects`/`02-Areas`/`03-Resources` folder, as before.
- If a note captures a single, reusable idea you expect to reference from multiple contexts later → move it to `05-Zettelkasten/` instead. One note = one idea.
- Every Zettelkasten note must link to at least one or two related Zettelkasten notes via `[[wikilinks]]` — no orphan notes. The goal is discovery through the link graph, not through folders.
- PARA notes (especially project notes) can `[[link]]` out to relevant Zettelkasten notes rather than duplicating the idea inline.
