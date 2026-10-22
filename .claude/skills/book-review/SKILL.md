---
name: book-review
description: Build or update a book review page for Dan's book-reviews library (civedan/book-reviews, served by GitHub Pages). Use when asked to review a book, add a book to the library, or update an existing review. Covers the three-way ratings comparison (Claude's take, public consensus, Dan's own rating), research rules, page structure, and the PR flow.
---

# Book review workflow

Each review is a single static HTML page (`<slug>.html`) with the cover in `images/<slug>-cover.jpg`
and a card added to the `books` array in `index.html`. Use `the-gift.html` as the reference layout.
Theme each page from the cover's palette.

## Principle

The page must show three separate views of the book and never blend them:
1. **Claude's take** — Claude's own assessment, labelled as judgment.
2. **Public consensus** — what readers and critics outside this session say, with sources.
3. **Dan's rating** — Dan's own scores and words. Dan is the reviewer of record.

Never present a number as Dan's opinion unless Dan gave it. Never invent quotes, scores, page
counts or statistics. If something could not be verified, say so on the page.

## Step 1 — Ask Dan before writing (do not skip, do not assume he liked it)

Ask, in one message:
- Overall rating out of 5, and what he liked / disliked, in his own words.
- Score out of 5 for each of the four standard categories:
  - **Ideas** — originality and depth of the central ideas
  - **Readability** — clarity, structure, prose, pacing
  - **Actionability** — can the reader use it personally or professionally
  - **Evidence** — how well the claims are supported
- Anything he wants captured (highlights, notes, favourite passages, takeaways).

Compute his category average and show it next to his overall rating; the gap between the two is
informative and should be shown, not smoothed over.

## Step 2 — Research real content (the pages are only as good as this)

Do not write chapter summaries from the title alone.
- Get the real table of contents (publisher page, Library, Open Library, full text when legally
  public, e.g. the Anarchist Library for some titles).
- Ask Dan for Kindle/Apple Books highlights, notes, or an exported summary. His own highlights are the
  best source of "what he actually read".
- Use critical essays, publisher/author interviews and reputable summaries for the chapter
  breakdown. Label chapter summaries clearly if they come from themes and headings, not a close reading.
- Say in the page's note box exactly what the summaries are based on.

## Step 3 — Consensus (WebFetch/WebSearch)

- Goodreads book pages are fetchable and free (no subscription). Goodreads merges editions, so
  several edition URLs often return the same totals. Check you fetched the right book: a wrong
  edition can show a handful of ratings. Record average, rating count, star distribution, and the
  date checked.
- Amazon and some critic sites return 403; do not cite numbers from pages that could not be read.
  Say "not available" instead.
- Summarise recurring praise and recurring criticism across sources, with a link for each source
  and the date checked. Include one or two reader or critic criticisms that Dan would not have
  noticed ("what you may have missed").
- Use short attributed phrases at most; no long quotes.

## Step 4 — Claude's take

Give four category scores and an overall score, each with one line of reasoning. If it is more than
~0.5 away from the Goodreads average, say why. Do not simply echo a book's reputation: weigh
repetition, structure, evidence, and practical value as a reader would.

## Step 5 — Page structure

Tabs: Overview, All Chapters, (a book-specific concepts tab), Notable Ideas, **Ratings & Verdict**.
The Ratings & Verdict tab contains, in this order:
1. Three side-by-side cards: Claude's take, Consensus, Dan's rating.
2. Category table: Claude's four scores vs Dan's four scores, plus each average.
3. Consensus summary (praise, criticism, what you may have missed) with source links and date.
4. Dan's take, in his own words.
5. Strengths & limitations, who should read it, single most important insight.

The `index.html` card shows Dan's overall rating once it exists. Until a book has Dan's rating, it
must not be presented as his.

## Step 6 — Ship

- Branch off `main`, one book (or one batch of retrofits) per PR, draft PR first.
- Open the page in a browser (Playwright/Chromium is installed) and check it renders and the
  index shows the card before pushing.
- The repository is public and served by GitHub Pages; do not commit anything private.
- Merge only when Dan says to.
