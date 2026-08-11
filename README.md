# Practical Deep Learning, self-paced section

A self-paced section of [fast.ai Practical Deep Learning for Coders](https://course.fast.ai/) run as an actual course: fixed weekly deadlines, a defined assignment each week, and a submission that either exists or does not. Paced at about 5 hours a week.

Live site: https://pistachionet.github.io/fastai-curriculum

Course material is by Jeremy Howard and the fast.ai team. This repo is a personal study record and is not affiliated with fast.ai.

## The schedule

Aug 16, 2026 to Jan 24, 2027. Notes are due Sunday 11:59pm local. Paced for about 5 hours a week, spread across weekday evenings rather than one sitting.

Most lessons run 2 weeks. The three hands-on, build-it-from-scratch lessons (3, 5, 8) get 3 weeks, since writing a training loop by hand doesn't compress into a single week at this pace. Review weeks stay at 1.

| Week | Due | Session | Reading |
| --- | --- | --- | --- |
| 1 | Aug 16 | Lesson 1: Getting started | ch 1 |
| 2 | Aug 23 | Lesson 2: Deployment | ch 2 |
| 3 | Sep 6 | Lesson 3: Neural net foundations (3 wks) | ch 4 |
| 4 | Sep 27 | Review week | ch 1, 2, 4 questionnaires |
| 5 | Oct 11 | Lesson 4: Natural Language (NLP) | ch 10 |
| 6 | Oct 25 | Lesson 5: From-scratch model (3 wks) | ch 4 and 9 |
| 7 | Nov 15 | Lesson 6: Random forests | ch 9 |
| 8 | Nov 29 | Review week | |
| 9 | Dec 6 | Lesson 7: Collaborative filtering | ch 8 |
| 10 | Dec 20 | Lesson 8: Convolutions (CNNs) (3 wks) | ch 13 |
| 11 | Jan 10 | Bonus: Data ethics | ch 3 |
| 12 | Jan 24 | Final project and retrospective | |

Lesson to chapter mapping is taken from the lesson pages on course.fast.ai, not guessed.

Budget is about 3 to 5 hours a week, weekdays. The review weeks and the extra time on lessons 3, 5, and 8 exist because a schedule with no slack becomes fiction the first time a week goes badly. Use them to catch up if you are behind and to rebuild things from memory if you are not.

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
