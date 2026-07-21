# instructional-voice-builder
An AI skill for university faculty who want to capture their instuctional tone and approach to draft communications and improve teaching presence in their courses. Works in Claude and OpenAI Codex; both follow the same SKILL.md standard.

**What this skill does**

The skill builds a personal instructional voice profile from two inputs: a short interview about how you communicate with students, and 3 to 5 samples of your teaching-related writing. The output is one file, instructional-voice.md, saved to your project root. Claude then follows this profile when drafting student-facing content.

The skill is discipline agnostic and platform agnostic. Supported formats include:


LMS announcements
Emails to students
Lecture and video scripts
Feedback on student work
Syllabus text
Discussion replies
Slide notes


**How to use**


Install the skill (see below).
Start a new project and say "capture my teaching voice", or drop a batch of your teaching writing into chat. The skill starts the interview immediately.
Answer the interview questions and share 3 to 5 writing samples. Good samples: an announcement you wrote, feedback you gave a student, a syllabus section, a lecture script.
The skill writes instructional-voice.md into your project. From then on, drafts follow your voice.


**Installation**

First download this repository as a ZIP (green Code button, then Download ZIP) and unzip. Then follow the step for your tool:

Claude desktop app (Cowork): add the instructional-voice-builder folder under Settings, Capabilities, Skills.

Claude Code: copy the instructional-voice-builder folder into .claude/skills/ in your project, or into ~/.claude/skills/ for use across all projects.

OpenAI Codex CLI: copy the instructional-voice-builder folder into .codex/skills/ in your project, or into ~/.codex/skills/ for use across all projects. Trigger with /instructional-voice-builder, or let Codex activate the skill automatically when your request matches.

**Who made this**

Built by Charlotte von Essen, Pedagogy and Digital Development Lead at the Stockholm School of Economics. Questions and suggestions are welcome via GitHub issues.

**License**

Reuse and adapt freely with attribution.
