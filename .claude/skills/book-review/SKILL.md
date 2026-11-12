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

## Step 0 — Which book? (every run)

Ask which book this run is for unless Dan has named it in this conversation. Never default to the
book from a previous session or to `the-gift.html`; it is only the layout reference. Ask for the
cover image too (save it as `images/<slug>-cover.jpg`), and theme the page from it.

## Step 1 — Ask Dan before writing (do not skip, do not assume he liked it)

This happens on every run, for every book, even if Dan says "just make it". Wait for his answers
before generating anything.

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

Dan often pastes his review as free text. Pull the five numbers out of it, but if any are missing,
ambiguous (a range, "4 to 4.5") or out of range (e.g. "6 out of 5"), ask him rather than guessing;
cap at 5 and say so. Write his words up in third person in the Dan's Take section, close to what he
said, and add nothing he did not say.

## Step 2 — Research real content (the pages are only as good as this)

Do not write chapter summaries from the title alone.
- Get the real table of contents (publisher page, Library, Open Library, full text when legally
  public, e.g. the Anarchist Library for some titles).
- Ask Dan for Kindle/Apple Books highlights, notes, or an exported summary. His own highlights are the
  best source of "what he actually read".
- Use critical essays, publisher/author interviews and reputable summaries for the chapter
  breakdown. Label chapter summaries clearly if they come from themes and headings, not a close reading.
- Say in the page's note box exactly what the summaries are based on.
- Never keep content you cannot verify. Remove or clearly flag invented chapter titles, quotes,
  anecdotes, statistics, "bestseller" / "copies sold" hero claims and made-up part groupings. Label
  any example you invent as the reviewer's own illustration. Mark low-confidence chapters on the page,
  and flag details that rest on a single source.

## Step 3 — Consensus (WebFetch/WebSearch)

- Goodreads book pages are fetchable and free (no subscription). Goodreads merges editions, so
  several edition URLs often return the same totals. Check you fetched the right book: a wrong
  edition can show a handful of ratings, or even an unrelated book. Confirm the title and author on
  the fetched page before using any number. Record average, rating count, star distribution, and the
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

Six tabs: Overview, All Chapters, a book-specific framework tab, Toolkit, Key Phrases, and
**Ratings & Verdict** last. Model the non-ratings tabs on `radical-candor.html`: expandable per-chapter cards, a
deep dive on the book's core framework (per-element breakdown, side-by-side table, an interactive
sliders/quiz element), a Toolkit tab and a Key Phrases tab (paraphrased, no long quotes) before the
final **Ratings & Verdict** tab. Radical Candor's older Verdict tab does not have the three-way
ratings; use the Ratings & Verdict layout below instead.
The Ratings & Verdict tab contains, in this order:
1. Three side-by-side cards: Claude's take, Consensus, Dan's rating.
2. Category table: Claude's four scores vs Dan's four scores, plus each average.
3. Consensus summary (praise, criticism, what you may have missed) with source links and date.
4. Dan's take, in his own words.
5. Strengths & limitations, who should read it, single most important insight.

The `index.html` card shows Dan's overall rating once it exists. Until a book has Dan's rating, it
must not be presented as his.

## Step 6 — Ship

- Cover images live at `images/<slug>-cover.jpg`. Chat-pasted images cannot be extracted, so Dan
  drops the file into `images/`; rename it to the slug convention and remove exact duplicates.
- Update the book's card in `index.html` with Dan's overall rating once he has given it, and word the
  verdict as "Dan's rating. …; readers rate it X on Goodreads." No placeholder or old rating may remain
  on the page or the card.
- Branch off `main`, one book (or one batch of retrofits) per PR, draft PR first. If `gh` is not
  installed, push over HTTPS using the token in the `origin` remote URL (never print it) and open
  the PR with the GitHub REST API; mark it ready with the GraphQL `markPullRequestReadyForReview`
  mutation, then squash-merge via REST.
- Open the page in a browser (Playwright/Chromium is installed) and check it renders and the
  index shows the card before pushing.
- The repository is public and served by GitHub Pages; do not commit anything private.
- Merge only when Dan says to.

## Retrofitting existing reviews (batches)

1. Branch `retrofit-batch-N` off `main`; check each book's cover is in `images/`.
2. One subagent per book, each editing only its own page and running no git. Brief them with this
   skill, `mindset.html`/`process.html` as format examples and `radical-candor.html` for depth.
3. Read each report: Goodreads numbers and date, what was removed as unverifiable, single-source
   details. Tell Dan about every removal.
4. Ask Dan for his scores one book at a time, then fill the Dan card, category column, average,
   Dan's Take and the index card.
5. Verify in the browser pane (tabs, console, 375px overflow, any quiz or slider), commit, push, open
   a draft PR, and merge only when Dan says to.
