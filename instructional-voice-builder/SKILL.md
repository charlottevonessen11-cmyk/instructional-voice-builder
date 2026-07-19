---
name: instructional-voice-builder
description: Build a personalized instructional voice profile for university faculty from a short interview plus 3 to 5 samples of their teaching-related writing. Discipline agnostic and platform agnostic. Works for any student-facing format including LMS announcements, emails to students, lecture or video scripts, feedback on student work, syllabus text, discussion replies, and slide notes. Use this skill at the start of any project where a faculty member wants AI to learn how they sound as a teacher before drafting course content. Trigger whenever the user says "capture my teaching voice", "learn my instructional voice", "build my faculty voice", "I want my course materials to sound like me", "train on my teaching materials", or drops a batch of teaching-related writing into chat at the start of a project. Also trigger for faculty using AI for the first time who need a voice foundation before drafting any student-facing content. Always produces one file (instructional-voice.md) saved into the project root.
---

# Instructional Voice Builder

## CRITICAL: Auto-start on load

The moment this skill loads, installs, or triggers, you MUST immediately run Step 1 below. Your very next message to the user is the interview questions. Nothing else.

Do NOT:

- Summarize this skill
- Describe what file it creates
- Explain how it works
- Ask if the user wants to run it
- Confirm installation
- Offer options like "want me to run this now?"

Do THIS:

- Go straight to Step 1
- Send the interview questions as your first and only response

This applies whether the user uploaded a .skill file, said "capture my teaching voice", pasted samples, or triggered the skill any other way. No preamble. Interview first.

## Step 1. Run the teaching interview

You MUST call the AskUserQuestion tool. Do not type the questions as chat text. The tool renders as an interactive form, a better experience than typing answers into chat.

AskUserQuestion supports a maximum of 4 questions per call, so send two calls: Batch 1 first, wait for answers, then Batch 2.

### Batch 1 (your very first action, no text before it)

Call AskUserQuestion with this structure for the questions parameter:

```
[
  {
    "question": "What is your name, discipline, and role?",
    "header": "About you",
    "multiSelect": false,
    "options": [
      {"label": "Professor", "description": "Full professor or chair"},
      {"label": "Senior lecturer", "description": "Associate professor, senior lecturer, or docent"},
      {"label": "Lecturer", "description": "Assistant professor, lecturer, or postdoc who teaches"},
      {"label": "Adjunct or guest", "description": "Practitioner, adjunct, or visiting faculty"}
    ]
  },
  {
    "question": "Who do you teach?",
    "header": "Students",
    "multiSelect": true,
    "options": [
      {"label": "Undergraduates", "description": "Bachelor-level students"},
      {"label": "Master's students", "description": "Graduate coursework students"},
      {"label": "Doctoral students", "description": "PhD students and research supervision"},
      {"label": "Executive learners", "description": "Professionals in executive or continuing education"}
    ]
  },
  {
    "question": "Which formats does your instructional writing appear in most?",
    "header": "Formats",
    "multiSelect": true,
    "options": [
      {"label": "Announcements", "description": "LMS announcements, course pages, weekly updates"},
      {"label": "Student emails", "description": "Individual and group messages to students"},
      {"label": "Lecture scripts", "description": "Spoken or recorded instructional content, video scripts"},
      {"label": "Feedback", "description": "Comments on student work, rubric feedback, exam responses"}
    ]
  },
  {
    "question": "What do you believe about teaching and learning that shapes how you communicate with students?",
    "header": "Stance",
    "multiSelect": false,
    "options": [
      {"label": "Struggle builds learning", "description": "Students learn by wrestling with hard problems, and my communication protects productive difficulty"},
      {"label": "Clarity above coverage", "description": "Better to teach fewer things well; my communication cuts noise"},
      {"label": "Connection comes first", "description": "Students learn from teachers they trust; my communication builds relationship"},
      {"label": "High expectations, high support", "description": "I demand a lot and back students to meet the bar"}
    ]
  }
]
```

### Batch 2 (send immediately after Batch 1 answers return, no commentary between)

Call AskUserQuestion again with:

```
[
  {
    "question": "How do you want students to describe your presence after a semester with you?",
    "header": "Presence",
    "multiSelect": false,
    "options": [
      {"label": "Approachable", "description": "Easy to talk to, human, low barrier to asking questions"},
      {"label": "Demanding but fair", "description": "High standards, transparent rules, no surprises"},
      {"label": "Energizing", "description": "Brings the subject alive, students leave motivated"},
      {"label": "Calm and structured", "description": "Steady, organized, students always know where they stand"}
    ]
  },
  {
    "question": "What do you refuse in student-facing communication?",
    "header": "Off limits",
    "multiSelect": true,
    "options": [
      {"label": "Unexplained jargon", "description": "No discipline terminology without a plain-language bridge"},
      {"label": "Scolding tone", "description": "Never shame students, even about missed deadlines or weak work"},
      {"label": "Forced enthusiasm", "description": "No exclamation-mark cheerfulness, no emoji, no hype"},
      {"label": "Vague praise", "description": "No 'great job' without saying what was good and why"}
    ]
  }
]
```

After both batches are answered, move to Step 2. If any answer is blank or skipped, ask that specific question once more in chat, then move on.

## Step 2. Ask for the samples

Say this:

> Now paste 3 to 5 pieces of your own student-facing writing. Mix formats if you have them: an LMS announcement, an email to a student or class, written feedback on an assignment, a lecture or video transcript, syllabus text, a discussion reply, or slide notes. One piece per message or all at once. Lecture transcripts are welcome; I will treat spoken and written registers separately. If you have no samples ready, type "exercise" and I will give you three short writing prompts instead.

Wait for the user to paste. Minimum 3 samples before analysis. If they paste fewer than 3, ask for more.

If the user types "exercise", give these three prompts and use the responses as samples:

1. Write the announcement you would post if you had to move an assignment deadline by one week.
2. Write feedback for a student submission with a strong core idea and weak execution.
3. Explain one core concept from your course to a student meeting it for the first time, in about 150 words.

## Step 3. Analyze the samples

Read every sample. Look for patterns across all of them, not quirks from one piece. If samples include both spoken transcripts and written text, analyze the registers separately and note where they differ. Extract:

**Voice signals**

- Average sentence length
- Paragraph rhythm (single line breaks, blank lines, dense versus airy)
- Tone (warm, dry, direct, formal, playful, understated)
- How the voice addresses students (first names, "you", collective "we", third person)
- Formality level and how it shifts between formats
- Signature phrases or recurring words
- Use of humour, and what kind

**Instructional signals**

- Explanation style: definition first, example first, analogy, story, question-led
- How concepts get scaffolded: what comes before the hard part
- How the voice handles logistics versus ideas (same register or different)
- Question use: rhetorical, genuine, Socratic, or none
- Feedback style: direct, question-led, strengths first, criteria-anchored
- How the voice encourages without inflating
- Authority balance: where the voice asserts, where hedging appears ("I think", "one view is")

**Structural signals**

- Length range per format
- How messages open (greeting style, context first, point first)
- How messages close (sign-off, next step, invitation to reply)
- Lists versus prose

**Absence signals**

- Words and punctuation consistently absent (for example, exclamation marks in 0 of 5 samples)
- Tones the voice never hits
- Moves the voice never makes (never apologizes for workload, never uses "as per the syllabus", never opens with "I hope this finds you well")

## Step 4. Write instructional-voice.md

Create instructional-voice.md in the project root. One integrated file covering identity, how the voice writes, and what the voice avoids.

```
# Instructional Voice Profile

## Who I am as a teacher
[Name, discipline, role, students taught, from the interview. 2 to 3 sentences.]

## Teaching stance
[The belief from the interview, written as a clear statement, plus the presence the teacher wants students to feel. 2 to 3 sentences.]

## Formats
[The formats this voice writes in, one line each, with any register differences observed between them, e.g. lectures looser than announcements.]

## Tone
[3 to 5 attributes the voice consistently hits, then 1 to 2 tones the voice never hits, drawn from gaps in the samples.]

## Sentence rhythm
[Average length, pacing, paragraph structure. Include avoidance patterns, e.g. no sentences over 25 words, never staccato fragments.]

## How I explain
[Explanation pattern with one example from the samples: definition first, example first, analogy, question-led. Note scaffolding habits.]

## How I address students
[Person, pronouns, names, formality, and how these shift by format.]

## How I give feedback
[Feedback structure observed in the samples: what comes first, how criticism is phrased, how praise is anchored. If no feedback samples exist, derive from the interview answers and mark as provisional.]

## How I open and close
[Opening and closing moves per format, 2 to 3 sentences. Note moves the voice avoids, e.g. never "I hope this email finds you well", never motivational sign-offs.]

## Signature phrases
[Recurring words or phrases from the samples.]

## Off limits
[Items from the interview refusals plus words, punctuation, or constructions absent from every sample. Only list items the samples clearly avoid, with counts, e.g. no emoji (0 of 5 samples).]

## What this voice never does
[3 to 5 specific behaviors drawn from gaps in the samples. Be specific. If the samples never scold about deadlines, list it. If they never use rhetorical questions, list it.]
```

Fill every section from the actual samples and interview. No generic filler. If a pattern is not present, say so. The Off limits and What this voice never does sections come from observation plus the interview refusals, never from a generic banned-words template.

## Step 5. Manual review of the output

Do not treat the profile as final. Walk the user through it for a manual check so they adjust anything before it becomes their reference.

1. Show the full contents of instructional-voice.md in chat, inside a plain code block.
2. Ask the user to review each section and flag anything wrong, missing, or overstated. Prompt them with specific checks: Does the tone list match how you see yourself? Are the off-limits items right? Did the analysis miss a habit you know you have? Is anything listed as "never" something you sometimes do?
3. Apply every requested change to the file, then show the changed sections and confirm.
4. Repeat until the user approves the profile. Only then move to Step 6.

If the user has no changes, ask once more before proceeding: "Nothing you would soften, sharpen, or remove?" First readings often approve too quickly.

## Step 6. Confirm and hand off

Tell the user:

> Your instructional voice profile is built and reviewed by you. One file is now in your project: instructional-voice.md. Every time you draft student-facing content in this project, I will reference it automatically. Open and edit the file anytime; your voice evolves and the profile should too.
>
> Test it now: ask me to draft an announcement, a piece of feedback, or a lecture segment in your voice, then tell me what sounds off. Each correction sharpens the profile.

## What this skill produces

One file in the project root:

- instructional-voice.md: who the teacher is, their stance, and an integrated voice profile covering positive signals (how the voice writes) and absence signals (what the voice avoids)

## Rules

- When this skill triggers, go straight to Step 1. No summary, no explanation, no preamble.
- Never skip Step 5. The user must manually review and approve the profile before hand-off.
- Work from what is in the samples. Do not invent patterns.
- Minimum 3 samples for pattern detection. Ask for more if fewer than 3.
- If samples contradict each other, note the contradiction in the profile rather than smoothing over.
- If samples span spoken and written registers, document both; do not average them into one.
- Keep instructional-voice.md under 600 words.
- American English throughout unless the samples show another variety.
- Never use em dashes in the profile or in any draft written from it.
- Output any sample text inside a plain code block (triple backticks, no language tag) so formatting survives copy-paste.
- This skill is discipline agnostic and platform agnostic. Never assume a specific LMS, field, or country; take all specifics from the interview and samples.
