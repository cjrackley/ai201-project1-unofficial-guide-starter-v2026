# The Unofficial Guide

Name: Cameron Rackley
Corpus: practice - 26 chunks total
> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

## What This Does

<!-- Three or four sentences. Which corpus you picked, and the kinds of
     questions your system answers. Write it for someone who has never seen
     this repo.

     Milestone 5. -->

This is a RAG system that uses a library of information called a corpus. The system breaks the corpus library into chunks for it to be easily readable by the system. Asking a question related to the corpus library should result in a valid answer, if a question is too vague, off topic or the corpus doesn't have adequate information to be answered, it will be rejected.

## Chunking Strategy

**Chunk size: N/A**
**Overlap: N/A**

My chunking strategy is different from the chunk size and overlap. I asked claude what were some ways the chunks could be generated and we came up with a chunking strategy that works for the practice corpus. Chunks are split by the heading, there is always 1 heading with each chunk, a chunk ends when a double linebreak is detected after a punctuated sentence.

<!-- What about YOUR documents made you pick these numbers? Short posts and
     long sectioned guides don't want the same chunking, and "800 seemed
     reasonable" earns nothing. Point at something you noticed when you read
     the documents in Milestone 1.

     If you changed your mind partway through, say so and say why. That's worth
     more than pretending you got it right first time.

     Milestone 3. -->

## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->

**Chunk 36** — source:  `` — produced by: `chunker.py::split_documents`

The last few turns

The deck running out ends the game, so count what is left in it once it looks
thin. A contract you cannot finish before the deck empties is worth one coin to
discard and nothing to keep. Crew tokens are two points each if unspent, which
means spending your last token to squeeze out a two-coin sale is exactly break
even, and spending it to complete a contract is clearly worth it. Deciding that
in advance is easier than deciding it under time pressure.

**Chunk 19** — source: `board_game_port_reference.txt#0` — produced by: `chunker.py::split_documents`


Which port accepts what

The six ports each accept two cargo types, printed on the board. Reading from the start of the coast track: timber and salt; salt and wool; wool and fish; fish and iron; iron and timber; and the sixth port accepts any two types chosen at setup.

The sixth port being flexible is what makes the far end of the track worth reaching.

**Chunk 16** — source: `board_game_house_rules.txt#3` — produced by: `chunker.py::split_documents`


Crew variants

The most common house rule is starting with four crew tokens instead of three.
It makes early turns more flexible and slightly cheapens the two points an
unspent token is worth at the end, since there is one more of them. A table that
finds the crew decision too painful will like it. A table that likes the
decision should leave it alone, because the tension between using a token now
and scoring it later is deliberate and is most of what the tokens are for.

**Chunk 6** — source: `board_game_designer_notes.txt#0` — produced by: `chunker.py::split_documents`

Why the rules are like this

The two-action limit exists to keep turns short. An earlier version allowed three actions and games ran past two hours.

Crew tokens scoring two points if unspent is deliberate tension: the tokens are most useful exactly when you can least afford to lose the points.

**Chunk 2** — source: `board_game_common_errors.txt#0` — produced by: `chunker.py::split_documents`


Rules people get wrong

Hold capacity is three cards, not three of each type. Crew tokens give an extra action, not an extra turn.

The market row is refilled immediately after a card is taken, not at the end of the turn. This matters more than it sounds.

## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->

**Question:**
 Should I focus on getting coins or contracts?
**Answer:**
Answer using only the documents above, and name the file you used.
======================================================================

You should focus on getting contracts rather than coins, because coins rarely decide a game while contracts usually do. 

Source: `board_game_scoring_example.txt` (and similar information in `board_game_strategy_guide.txt`)

Sources retrieved: board_game_rules_walkthrough.txt, board_game_scoring_example.txt, board_game_strategy_guide.txt

```
```

**My relevance cutoff: .65**

My group of accepted questions only got up to .529, short of the cutoff. That was my more complicated question for the corpus, and since it met the cutoff I don't believe the cutoff needs to be shifted too much. I raised it to give just a little more room for relevance without going too far, since all the rejected questions had a distance of .87 or above
<!-- The number you set in config.py, and how you got there.

     You ran five questions your corpus covers and the five in OUT_OF_SCOPE
     that it clearly doesn't, and wrote down the best distance for each. What
     did those two groups look like? Where was the gap? Put the actual numbers
     here — the table below wants all ten rows.

     Milestone 4. -->

| Question | In corpus? | Best distance |
|what pages are examples in the rulebook?|yes|.481|
|Can Harbourmaster be played solor?| yes |.296|
|Should I focus on getting coints or contracts?|yes|.529|
|What actions can i use during my turn?|yes|.445|
|What cargo types are accepted at the fourth port?|yes|.280|
|what is the capital of mongolia?|no|.967|
|How do I change the oil in a diesel engine?|no|.873|
|Who won the 1994 World Cup?|no|.876|
|what is the recommended dosage of ibuprofen for a headache?|no|.875|

## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

**1.**
I asked claude to explain the syntax of the chunker and ways I could change it. It explained each line of code along with the parameters and where the data was coming from and going to. This led into the next use of claude for this assignment.
**2.**
I asked claude what the best chunking size would fit the practice corpus best. It told me the best chunking size would be 800 and the overlap be 300, with these set it would lead to fewer chunks with useless information. I didn't feel like it fit right, so I asked claude to find a better way to chunk the corpus. It came up with the method of starting every chunk with a header with its respective data, which is where it would end.
<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 5 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 2. Every answer names a source | 5 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 4. Total character count from all chunks should not exceed 2000 characters| 4 of 5 | 4 of 5 | 4 of 5 | 4 of 5 | MET |
| 5. Responses are well put together, with sources just at the end.| 4 of 5| 3 of 5 | 4 of 5| 0 of 5 | MISSED |

<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->

1. What pages are examples in the rulebook? — run 1

- Best distance: 0.4808 (passed the gate)
- Sources retrieved: board_game_components.txt, board_game_history.txt, board_game_house_rules.txt, board_game_rules_walkthrough.txt, board_game_teaching_new_players.txt


Pages six and seven are examples in the rulebook (from board_game_components.txt and board_game_teaching_new_players.txt).

output contains a chunk with the answer

2. Can Harbourmaster be played solo? — run 1

- Best distance: 0.2962 (passed the gate)
- Sources retrieved: board_game_rules_walkthrough.txt, board_game_scoring.txt, board_game_setup.txt, board_game_solo.txt, board_game_variants.txt


Yes, Harbourmaster can be played solo by playing with two boats and alternating turns between them to try to score more than 40 points across both. 

Source: `board_game_solo.txt`

output contains a named source

3. The relevance gate on out-of-corpus questions

Produced by `run_eval.py::check_out_of_scope`, cutoff 0.65. Refused 5 of 5.

output contains evidence of out of scope questions being refused

4. Should I focus on getting coins or contracts? — run 1

- Best distance: 0.5292 (passed the gate)
- Sources retrieved: board_game_rules_walkthrough.txt, board_game_scoring_example.txt, board_game_strategy_guide.txt


You should focus on getting contracts rather than coins, as coins rarely decide a game while contracts usually do. 

Source: board_game_scoring_example.txt (and also mentioned in board_game_strategy_guide.txt)

Total sum of chunk characters used for this result is 2,076, above 2,000 characters allowed failing the criterion.

5. Should I focus on getting coins or contracts? — run 3

- Best distance: 0.5292 (passed the gate)
- Sources retrieved: board_game_rules_walkthrough.txt, board_game_scoring_example.txt, board_game_strategy_guide.txt


You should focus on getting contracts rather than coins. Coins rarely decide a game, whereas contracts usually do (board_game_scoring_example.txt). Between one more sale and one more delivery, you should deliver (board_game_strategy_guide.txt).

Output contains sources throughout the explanation, not just at the end, so this fails the criterion

## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | Retrieved chunk contains the answer | MET | Every answer contains a chunk with the answer |
| 2 | Every answer names a source | MET | Every answer either names a source inline or after the explanation |
| 3 | Gate stops out-of-corpus questions | MET | All 5 out of scope questions were rejected |
| 4 | Total character count from all chunks should not exceed 2000 characters | MET | Only 1 of 5 responses contained chunks that exceeded the 2,000 character sum |
| 5 | Responses are well put together, with sources just at the end | MISSED | The entire 3rd run gave explanations with 1 or more inline sources, which muddy the answer, so it fails. |

## Diagnoses

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->

     The only criterion missed was #5. The criterion almost entirely relies on the "chat" part of the bot. This is why it's happening accross all questions throughout the 3 runs, because it's not dependant on the answer itself. This leads me to believe the cause of these missing comes from the generation stage, specifically the grounding instructions. One of the rules is 'Name the document your answer came from, using the filename given in each excerpt.' which isn't specific on where the sources should be placed.

## The Improvement

**What I changed:**

**Why I picked it:**

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |  |  |  |  |
| 2. Every answer names a source | 5 of 5 |  |  |  |  |
| 3. Gate stops out-of-corpus questions | 4 of 5 |  |  |  |  |
| 4. Total character count from all chunks should not exceed 2000 characters| | | | | |
| 5. Responses are well put together, with sources just at the end.| | | | | |

**Did it help?**

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

## What's Still Broken

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

## What I'd Do Differently

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->
