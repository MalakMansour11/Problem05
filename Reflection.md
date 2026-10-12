# Reflection — Side-Channel & Algorithmic Complexity Attacks Interactive Explainer

## What I built

For Problem 5, I built a single-page interactive web app with two demos tied directly to what I
worked through earlier in this sprint: a counting side-channel oracle (mirroring the `passCheck.c`
vulnerability from Problem 2) and a ReDoS slowdown demo (mirroring the `EmailValidator.java`
vulnerability from Problem 3). Rather than just describing these attacks in text, the app lets a
visitor actually run them — guess a password and watch the mismatch count narrow it down, or drag
a slider and watch a regex engine visibly slow down on a crafted input.

## How this deepened my understanding

Building the password-oracle demo forced me to implement the exact same logic as `compare_key()`
in JavaScript and then write the character-by-character solving loop myself, which made the attack
feel mechanical rather than abstract — it's really just "try each letter, keep whichever one makes
the score go down." Seeing it solve a random key live, over and over, made it obvious why leaking
even a single integer (a mismatch count) is enough to break an authentication check that looks
secure at a glance.

The ReDoS demo was the more surprising one to build. I expected the malicious input to blow up
dramatically, the way the classic catastrophic-backtracking examples do, but when I actually
measured it (both in the Java program for the written problem and in the browser's JavaScript
engine for this app), the slowdown was real but much more modest — a single-digit to low-double-digit
multiplier, not an explosion to seconds. That pushed me to actually read how the pattern's ambiguity
works (the `.` character doing double duty as both a mandatory separator and part of a character
class) instead of assuming "nested quantifiers always mean catastrophic blowup." It was a good
reminder that these vulnerabilities need to be measured, not just asserted.

## Workflow

I used Claude to help scaffold and test the app: generating the HTML/CSS/JS structure, then
actually running the embedded JavaScript logic (the password-cracking loop and the regex timing
functions) in a sandboxed Node environment to confirm it worked correctly before putting it in the
page, rather than trusting untested code. The same AI-assisted, verify-before-trusting approach
carried over from the rest of this sprint — for example, actually compiling and running the C and
Java programs from the earlier problems instead of guessing at their behavior. I reviewed the
generated code, adjusted the demo scenarios to match what I'd actually learned from Problems 2 and
3, and wrote this reflection myself based on that process.

## What I'd extend with more time

A third tab covering the AC-time linked-list bug from Problem 4 (the shared `static` field in
`Rectangle.java`) would round this out nicely — visualizing the cycle forming in the linked list as
shapes are added would make that bug as tangible as the other two. I'd also like to add a second
regex pattern side-by-side (a "fixed," non-ambiguous version) so visitors can see the fix, not just
the problem.
