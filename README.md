# Constitution of India — git history

The Constitution of India as a git repository: the text as adopted, then one
commit for every Constitution Amendment Act, and for every other Act, Order or
Supreme Court judgment that changed the text, in order.

Browse it with explanations and word-level highlighting at
https://constitutionofindia.vijaya.io.

## Using it

Every version is tagged:

| Tag | Version |
|---|---|
| `original-1950` | the text as adopted |
| `amendment-001` … | the Nth Constitution Amendment Act |
| `act-11-of-1960`, `order-c-o-272`, … | other Acts and Orders that changed the text |

```sh
git log --oneline --decorate                          # every version, newest first
git diff amendment-041 amendment-042 --word-diff      # what the 42nd Amendment changed
git diff original-1950 main --stat                    # every provision changed since 1950
git log -p -- constitution/preamble.md                # every change to the Preamble
git blame constitution/part-iii/article-15.md         # which version wrote each line
git checkout amendment-024                            # the text after the 24th Amendment
```

On GitHub, the same works through the commits list, the tags list, the compare
view (`/compare/amendment-041...amendment-042`) and blame.

## Layout

```
constitution/
  preamble.md
  part-i/article-1.md …     one file per article, grouped by Part
  schedules/schedule-01.md …
```

Each file holds the full text of one provision, with its number, title and Part
in the frontmatter. A provision that was omitted or struck down keeps its file,
with `status: omitted` or `status: struck-down`.

## Dates

Git cannot store dates before 1970, so the commit dates of early versions are
placeholders that only keep the versions in order. The real dates are trailers
at the end of each commit message:

```
Version: 1
Type: amendment
Assented: 1951-06-18
Effective: 1951-06-18
```

The version is the Amendment's number. Other Acts and Orders have a decimal
placing them after the last amendment assented to before they came into force
(`8.02` = the Bombay Reorganisation Act, 1960). The commits are in version
order, so the last commit can be an Act that was enacted but never brought into
force.

## Where the text comes from

Today's text is the English edition published by the Legislative Department,
Ministry of Law and Justice, Government of India. Every earlier version is
rebuilt from that edition's footnotes, which record what each amendment
replaced and when. Wording the footnotes do not quote is filled in from
scanned official editions (1949, 1993) and the Amendment Acts. A few
earlier passages are still missing and read
"⟨wording before the Nth Amendment not yet imported⟩".

This is not an official copy. The text has not been checked against the
Gazette of India (`Verified: false` in each commit). For legal use, rely on the
Legislative Department's publications.

This repository is generated: it is rebuilt from scratch whenever the data is
corrected, so its history may be rewritten. Do not send pull requests here.

## License

The text of the Constitution and of the Acts and Orders is published by the
Government of India; no rights in it are claimed here. Everything else in this
repository (its arrangement, commit messages and this README) is dedicated to
the public domain under [CC0 1.0](LICENSE).
