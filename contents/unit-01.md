<frontmatter>
  title: "Unit 1 · How LLMs Actually Work"
  layout: default.md
  pageNav: 2
  pageNavTitle: "On this page"
</frontmatter>

<div class="hero">
  <div class="hero-text">
    <div class="eyebrow">Unit 1 · Foundations</div>
    <h1 class="no-index">How Large Language Models Actually Work</h1>
    <p class="lead">A programmer's mental model of next-token prediction — and why fluent is not the same as correct.</p>
  </div>
  <img class="hero-art" src="{{baseUrl}}/images/hero-unit-01.svg" alt="A sequence of tokens predicting the next token, with a probability hint">
</div>

<span class="ilo-tag">ILO 1.1 — explain token prediction</span>
<span class="ilo-tag">ILO 1.2 — AI vs. search vs. algorithm</span>
<span class="ilo-tag">ILO 1.3 — why hallucination happens</span>

A large language model does one deceptively simple thing: given some text, it predicts what comes next. Everything else — answering questions, writing code, explaining a bug — is that one operation, repeated.

<box type="definition" header="**Next-token prediction**">

A language model assigns a probability to every possible next *token* (roughly, a word-piece) and samples one. It appends that token and repeats. There is no database lookup and no guarantee of truth — only "what text is statistically likely to follow."

</box>

## A programmer's mental model

Think of it less like a search engine and more like an extremely well-read autocomplete. That framing explains both its strengths and its failure modes.

<tabs>
  <tab header="Generative AI">

Produces *new* text by sampling likely continuations. Great for drafting, explaining, and transforming. **No guarantee of correctness** — it can state false things fluently.

  </tab>
  <tab header="Search">

Retrieves *existing* documents that match a query. The results are real (they exist somewhere), but you must read and judge them yourself.

  </tab>
  <tab header="Deterministic algorithm">

Given the same input, always returns the same, provably-correct output (e.g. a sort). No creativity, no surprises — and no hallucination.

  </tab>
</tabs>

## Why hallucination happens

Because the model optimises for *plausible* text, not *true* text, it will confidently invent APIs, citations, or function signatures that look exactly right and do not exist.

<panel header="**Worked example — a plausible but fake API**" type="seamless" peek>

Ask a model to "use the `requests` library's built-in retry decorator" and it may produce:

```python
@requests.retry(max_attempts=3)   # ← this decorator does not exist
def fetch(url): ...
```

It reads like real `requests` code. It is fluent, idiomatic, and wrong. The fix isn't to trust harder — it's to verify against the actual docs.

</panel>

## Check your understanding

<quiz>
  <question type="mcq" header="Why can a language model produce a confident answer that is completely false?" hint="Think about what the model is optimising for.">
    <q-option reason="It does retrieve text, but that's search. A base LLM samples likely tokens; it isn't looking anything up.">
      It looked the answer up in a database and the database was wrong
    </q-option>
    <q-option correct reason="Exactly. It optimises for *plausible* continuations, and a confident-sounding falsehood can be highly plausible.">
      It predicts plausible next tokens, and a fluent falsehood can be more probable than an awkward truth
    </q-option>
    <q-option reason="Temperature affects randomness, but even at zero the model can still be confidently wrong.">
      Only because the temperature setting was too high
    </q-option>
  </question>

  <question type="mcq" header="Which task is a deterministic algorithm the right tool for — not generative AI?" hint="Which needs a provably correct, repeatable result?">
    <q-option reason="Drafting is open-ended — a good fit for generation.">
      Drafting a first explanation of recursion for a peer
    </q-option>
    <q-option correct reason="Correct. Sorting has a provably correct, repeatable answer — use an algorithm, not a probabilistic model.">
      Sorting a list of ten million integers correctly every time
    </q-option>
    <q-option reason="Brainstorming rewards variety, which generation provides.">
      Brainstorming names for a variable
    </q-option>
  </question>
</quiz>

<box type="success" icon=":fas-flag-checkered:" header="**Next**">

Move on to [Unit 2 · Using AI to Write Code]({{baseUrl}}/contents/unit-02.html), where we put this scepticism to work reviewing generated code.

</box>
