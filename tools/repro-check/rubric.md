# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| issue-specific-claim | Claim comment compared with the issue description and relevant thread context; Evidence guide: Comms. | The claim identifies the particular behavior or request being investigated and a relevant next step. A generic offer to help is insufficient. It does not promise a fix or deadline beyond the author's established ability to deliver. | required |
| environment-recorded | Repro report's environment record compared with the issue's target; Evidence guide: Environment. | The report identifies the revision or version tested and the runtime, platform, configuration, and dependencies material to this behavior. Material differences from the issue's setup are disclosed. Do not require unrelated environment details. | required |
| steps-rerunnable | Repro report's setup, inputs, commands or actions, and trigger; Evidence guide: Steps. | A reader can repeat the investigation from the stated starting state without inventing a material input or missing action. Necessary fixtures or their contents are supplied or retrievable. A documented setup reference is sufficient when the report identifies the relevant procedure and any deviations. | required |
| issue-matched-evidence | Output, logs, screenshots, or test results in the report, compared with the issue's described behavior; Evidence guide: Behavior shown. | Evidence demonstrates the reported behavior, or documents a relevant attempt that did not reproduce it. An unrelated failure, setup error alone, or unsupported assertion of success is not proof of the target behavior. Controlled or simulated inputs are identified, and conclusions stay within what the exercised code path establishes. | required |
| honest-outcome | Report's conclusion and expected/observed comparison against its artifacts and stated limits; Evidence guide: Honesty. | The conclusion accurately states what occurred, including cannot-reproduce or partial findings when warranted. It does not turn a hypothesis into a proven cause, a simulation into a live observation, or a narrow result into a general guarantee. An evidenced cannot-reproduce is not a failure merely because the original behavior was absent. | required |
| repo-conventions | Claim and repro comments against the issue context, repo-facts policy statements, and applicable contribution instructions; Evidence guide: Comms. | The comments follow applicable communication and contribution rules, including required AI-assistance disclosure and templates where mandated. No required disclosure is omitted. Verified policy silence does not create a requirement; unread or unavailable policy evidence is unclear. Apply scoped house rules only in live mode. | required |
| focused-report | Claim and repro text around the decisive evidence; Evidence guide: Comms. | The reader can identify the finding and the relevant evidence without unrelated logs, repeated narrative, or an unsupported solution proposal obscuring them. Judge clarity rather than length or heading count. | preferred |

## Verdict rule

`accept` only if every applicable `required` check is `pass`; otherwise `reject`, including any `unclear` required check. `preferred` checks do not change the verdict.

For a live claim-only draft, apply `issue-specific-claim` and `repo-conventions`. Mark checks requiring the reproduction report `unclear` with evidence `not yet applicable: claim-only draft`, and exclude them from the verdict. A full package, including every eval package, uses all checks. The personal voice guide is reported separately in live mode; it does not independently change this verdict.
