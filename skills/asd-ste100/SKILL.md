---
name: asd-ste100
description: Write reader-facing technical content — Linear issues, project docs, change summaries, PR descriptions, announcements — in Simplified Technical English (ASD-STE100), stripped of conversation-local context. Use whenever compiling the results of a working conversation into content for readers who were not part of that conversation.
---

# ASD-STE100 Technical Writing

Produce content that a reader with zero knowledge of the source conversation can understand on first read. There are two failure modes to prevent:

1. **Context leakage** — names, framing, and narrative that only make sense inside the conversation that produced the content.
2. **Complex prose** — long sentences, passive voice, synonym variation, idiom.

Do the steps in order. Step 1 is about *what* the content says; step 2 is about *how* it says it.

## Step 1: Strip conversation context

Before you write, remove every artifact of the working conversation:

- **Invented names.** Nicknames, codenames, and metaphors coined during the conversation ("the zombie handler", "option B", "the nuclear approach") do not exist to the reader. Replace each one with the real identifier or a plain description.
- **Discovery narrative.** Remove "we realized", "it turns out", "after some digging", "as discussed", "interestingly". State each finding as a fact. The reader needs the conclusion, not the journey.
- **Dead theories.** Do not mention approaches that were considered and rejected, unless the rejection itself must be documented. If it must, put it in an "Alternatives considered" section with the reason it was rejected, stated as fact.
- **Conversational tone.** Remove humor, emphasis ("critically", "huge"), hedging ("probably fine", "should work"), and any reference to the conversation, the author, or the assistant.
- **Unstated context.** Every system, service, or term you reference must be either standard knowledge for the team or defined at first use.

**Test:** an engineer who joins the team today and reads only this content must understand what it says and why it matters.

## Step 2: Write in Simplified Technical English

Apply these rules to every sentence. The full rule digest with before/after examples is in [reference.md](reference.md).

**Sentences and paragraphs**
- Maximum 20 words in an instruction sentence. Maximum 25 words in a descriptive sentence.
- One instruction per sentence.
- One topic per paragraph. Maximum 6 sentences per paragraph.

**Verbs and voice**
- Use the active voice. Name the agent that does the action.
- Use only simple tenses: past, present, future. Do not use perfect or progressive tenses.
- Use the imperative for instructions: "Run the migration", not "The migration should be run".
- Do not use "-ing" verb forms, except inside technical names.

**Words**
- Use one term for one concept, spelled the same everywhere. Never vary terms for style.
- Keep code identifiers, API names, file paths, and error text verbatim, in backticks. Technical names are exempt from all word rules.
- Do not use idioms, slang, or Latin abbreviations (write "for example", not "e.g.").
- Do not chain more than 3 nouns. Break long noun clusters apart.
- Keep the articles "a" and "the". Do not write in telegraph style.

**Structure**
- Use a vertical list for any sequence of steps or set of more than 2 items.
- Put a warning or precondition before the step it applies to, never after.

## Step 3: Verify

Check the finished content against this list. Fix every failure before you return it.

- [ ] No invented names from the conversation remain.
- [ ] No discovery narrative remains.
- [ ] Every sentence is within the word limits.
- [ ] Every instruction is imperative and active.
- [ ] Each concept has exactly one name throughout.
- [ ] The content passes the new-engineer test from step 1.

## Shape for Linear issues

- **Title:** one imperative sentence or noun phrase, maximum 10 words, no punctuation flourishes.
- **Body sections, in order:** Problem, Cause (only if known), Change, Acceptance criteria. Omit a section rather than pad it.
- Acceptance criteria are a vertical list. Each item is one testable statement.

> This skill applies the writing rules of ASD-STE100 adapted for software documentation. It does not enforce the licensed STE dictionary; software technical terms are treated as technical names.
