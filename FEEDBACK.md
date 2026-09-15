# Overnight review: Larkspur disruption-care agent

**To:** room16  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-09-15 12:58

## Priya's note

> Our vendor says we should just be using your best model.
>
> Why aren't we?
>
> Priya Raghavan, Larkspur Airlines

She sent that before this session opened. She means it. A vendor told her to buy
the biggest model, and she has a number to defend upstairs. Her four questions from
day one are still open. Naming a model answers none of them.

## Still open from day one

| Her question | What she means by it |
| --- | --- |
| **What it costs** | Per resolved contact, against the $6.90 a human contact costs us. |
| **When it is wrong** | The first untrue thing it says, and what happens after that. |
| **Who runs it** | In June, after you have left. |
| **What you left out** | The scope you cut, and why. |

## What the review agent found

Overnight, Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. search_alternatives in agent.py still carries the description string "search", 6 characters, unchanged by this pod's diff.**

The static scan flags this tool description as under 40 characters, and it is the tool Claude must pick to find rebooking options after a cancellation. The diff this pod wrote touches TONE_ADDENDUM, EXTRA_TOOLS, LOCAL_TOOLS, and tool_list(), but never this string. Whatever model sits behind this loop, it is choosing among nine tools and one of the load-bearing ones is described in a single word.

Run python3 run.py --show-tools and paste the printed description for search_alternatives.

**2. agent.py adds one local tool, flag_sensitive_case, and its description tells the model to consult a document nothing in the repo provides.**

The tool's description in the diff instructs escalation to reference 'fare_rules section 7,' and _flag_sensitive_case repeats that instruction in its returned reason string. No fare_rules file, table, or section appears anywhere in agent.py, support/mcp_server.py, or the file list for this review. The keyword matching behind it is three word lists (minor/child/unaccompanied/umnr, medical/wheelchair/oxygen/ssr/disability, threat/abus/rude/angry/lawsuit/lawyer), not a model call.

Run python3 verify.py 4.1 and paste the result, or grep -rn fare_rules across the repo and paste what matches.

**3. support/mcp_server.py is a given file this pod modified, and tool_list() now calls mcp_client.tools() with no committed run showing what that returns.**

The diff adds mcp_client.tools() to tool_list() alongside build_tools() and EXTRA_TOOLS. The file list marks support/mcp_server.py as differing from the shipped pack, which changes what any verify.py or eval_harness.py number would mean here. There is no readout-trace.json in the repository, so nobody has captured what tool_list() actually returns with this change in place.

Run python3 run.py --show-tools and paste the full tool list including anything mcp_client.tools() contributes.

**4. run_agent's loop fix in agent.py changes what gets appended to messages, but no trace or eval case shows the corrected loop actually running.**

The diff changes the assistant-turn append from text_of(response) to response.content, and changes the return value from answer to text_of(response). This is a structural fix to the tool loop's message history, sitting inside a while loop still bounded by MAX_TOOL_CALLS = 8. There is no readout-trace.json and no evals/cases.json in this repository, so nothing demonstrates this loop completing a multi-tool disruption case end to end.

Run python3 run.py K7PQ2M --trace and paste the full transcript.

**5. TONE_ADDENDUM in agent.py is still 0 characters and PITCH.md is still the unedited template.**

The static scan confirms TONE_ADDENDUM at zero characters, and the diff this pod submitted does not touch it. PITCH.md is byte-identical to the shipped template, so no case for model choice, cost, or tradeoff has been written down anywhere in this repository yet. Whatever argument the team makes to Priya about needing a specific model has to come from evidence that does not exist here yet.

Run python3 bench.py --compare <a> <b> once a baseline exists and paste the comparison output.

## Your four answers

The four lines under `## Priya asked` in your PITCH.md are still empty. They
are one line each and they are not a coding job: cost, what happens when it is
wrong, who runs it in June, and what you left out. Whoever on your side is not
editing agent.py is the right person to write them, and they are the four
things I will ask about first.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

## What this review read

- `agent.py (286 lines)`
- `PITCH.md (unchanged template)`
- `TEAM.md`
- given files that differ from the shipped pack: `support/mcp_server.py`

Reviewer: `claude-sonnet-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
