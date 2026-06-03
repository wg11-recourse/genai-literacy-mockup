<frontmatter>
  title: "Unit 2 · Using AI to Write Code"
  layout: default.md
  pageNav: 2
  pageNavTitle: "On this page"
</frontmatter>

<div class="hero">
  <div class="hero-text">
    <div class="eyebrow">Unit 2 · Practice</div>
    <h1 class="no-index">Using AI to Write Code — Responsibly and Correctly</h1>
    <p class="lead">Treat generated code like a confident junior's pull request: review it, don't merge on sight.</p>
  </div>
  <img class="hero-art" src="{{baseUrl}}/images/hero-unit-02.svg" alt="A code window under review with an approval checkmark">
</div>

<span class="ilo-tag">ILO 2.1 — review generated code</span>
<span class="ilo-tag">ILO 2.2 — integrity & attribution</span>
<span class="ilo-tag">ILO 2.3 — when reliance hurts learning</span>

Generated code compiles, runs, and looks right far more often than it *is* right. Treating it as a confident junior's pull request — to be reviewed, not merged on sight — is the habit this unit builds.

## Review it like a pull request

<box type="warning" header="**Fluent ≠ correct**">

The most dangerous AI code is the kind that almost works: an off-by-one, a missing edge case, a subtly insecure default. It passes a glance and fails in production.

</box>

Run every snippet through three lenses before you trust it:

1. **Correctness** — does it handle empty input, large input, the boundary case?
2. **Security** — does it interpolate user input into a query, shell, or path?
3. **Provenance** — do the functions and flags it calls actually exist?

<panel header="**Spot the flaw — can you find it before opening the answer?**" type="seamless" peek>

```python
def get_user(db, user_id):
    query = f"SELECT * FROM users WHERE id = {user_id}"
    return db.execute(query).fetchone()
```

<panel header="Answer" type="info" expanded>

**SQL injection.** `user_id` is interpolated straight into the query string. A value like `0 OR 1=1` returns every user. Use a parameterised query instead:

```python
db.execute("SELECT * FROM users WHERE id = ?", (user_id,))
```

</panel>

</panel>

## Integrity and attribution

<box type="important" header="**Disclose, don't disguise**">

Using AI is usually allowed; *hiding* it usually isn't. Follow your course's policy, and attribute assistance the same way you'd cite any other source. When unsure, ask the instructor **before** you submit.

</box>

## When leaning on AI costs you

<box type="definition" header="**The competence trap**">

If the AI does the part you were meant to *learn*, you'll pass the assignment and fail the exam. Offload the boilerplate; struggle through the fundamentals yourself.

</box>

## Check your understanding

<quiz>
  <question type="mcq" header="An AI gives you a 30-line function for an assignment. What's the responsible first move?" hint="What did the task actually ask you to demonstrate?">
    <q-option reason="Running tests is good, but it comes after you understand and can stand behind the code.">
      Paste it in, run the tests, and submit if they pass
    </q-option>
    <q-option correct reason="Right. Read it, confirm correctness and security, make sure you could have written and can explain it, and disclose the assistance per policy.">
      Read and verify it, confirm you understand every line, then attribute the assistance
    </q-option>
    <q-option reason="Rewording to hide AI use is exactly the integrity violation to avoid.">
      Reword the variable names so it looks like your own work
    </q-option>
  </question>

  <question type="checkbox" header="Which of these warrant a closer look in AI-generated code? (Select all that apply.)" hint="Think correctness *and* security.">
    <q-option correct reason="Yes — unhandled edge cases are a classic generated-code bug.">
      It assumes the input list is never empty
    </q-option>
    <q-option correct reason="Yes — interpolating user input into a query is an injection risk.">
      It builds an SQL query with an f-string from user input
    </q-option>
    <q-option correct reason="Yes — invented APIs are a hallmark of hallucinated code.">
      It calls a library function you can't find in the docs
    </q-option>
    <q-option reason="Clear names are good. They aren't a red flag in themselves.">
      It uses descriptive variable names
    </q-option>
  </question>
</quiz>

<box type="success" icon=":fas-circle-check:" header="**You've reached the end of the mockup**">

Two units, calm-academic styling, and the core MarkBind components — boxes, panels, tabs, tags, and quizzes — all in place.

</box>
