# Practical Deep Learning, self-paced section

A twelve week section of [fast.ai Practical Deep Learning for Coders](https://course.fast.ai/) run as an actual course: fixed weekly deadlines, a defined assignment each week, and a submission that either exists or does not.

Live site: https://pistachionet.github.io/fastai-curriculum

Course material is by Jeremy Howard and the fast.ai team. This repo is a personal study record and is not affiliated with fast.ai.

## The schedule

Twelve weeks, Aug 2 to Oct 18, 2026. Notes are due Sunday 11:59pm local.

| Week | Due | Session | Reading |
| --- | --- | --- | --- |
| 1 | Aug 2 | Lesson 1: Getting started | ch 1 |
| 2 | Aug 9 | Lesson 2: Deployment | ch 2 |
| 3 | Aug 16 | Lesson 3: Neural net foundations | ch 4 |
| 4 | Aug 23 | Review week | ch 1, 2, 4 questionnaires |
| 5 | Aug 30 | Lesson 4: Natural Language (NLP) | ch 10 |
| 6 | Sep 6 | Lesson 5: From-scratch model | ch 4 and 9 |
| 7 | Sep 13 | Lesson 6: Random forests | ch 9 |
| 8 | Sep 20 | Review week | |
| 9 | Sep 27 | Lesson 7: Collaborative filtering | ch 8 |
| 10 | Oct 4 | Lesson 8: Convolutions (CNNs) | ch 13 |
| 11 | Oct 11 | Bonus: Data ethics | ch 3 |
| 12 | Oct 18 | Final project and retrospective | |

Lesson to chapter mapping is taken from the lesson pages on course.fast.ai, not guessed.

Budget is about 8 hours on a lesson week and 4 to 5 on a review week. The two review weeks exist because a schedule with no slack becomes fiction the first time a week goes badly. Use them to catch up if you are behind and to rebuild things from memory if you are not.

## Submitting

Go to the site, expand the week, and either drop in a `.md` file or write directly in the box. Press submit. The page commits it to `notes/week-NN.md` through the GitHub API and the week flips to submitted.

To submit from the terminal instead, the site reads whatever is in `notes/`, so this works identically:

```
cp notes/TEMPLATE.md notes/week-01.md
git add notes/week-01.md && git commit -m "submit week-01" && git push
```

Keep the commit message format `submit week-NN`. That is how the site works out whether a submission was on time, using the commit date. Without it the week still shows as submitted, just without a timestamp.

## Connecting the token

Committing from the browser needs a token. On the site, press Connect GitHub and follow the steps:

1. Go to [Settings, Developer settings, fine-grained tokens](https://github.com/settings/personal-access-tokens/new)
2. Repository access: Only select repositories, then this repo
3. Permissions: Contents, Read and write. Nothing else
4. Generate, paste it into the site, save

The token is kept in your browser's local storage and is sent only to `api.github.com`. Scoped to one repo with contents access, the worst case if it leaks is that someone can write to this notes repo. The repo is public, so the notes are readable by anyone regardless.

Without a token the site still works, it just becomes read only.

## Publishing

```
git init && git add -A && git commit -m "course live"
gh repo create fastai-curriculum --public --source . --push
gh api -X POST repos/pistachionet/fastai-curriculum/pages -f "source[branch]=main" -f "source[path]=/"
```

Everything must sit at the repo root, not inside a subfolder:

```
index.html
README.md
.gitignore
notes/TEMPLATE.md
```

## Changing the schedule

Edit the `SCHEDULE` array in `index.html`. Dates are `YYYY-MM-DD` and are treated as due at 11:59pm local on that day. If you fall behind, shift the remaining dates as a block rather than moving one week at a time.
