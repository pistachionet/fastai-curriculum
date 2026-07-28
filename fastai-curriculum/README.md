# fastai curriculum

Public record of working through Deep Learning for Coders with fastai and PyTorch. Twenty chapters, each with a due date and a deliverable. Notes get committed to this repo, and the site stamps itself by asking the GitHub API which notes exist.

Live page once published: https://pistachionet.github.io/fastai-curriculum

## How it works

- `index.html` is the whole site. The schedule lives in the `CURRICULUM` array inside it.
- Submitting a chapter means committing `notes/chapter-NN.md`. No database, no backend. The repo is the record.
- On load, the page fetches the contents of `notes/` from the GitHub API and marks each chapter done, running, due soon, overdue, or queued.
- If the API is unreachable or rate limited, the page shows the schedule without statuses.

## Publish

```
cd fastai-curriculum
git init && git add -A && git commit -m "curriculum live"
gh repo create fastai-curriculum --public --source . --push
```

Then enable Pages: Settings, Pages, Deploy from a branch, `main`, `/ (root)`. Or from the CLI:

```
gh api -X POST repos/pistachionet/fastai-curriculum/pages -f "source[branch]=main" -f "source[path]=/"
```

The site appears at `pistachionet.github.io/fastai-curriculum` within a couple of minutes.

## Submit a chapter

```
cp notes/TEMPLATE.md notes/chapter-01.md
# write it
git add notes/chapter-01.md && git commit -m "ch 01: your deep learning journey" && git push
```

Reload the page and chapter 1 reads `done`.

## Change the schedule

Edit the `due` fields in `CURRICULUM` inside `index.html`. Format is `YYYY-MM-DD`, parsed as local time.

Current pacing: every due date is a Sunday. One week for light chapters, two for most, three for the ones that are a wall (4, 12, 16, 17, 19). Three terms with real recesses:

| Term | Chapters | Dates |
| --- | --- | --- |
| Fall 2026, practice and applications | 1 to 9 | Aug 2 to Nov 22, 2026 |
| recess | | Nov 23 to Jan 17 |
| Spring 2027, foundations | 10 to 16 | Jan 24 to May 2, 2027 |
| recess | | May 3 to Jun 6 |
| Summer 2027, from scratch | 17 to 20 | Jun 27 to Aug 8, 2027 |

Recesses sit on top of OMSCS finals in December and late April, so nothing here is due while a graded course is closing out.

## Notes on the API check

Unauthenticated GitHub API allows 60 requests an hour per IP, which is plenty for a personal page. Filenames must match `chapter-NN.md` with a two digit number, so `TEMPLATE.md` and anything else in `notes/` is ignored.
