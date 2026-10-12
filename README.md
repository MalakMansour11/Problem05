# Side-Channel & Algorithmic Complexity Attacks — Interactive Explainer

An interactive, single-file HTML/JavaScript visualization built for **SE/CprE 4210 Learning
Sprint #3, Problem 5**. It teaches two concepts from the algorithmic complexity and side-channel
attacks module through hands-on demos rather than static text.

## Live demo

Open `index.html` in any modern browser — no server, build step, or dependencies required. (If
you'd rather not open a local file directly, you can also serve it with
`python3 -m http.server` from this folder and visit `http://localhost:8000`.)

## What's inside

### 1. Counting Side-Channel demo

Simulates a password-check function that leaks the number of mismatched characters instead of a
plain pass/fail result — the same pattern analyzed in this sprint's `passCheck.c` problem. You can:

- Type your own guesses against a randomly generated 6-letter key and watch the mismatch count
  update live, with correct letters highlighted.
- Click **"Watch the automated attack"** to see the key solved automatically, one character at a
  time, using *only* the mismatch count — exactly how a real attacker would exploit this kind of
  oracle without ever seeing the source code or the key itself.

### 2. Algorithmic Complexity (ReDoS) demo

Runs a regex with the same structural ambiguity as the email validator analyzed in this sprint's
`EmailValidator.java` problem (a repeated group where a `.` can be consumed either as the
mandatory separator or inside the trailing character class). You can:

- Drag a slider to control how long the test inputs are.
- Click **"Run both inputs now"** to measure, in your own browser, how long the regex takes on a
  benign (matching) input versus a malicious (deliberately failing, ambiguity-heavy) input of
  similar structure.
- See the real measured times plotted as a bar chart, with the slowdown ratio reported below it.

Both demos run live computations in your browser (nothing is pre-recorded), so the numbers you
see are real timings/results for your machine at the moment you click.

## Why these two topics

The sprint's own Problems 2–4 cover exactly this module: a timing/count side-channel in a C
authentication check, a ReDoS-vulnerable Java regex, and an algorithmic-complexity bug in a
Java linked-list implementation. This app distills the first two of those into something a
classmate with no security background could click through in a couple of minutes and come away
understanding *why* "the algorithm reveals too much information" and "crafted input defeats the
expected time complexity" are both real, exploitable classes of vulnerability — not just abstract
definitions.

## Tech notes

- Pure HTML/CSS/vanilla JavaScript — no frameworks, no CDN dependencies, no build step.
- The chart is hand-drawn inline SVG (no charting library).
- All computation happens client-side; nothing is sent anywhere.

## Files

- `index.html` — the full app (structure, styling, and logic all in one file).
- `reflection.md` — reflection on building this and how it deepened understanding of the topic.
