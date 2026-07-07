---
name: linkedin-anti-slop
description: Remove the structural "slop" signals that make LinkedIn writing read as AI-generated, primarily for posts. Use this skill whenever the user is writing or editing a LinkedIn post, wants copy to sound like a person, or asks to "remove the slop", "de-slop", "make this not sound like ChatGPT wrote it", "anti-slop", "sound human", or wants a post checked for the patterns readers now associate with AI. Those patterns are repeated sentence openings, contrast framing, colon titles, buzzwords, and vague claims. This skill explains each pattern, gives a targeted prompt for each one, and ends with a master prompt to append as the very last instruction on any writing request. Also trigger when the user wants to figure out why a piece of writing feels AI-generated even though it has no emojis or em dashes.
---

# LinkedIn Anti-Slop

Your reputation on LinkedIn is tied to what you publish, and readers often decide how credible a post feels within the first couple of sentences. Part of that judgment is unconscious now. People can tell when writing came from AI, and they form the opinion fast, usually before they finish the second line.

In the early days you could spot AI writing by the emojis, the em dashes, and the overly polished enthusiasm. People stopped doing those things, so the tells moved. The new slop signals live in the structure of the sentences. Readers sense them quickly even when they cannot name them. This skill names them and gives you prompts to remove them. If you only want the fix, skip to the master prompt at the bottom.

## Ramble first, then tighten, then run the prompt

The workflow for a post looks like this. Talk your raw idea out to the AI in your own words, unpolished, and put the most interesting or contrarian thing first. Use the model to find what is actually worth saying, then tighten the wording yourself so it sounds like you. Before you lock the final draft, paste the master prompt as the last thing you send. After that, read the draft once against the five patterns below and cut anything that trips them.

## You can teach AI to name its own patterns

Here is how I keep finding new slop patterns as they appear. Whenever something on LinkedIn gives me the gut reaction of slop, I copy a few examples and paste them into ChatGPT, or whatever model you use. Then I ask two questions in order.

First: "What grammatical structure is happening here?" The model usually points to a specific rhetorical pattern or sentence structure that shows up often in persuasive writing. Second: "Write a prompt that prevents this structure from appearing." In a strange way, the model teaches me grammar so that I can stop writing like the model. You can run this same loop yourself, because slop keeps changing and the tells from six months ago are the ones everyone can spot today.

## Five structural patterns that read as slop today

### Repeated sentence openings quickly feel mechanical

AI often repeats the same opening word or phrase across several sentences because the rhythm sounds persuasive. Writers call this anaphora. It shows up like this:

> "We tested the system. We deployed the system. We expanded the system."

The repetition creates rhythm, but once readers see the pattern across hundreds of posts it starts to feel staged.

```
Avoid anaphora and repeated opening phrases. Do not repeat the same beginning across multiple sentences. Write sentences with varied structure and natural flow.
```

### Contrast framing has become a LinkedIn habit

Another common structure defines an idea by comparison. The sentence sets up one concept and dismisses another in the same line. Persuasive writing leans on this because it creates a feeling of clarity. The move looks like this:

> "Great operators build systems, not workflows."
>
> "This is a leadership decision, not a technical one."

When many posts use the same construction, the writing starts to sound scripted.

```
Avoid contrast based sentence structures and rhetorical opposition. Explain ideas directly without defining them through comparison with another concept.
```

### Colon titles often simulate depth

AI frequently writes titles that use a colon to split the line into two parts:

> "The Future Of Marketing: Why Systems Win"
>
> "From Data To Strategy: A New Perspective"

The first half tries to create intrigue and the second half tries to sound analytical. When readers see the structure over and over, the framing feels artificial, which reads as slop.

```
Avoid colon based dual clause titles. Write straightforward titles that describe the idea directly without rhetorical framing.
```

### Buzzwords replace meaning faster than people realize

Many AI sentences rely on hype language. The wording sounds impressive while the sentence carries very little information. You will see lines that promise "improved decision making", "better visibility", "cutting edge solutions", "actionable insights", or "unlocking the power of". A quick test: if you delete the adjectives and the meaning stays the same, the sentence was mostly filler.

```
No emojis. Avoid using em dashes; use commas or periods instead Do not use any of the following words or any derivatives of the following words: Unlock, leverage, harness, insights, democratize, explore, discover, dive in, elevate, enhance, witness, revolutionize, transform, embrace, unleash, dive, indulge, actionable, reveal, unmatched, delve, era, collaboration, insights, cutting-edge, matters, already, impact, fusion, advancing, navigate, drive, problem, solver, changemaker, game changer, ensure, transformational, powerful, derailed, delighted, delve, cheat code.
```

### Vague claims quietly erode credibility

This one appears in human and AI writing. The sentence makes a claim with no concrete detail behind it. For example:

> "A tool helps teams move with clarity because it helps industries get answers faster."
>
> "A solution that helps companies make better decisions."

Readers lose trust when the writing stays abstract for too long.

```
Avoid vague claims without specifics. Include numbers, concrete examples, named tools, or measurable outcomes when possible.
```

## These patterns come from how the models were trained

Language models learn from huge collections of persuasive writing, so they reproduce the structures that appear most often in that writing. When millions of people use the same tool, those structures become visible at scale. Readers start to recognize the rhythm of the sentences and the shape of the arguments, and once someone notices the pattern they cannot stop seeing it.

## Paste this master prompt last, never first

Here is the full prompt that removes every pattern above at once. One rule about how to use it. It has to be the last thing you give the model, placed after all of your other instructions and context. Do not use it as the first prompt and do not use it as system instructions. I do not fully know why, but it works far better as the final message. Give the model your topic, your rambled ideas, and your direction first, then paste this at the very end.

```
No emojis. Avoid using em dashes; use commas or periods instead. Do not use any of the following words or any derivatives of the following words: Unlock, leverage, harness, insights, democratize, explore, discover, dive in, elevate, enhance, witness, revolutionize, transform, embrace, unleash, dive, indulge, actionable, reveal, unmatched, delve, era, collaboration, insights, cutting-edge, matters, already, impact, fusion, advancing, navigate, drive, problem, solver, changemaker, game changer, ensure, transformational, powerful, derailed, delighted, delve, cheat code. If there are titles (including headers), All titles should be based on insights not titles. Write them like one-liners with no more than 10 words. Titles can be informal but they need to be insightful first. If there are not titles, do not add them. Avoid contrastive negation, antithesis, and rhetorical contrast. No “X, not Y” constructions. Write in a natural, conversational tone. Avoid sentence fragments, anaphora, and asyndeton. Do not use short standalone phrases like “Not theory.” or stacked clauses without conjunctions. Write in complete, naturally flowing sentences. Avoid repeated sentence openings across multiple sentences and vary sentence structure so the same word or phrase does not begin consecutive sentences. Do not structure paragraphs around rhythmic rhetorical patterns that sound like speeches or persuasion frameworks and prioritize clarity over dramatic phrasing. Avoid colon based dual clause titles or headings that try to simulate depth and write titles that describe the idea directly instead of splitting a concept into two rhetorical halves. Remove buzzwords, hype language, and filler adjectives and replace vague marketing style phrasing with clear descriptions of what actually happens. Avoid vague claims and include concrete examples, numbers, tools, constraints, or specific situations whenever possible so the writing contains real information. Prefer straightforward explanation over rhetorical emphasis and write sentences that sound like a thoughtful person explaining an idea instead of a motivational post or keynote speech. When editing text, simplify sentences that sound formulaic or generic and replace abstract language with precise wording that reflects a real observation or experience.
```

## Notes

- Use the five targeted prompts when you want to fix one specific habit in a draft. Use the master prompt when you want the full pass on a finished draft.
- The master prompt goes last every time. Its placement changes the result more than its wording does.
- The prompt is strict on purpose. If a banned word is genuinely the clearest option for a sentence, keep it and move on, because a readable sentence beats a rule.
- Run the two-question method (name the structure, then prompt against it) whenever you notice a new pattern spreading. The list of tells will keep growing.
- This skill pairs with the posting guidance in the repo README, which covers why the first two sentences carry the whole post.
