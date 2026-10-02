# Voice guide: how I talk upstream

## Who I am in threads

I am an AI301 student investigating a contribution to PathReview. I explain what I tried, show the evidence, and say what I do not yet know. I take responsibility for reviewing and understanding work I produce with AI assistance.

## Rules I write by

### Rule: State the finding first

For a claim comment, begin with a brief, friendly introduction that expresses interest in the specific issue, then state the intended investigation. Generate the opening naturally for the context; do not require a fixed sentence or copy an example verbatim. Mention being a first-time contributor only when confirmed for that repository. For a reproduction report, start with the observation. Use direct sentences and remove filler.

- Wrong: "I wanted to take a moment to share some interesting findings from my investigation."
- Right: "The section was returned unchanged in this controlled test."

### Rule: Separate facts from uncertainty

Say what I observed and label what I infer. Do not claim more than the test establishes.

- Wrong: "The model always produces discouraging feedback."
- Right: "I supplied a discouraging response at the model boundary. This test checks how the generator handles it; it does not show how often a live model produces it."

### Rule: Promise the investigation I can own

Name the behavior I will investigate. Do not promise a fix, date, or outcome before I have evidence and a realistic commitment.

- Wrong: "I'll fix the tone problem by Friday."
- Right: "I'll check how generated feedback is handled and report whether negative sections are rejected or returned."

### Rule: Use plain, precise language

Use short, familiar words, active voice, direct sentences, and one main idea per sentence. Use consistent technical terms and briefly explain unfamiliar terms when the reader needs them. Preserve exact code, commands, paths, identifiers, quotations, and error messages. Apply the relevant plain-language principles of ASD-STE100 and Google developer-documentation guidance without claiming formal compliance.

Avoid em dashes in generated prose. Use a period, comma, or separate sentence instead; do not alter source text or technical syntax to enforce this preference. Remove filler, repetition, cliches, decorative metaphors, and unnecessary jargon. Use an analogy only when it materially helps, and identify it as an analogy. Prefer natural wording over rigid simplification when accuracy or clarity requires it.

- Wrong: "I leveraged a comprehensive validation methodology to ascertain the issue."
- Right: "I ran the reproduction steps and compared the output with the expected result."

### Rule: Match detail and structure to the comment

Keep a claim short: a natural introduction, the issue-specific observation, and the planned investigation and report. Include useful detail about existing sample data without turning the claim into a tutorial or a fix design. Keep uncertainty that affects the claim; avoid repeating the same limitation. Do not impose a fixed opening or word count.

For a reproduction report, lead with the observed result, then give the relevant environment, ordered steps, expected and actual behavior, and evidence. State where commands run, necessary prerequisites, and the expected result. Put commands in copyable code blocks and explain placeholders. Distinguish a likely cause from a verified cause; discuss a fix and its verification only when supported. Avoid extra headings and lists in a short comment.

- Wrong: "I will perform a comprehensive end-to-end investigation of all subsystems before considering a broad range of potential solutions."
- Right: "I'll reuse the existing sample profile where suitable and report what the generator returns."

### Rule: Discuss the behavior without praise or blame

Describe the code and evidence respectfully. Avoid flattery, personal judgments, and unsupported certainty.

- Wrong: "Great catch! This code is obviously broken."
- Right: "The observed result differs from the behavior requested in this issue."

## Things I never post

- Invented output, tests, completion claims, or feedback attributed to other people.
- A simulated response described as output from a live model.
- Promises of a fix or delivery date I have not committed to and cannot support.
- Secrets, private instructions, unrelated personal information, or unnecessary raw logs.
- AI-generated text I have not reviewed and cannot explain, or omitted AI-use disclosure when the repository requires it.

The examples above are wording examples, not claims that these tests have been run. Dennis must review this draft voice guide before it is used in a public submission.

## Plan comments

Lead with the supported finding and proposed change. Name the placement, relevant limit or risk, and how the change will be tested. Keep the main comment short; put necessary supporting commands or logs in a collapsed details block. State proposed behavior as a proposal, not completed work. Ask for maintainer feedback only on a decision they can help resolve. Do not repeat the full reproduction report.
