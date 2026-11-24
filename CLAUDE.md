# Book Reviews

Dan's personal book-review library. Static HTML, one page per book, published with GitHub Pages
from `civedan/book-reviews` (`main` branch).

## Layout
- `index.html`: the library home page. Each book is a card in its `books` array.
- `<slug>.html`: one self-contained review page per book. `the-gift.html` is the reference layout.
- `images/<slug>-cover.jpg`: cover image; each page is themed from its cover's palette.
- `pdfs/`: supporting downloads linked from review pages.

## How to work here
- To add or update a review, use the `book-review` skill (`.claude/skills/book-review/SKILL.md`).
  It has the research rules, ratings structure and PR flow. Follow it rather than improvising.
- Dan is the reviewer of record. Never present a rating, quote or statistic as his unless he gave it.
- Preview locally: `python3 -m http.server 4200`, then open http://localhost:4200.

## Git
- Never commit to `main` directly. Use a branch per book or change, then open a PR.
- Remote uses SSH (`git@github.com:civedan/book-reviews.git`). Never put a token in the remote URL.
