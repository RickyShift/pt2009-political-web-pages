# pt2009-political-web-pages

4,265 pages from the 2009 Portuguese web archive crawl (arquivo.pt),
each one matched to at least one Portuguese political party and mapped to a
broad ideological category, together with their archived HTML (4,083 of the
4,265 successfully retrieved -- see `metadata.csv` for the per-page status).

Produced by the processing pipeline in
[RickyShift/Portuguese_Web](https://github.com/RickyShift/Portuguese_Web)
(see `work/5_Fuzzy_Match.py`, `work/6_Party_Category.py` and
`work/8_Dataset.py` there for the matching methodology and export code). This
repository holds only the resulting dataset.

## Contents

- `metadata.csv` -- one row per page:
  - `id` -- page id in the source database.
  - `url` -- clean URL (query string stripped during deduplication upstream), SURT-canonicalized,
    e.g. `(com,blogspot,example,)/2009/06/post.html`.
  - `plain_url` -- the same URL in ordinary form, e.g. `http://example.blogspot.com/2009/06/post.html`.
  - `capture_date` -- when arquivo.pt crawled the page.
  - `real_date` -- the page's actual content date, extracted separately from the crawl date (`YYYYMMDD` or `YYYYMM`).
  - `matched_parties` -- comma-separated party name(s) the page matched on.
  - `party_category` -- comma-separated ideological categor(y/ies): Radical Left, Mainstream Left, Mainstream Right, Radical Right, Other.
  - `download_status` -- `ok`, `not_found`, `skipped_non_html`, `failed`, `skipped_no_date_or_url`, or `error`. See note below.
  - `http_status` -- the HTTP status code returned by arquivo.pt, where applicable.
  - `html_filename` -- the corresponding file in `html/`, or empty if not downloaded.
- `html/{id}.html` -- the archived HTML itself, one file per successfully downloaded page.

## Download outcome

Of 4,265 pages: 4,083 (95.7%) have their HTML included in `html/`.
The rest are listed in `metadata.csv` with their outcome so the gap is visible
rather than silent:

- `ok`: 4083
- `skipped_non_html`: 156
- `not_found`: 17
- `error`: 9

Most non-`ok` rows are pages no longer archived under their (query-string-free)
clean URL -- arquivo.pt's own "page not archived" response, not an ambiguous
match. Use `metadata.csv`'s `url` column to re-fetch any of them directly
from arquivo.pt if needed.

## Categories present

Radical Left, Mainstream Left, Mainstream Right, Radical Right, Other

## License and reuse

The files in `metadata.csv` (URLs, dates, party/category labels) are this
project's own derived work, released under
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) -- see `LICENSE`.

The archived HTML under `html/` is **not** covered by that license: it is
third-party content (the original pages' own text, markup and assets) sourced
from [arquivo.pt](https://arquivo.pt), Portugal's public web archive, and
reflects the original pages as crawled in 2009. It belongs to its original
authors/publishers. Check arquivo.pt's own terms of use before any further
redistribution of the HTML itself.
