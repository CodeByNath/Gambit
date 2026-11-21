# Gambit — handover for a new chat
Updated: 21 November 2026. Repository: https://github.com/CodeByNath/Gambit (public), default branch `main`. Live app: https://codebynath.github.io/Gambit/.

## Owner's objective and boundaries
Keep Gambit simple. The core signal is **a horse's own total time to complete a race distance**—not its finishing place, bookmaker odds, last-600m split, or the winning race time misattributed to the horse. Compare **the exact upcoming distance first**: personal best, other same-distance records, recent time and consistency. **Only if no exact-distance records exist**, use the closest distance and label any equivalent-duration projection clearly. Do not let projections override exact-distance evidence. Do not add unrelated features or change the method without owner approval.

## What actually exists in GitHub
- `index.html`: single-file Stage 1 horse profile editor. Horse name, weight, multiple historical races; date, track, condition, distance, finishing position, number of runners, winning race time, margin (lengths), optional last-600m. Displays estimated individual completion time in race history. Search/edit/delete, JSON export.
- `data/horses.json`: public JSON store; **currently `[]`** at verification. Do not claim the screenshots were loaded into GitHub.
- Browser saves changes in localStorage first. Public data loads from GitHub; writing back uses an optional fine-grained, repo-scoped GitHub token manually entered on the page. Token is not stored. Check edit/update and sync behaviour before relying on it; browser storage and remote repository are different states.
- The app uses `estimated_time = winning_time + beaten_lengths * 0.17s`. **0.17 seconds/length is an approximate assumption, not an officially measured individual time.** Preserve raw winning time, margin and the estimate distinctly. Last 600m is separate.
- Stage 2 race builder (browse/select horses or create-and-add) and fastest/slowest tools are **future scope, not implemented**.

## Analysis method requested
For each runner in an upcoming race:
1. Gather **individual** full-distance times or explicitly labelled estimates and dates.
2. Use **all available races at today's exact distance**, including personal best and latest/recent pace. Verify data interpretation first.
3. When no exact-distance history exists, use closest race distance and explicitly mark the projection as uncertain. Separate trials from official races.
4. Compare entrants, identify the best six; establish the **strongest three from exact-distance and recent evidence**, not from old projected personal best alone. Never claim 90% or any other win probability without validation.
5. Backtest using only data available **before** each completed race; record results without hindsight selection.

## Bet-combination structure discussed (not implemented)
Six different horses each appear once as the **Win** leg, across six single-race multis. Each multi has **1 Win + 3 other horses Top 5**. For winner selections among the strongest three, use the other two strongest as Top 5 plus one from the remaining three. For winner selections among the remaining three, use all strongest three as Top 5. The owner wants to evaluate this across several races. This structure does not guarantee a profitable outcome; compare full-multi successes and stakes, not just whether a winner was included.

## Lessons from past tests
- Wangaratta 1000m: repeated assistant errors used winner times as individuals, relied on placing and projected records, and produced losing combinations. Do not repeat.
- Narrogin 1100m: #7 Pariah's Thanks won; #1 Casino Royale placed fifth and #10 What Have You Done fourth. #6 Mantua finished eighth and spoiled a multi. Mantua had **three actual 1100m records** (estimated 65.64s, 65.26s, 64.85s), yet was incorrectly ranked high using a projected 1000m personal best (63.66s equivalent). Do not assert hindsight alternatives were pre-race predictions.
- Owner needs clear, concise answers and strict adherence to the chosen method; do not overcomplicate or invent certainty.

## Next chat
Start by reading this handover and inspecting `index.html` and `data/horses.json` on `main`. Ask what specific next change or analysis the owner wants; do **not** implement Stage 2 or change betting logic unprompted. Validate calculations and deployed behaviour separately from repo commits.
