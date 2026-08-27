# DATASCI 350 - Data Science Computing

## Quiz 02 - Building a website with Quarto and GitHub Pages

### The scenario

A film magazine has hired you to turn its box-office dataset into a small public website. The repository holds `films.csv`: 104 well-known films from 1980 to 2025, with approximate budgets, worldwide revenues, runtimes, and ratings. Your job is to build a four-page Quarto website from it and publish the site on GitHub Pages.

This quiz is worth 6% of the final grade, and covers lectures 10 and 11. It is open-book and open-notes. It is an individual assessment: do not discuss the questions with your colleagues during class. You have 75 minutes.

You must be able to explain every command and every line you submit. The instructor may ask any student to walk through part of their work, during the quiz or right after it.

### The data

`films.csv` has one row per film and seven columns:

| Column | Meaning |
|--------|---------|
| `title` | Film title |
| `year` | Release year |
| `franchise` | Series the film belongs to, or `Standalone` |
| `budget_musd` | Production budget, millions of US dollars |
| `revenue_musd` | Worldwide revenue, millions of US dollars |
| `runtime_min` | Runtime in minutes |
| `imdb_rating` | Public rating, 0 to 10 |

The figures are approximate and not adjusted for inflation: they are for teaching, not for research. The file `create-dataset.py` shows how the dataset was built.

The quiz grades your Quarto and Git work, not your Python. Any working plot earns the marks, and the plotting patterns from the lecture 11 examples are enough for every task. Where a task needs a Python idiom we have not covered, the code is given in the task.

### Rules

- Work from the command line and your editor throughout. Files created or uploaded through the GitHub website lose points: the grader reads your commit history.
- Record every command you run in a file named `commands.txt` in the repository's root directory. Where a task asks for a short explanation, write it in `commands.txt` too.
- When you finish, post the link to your published website AND the link to your fork on Canvas, in the "Assignments" tab under Quiz 02.
- State your AI usage on the index page (see task 6). The syllabus AI policy applies.

### If `git push` asks for credentials

Your machine should already be logged in to GitHub. If a push fails with an authentication error, do not waste time creating tokens: run `gh auth login`, choose GitHub.com, then HTTPS, and log in with the browser. After that, `git push` works normally.

### Setup

1. Fork this repository to your GitHub account.
2. Clone your fork to your machine with the command line.
3. Change directory into the cloned repository.

### Tasks

1. Create a new Quarto website project inside the cloned repository folder (in VS Code, run `Quarto: Create Project`; if a tool asks you to choose a directory, use the repository folder itself). The folder gains `_quarto.yml`, `index.qmd`, `about.qmd`, and `styles.css`.

2. Create a `.gitignore` file with these three lines, then stage and commit it with the message "Add gitignore" before you render anything:

    ```text
    /.quarto/
    /_site/
    __pycache__/
    ```

3. In `_quarto.yml`, set the website title to `Box Office Numbers`.

4. In `_quarto.yml`, add the three analysis pages (tasks 7 to 9 create them) to the navigation bar with exactly these link texts: `Budget and Revenue`, `Runtime and Ratings`, `The Bond Films`.

5. In `_quarto.yml`, set a theme of your choice from [Quarto's theme list](https://quarto.org/docs/output-formats/html-themes.html) and add `freeze: auto` under the `execute:` key.

6. Edit `index.qmd` so the home page has: a title, two or three sentences describing the dataset, links to the three analysis pages, and one final line stating which AI tools you used during the quiz (or that you used none).

7. Create `budget-revenue.qmd`: a short introduction and a scatter plot of budget against revenue. Show the code (`echo: true`), and give the plot a caption with `fig-cap` and a label starting with `fig-`.

8. Create `runtime-rating.qmd`: a short introduction, a scatter plot of runtime against rating with the same chunk anatomy as task 7, and a table of mean rating by decade. Build the decade column with `films["decade"] = films["year"] // 10 * 10` (this idiom is given because we have not covered it).

9. Create `bond.qmd`: a line chart of revenue over time for the films where `franchise` is `James Bond`, plus one sentence of prose that reports the first and last Bond year in the data using inline code, so the sentence updates if the data changes.

10. On one of the three analysis pages, reference the figure in your text with `@fig-...` so it renders as a numbered, clickable link.

11. Render the website. Confirm that a `_freeze/` folder appeared, then stage and commit everything with the message "Add site pages and freeze".

12. Publish the site with `quarto publish gh-pages`, as shown in lecture 11. (If that command fails on your machine, the fallback is the manual route: set `output-dir: docs` in `_quarto.yml`, render, commit, push, and enable GitHub Pages from the `docs` folder in your fork's settings. Note in `commands.txt` which route you used.)

13. Open the published link and check that all four pages load and the navigation works. Fix and republish if not.

14. Update `commands.txt` with every command you used, then stage and commit it with the message "Add command log".

15. Push everything to your fork, then submit both links (website and fork) on Canvas. Done! 😊

### Bonus tasks

Attempt these only after finishing the main tasks, if you still have time. Document every step in `commands.txt`.

1. Give the site a custom look: edit `styles.css` (change at least the link colour and one font setting) and make sure `_quarto.yml` points at it.
2. Give the site paired light and dark themes in `_quarto.yml`, so the toggle appears in the navigation bar.

Best of luck!
