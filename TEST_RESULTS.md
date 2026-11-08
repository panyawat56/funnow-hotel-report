# Test results

These are the results of runs on 5 and 8 November 2026, using `gemini-3.5-flash-lite` and the mock data supplied with the assignment. The numbers come from one person's testing and one week of data. They show what was tried, and they don't prove the system never makes a mistake.

## Bad data

| Input | Result |
|---|---|
| `week_start` is not last week | The whole run stops |
| A required column is missing | The whole run stops |
| The sheet has no data | The whole run stops |
| Owner email is missing | That hotel goes to a reviewer and is left out of the median |
| Revenue is text | That hotel goes to a reviewer and is left out of the median |
| Revenue is negative | That hotel goes to a reviewer and is left out of the median |
| Revenue and orders are 0 | That hotel goes to a reviewer and is left out of the median |
| `target_revenue` is not a positive number | That hotel goes to a reviewer and is left out of the median |
| Fewer than 5 usable hotels | Every hotel goes to a reviewer |
| Free-text note in row 14 | Ignored, and not counted as a hotel |

## Deliberately wrong AI drafts

Each draft below was inserted in place of the AI's answer. The check caught all 8 and passed the one correct draft.

| Inserted text | Why the check rejected it |
|---|---|
| "Your revenue of 428,000 is above usual." | It has a number |
| "Your revenue is below the usual range" for a hotel with nothing low | The status doesn't match, and nothing is low |
| "Orders are below usual too" for a hotel with orders in range | Wrong status for orders |
| "orders are in range" for a hotel with orders above usual | Wrong status for orders |
| "close to Sky Spa" in another hotel's email | It names another hotel |
| "driven by fewer orders" | It invents a cause |
| "for similar hotels" | It claims data we don't have |
| "Revenue per order is below usual too" for a hotel with it in range | Wrong status for revenue per order |

## Real AI drafts

| Measure | Result |
|---|---|
| Runs inspected | 6 |
| Drafts | 54 |
| Rejected by the check, so the template was used | 2 |
| Wrong sentences that passed the check | 2 |

The prompt and check changed between these runs, so this is a record of what happened and not a rate for the final version.

The 2 sentences that passed were:

- "higher than usual for similar properties": false, because the group is all partner hotels. The check now rejects "similar".
- "below the target for this group": a target belongs to one hotel. It came from a test with sample goals, and it is not fixed, because the mock sheet has no goals.

A word list can only catch what it lists, which is why needs-improvement emails still go to a person.

## End-to-end runs

| Test | Result |
|---|---|
| Full run on the mock sheet, 5 Nov | 10 emails sent: 5 to owner addresses and 5 to the reviewer |
| Full run with the latest version, 8 Nov | 10 emails sent: 6 to owner addresses and 4 to the reviewer. All 9 AI drafts passed the check, so no template was used |
| Wrong date in the sheet, with the workflow live | The run stopped before any report email, and the alert workflow ran |
| Run time with AI calls | 46 seconds to 5 minutes for 10 hotels (74 seconds on 8 Nov) |

The 5 Nov full run used an earlier version of the AI prompt. The 8 Nov run used the latest version and was started by hand for the demo video; the schedule is set for every Monday at 09:00.
