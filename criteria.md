# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

# Acceptance Criteria — TakeMeter

Written before training or viewing results.

Labels: seeking_support, venting, sharing_progress,
general_discussion.

Planned dataset: at least 200 real public posts from r/mentalhealth.
Actual label counts will be recorded after collection.

## 1. Overall accuracy

The classifier will achieve accuracy of at least 0.65 on the
held-out test set. All test posts count, including predictions
marked as needing review.

**Why this target:**
Uniform random guessing across four labels has an expected accuracy
of 25%. A target of 65% requires substantially better performance,
while allowing mistakes on posts that mix personal experiences,
requests for support, and expressions of distress. I will also
report the actual majority-label baseline for comparison.

## 2. Per-label performance

Every label will achieve an F1 score of at least 0.55 on the
held-out test set, and seeking_support will achieve at least 0.60.

**Why this target:**
Overall accuracy could hide poor performance on one category.
The minimum for every label requires the classifier to recognize
all four purposes. The higher target for seeking_support reflects
the importance of distinguishing explicit requests for help from
posts that mainly express feelings. This measures communication
purpose, not clinical urgency.

## 3. Label balance

In the complete labeled dataset, no label will account for more
than 50% of posts, and no label will account for less than 15%.

**Why this target:**
These limits are stricter than the assignment's 70% maximum.
They reduce the chance that one category dominates training.
With exactly 200 posts, each label would have at least 30 examples.
This provides representation, although small test-set counts may
still make per-label results unstable.

## 4. Labeling consistency

A second labeler will agree with my labels on at least 15 of the
20 independently labeled cold examples, giving agreement of
at least 75%.

The second labeler will receive the same definitions and decision
rule but will not see my labels before assigning their own.

**Why this target:**
Seeking support and venting can overlap, so some disagreement is
expected. Agreement below 75% would prompt a review of ambiguous
definitions and boundary cases. Disagreements will be recorded
rather than hidden by changing the original cold labels.

## 5. Confidence and correctness

Among held-out test predictions with model confidence of at least
0.70, at least 80% will be correct.

Predictions below 0.70 will be marked "needs review" in the
evaluation report while retaining their predicted labels.
They will remain included in overall accuracy and per-label F1.

At least 10 held-out test predictions must have confidence of
0.70 or higher. If fewer than 10 qualify, this criterion will
be marked as insufficient evidence rather than passed.
The number of qualifying predictions will always be reported.

**Why this target:**
The high-confidence group should be more accurate than the 65%
overall target. This checks whether the chosen confidence threshold
identifies a more reliable subset. Reporting the group size prevents
a high percentage based on very few predictions from being
presented without context.I chose a minimum of 10 because the expected test set contains
about 30 posts. This requires roughly one-third to qualify and
avoids judging the 80% target from only one or two predictions.
The result will still be sensitive to individual mistakes.

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
