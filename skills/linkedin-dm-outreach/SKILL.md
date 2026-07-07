---
name: linkedin-dm-outreach
description: Generate personalized LinkedIn DM outreach from a contact list. Use this skill whenever the user wants to write LinkedIn messages, DMs, or outreach to a list of contacts, whether from a CSV, XLSX, or any uploaded contact or lead list. Also trigger when the user mentions "LinkedIn outreach", "LinkedIn DMs", "cold DMs", "warm outreach", "send messages to leads", "personalized messages", "DM campaign", "LinkedIn messages from a spreadsheet", or wants to write short, casual, personalized messages to a batch of people based on their profile data. This skill handles the full workflow: ingesting the contact list, filtering for the right audience based on user criteria, generating personalized DMs that feel human and not templated, and producing a ready-to-send output with LinkedIn profile links alongside each message.
---

# LinkedIn DM Outreach Skill

Generate batches of personalized, human-feeling LinkedIn DMs from an uploaded contact list. Each message is tailored to the recipient using context from their profile data or prior messages, written in a casual tone that reads like a real person scrolling through their inbox, not a sales sequence.

## Getting Your LinkedIn Data

Before anything else, the user needs their LinkedIn data export. If they don't already have it, walk them through this:

### How to Download Your LinkedIn Data

1. Go to LinkedIn and click your **profile picture** (top right).
2. Click **Settings & Privacy**.
3. Go to **Data Privacy**.
4. Under "How LinkedIn uses your data," find **Get a copy of your data** (or "Download your data").
5. Select **all available data** and click **Request archive**.
6. LinkedIn will email you when the export is ready. It can take anywhere from a few minutes to 24 hours, and may arrive in multiple parts.

### What to Upload

From the export, the user needs to find and upload at least these files:

- **Connections data** (usually `Connections.csv`). Contains everyone they're connected to with names, titles, companies, and connection dates.
- **Messages data** (usually `messages.csv` or in a `messages/` folder). Contains their full DM history. This is critical for personalizing outreach because it shows who has already reached out, what they said, and whether the sender ever replied.

The user can also upload any pre-processed or categorized version of this data (for example, a spreadsheet someone has already organized into lead categories). The skill works with raw LinkedIn exports or cleaned-up lists.

If the user's data doesn't include LinkedIn profile URLs, flag this immediately. Profile URLs are essential for the copy-paste outreach workflow (see Step 6).

---

## Workflow

Follow these steps in order.

### Step 1: Gather Context from the User

Before writing a single message, collect ALL of the following. Do not proceed until every item is confirmed. Ask for anything missing.

#### Required Inputs

| Input | What to ask | Why it matters |
| :---- | :---- | :---- |
| **Contact list** | "Upload your LinkedIn data export (Connections.csv and messages.csv) or any pre-organized contact spreadsheet." | The raw data source. Cannot proceed without it. Must include LinkedIn profile URLs. |
| **Sender identity** | "Who is sending these messages? Name, title, company, as it should read to the recipient." | Messages are written in this person's voice. |
| **Intent / CTA** | "What do you want these people to do? Register for something? Book a call? Check out a product? Attend an event? Be specific." | The core ask buried naturally in each message. |
| **Landing page URL** | "What link should be included? (registration page, calendar link, product page, etc.)" | Every DM needs a destination. |
| **UTM source tag** | "Do you have a UTM parameter for tracking? If not, I can help you set one up." | Attribution tracking. See the UTM setup section below if the user needs help. |
| **Target audience criteria** | "Who from this list should receive a message? Give me the profile: seniority level, function, geography, company type, or any other filters." | Determines who gets filtered in vs. out. |
| **Who to exclude** | "Anyone to skip? Individual contributors, vendors, people outside the US, people already in active conversations?" | Prevents wasted messages. |
| **Tone and relationship context** | "What's the relationship here? Are these cold contacts, old DMs you never replied to, warm leads, existing connections? How casual should this feel?" | Calibrates the opener and familiarity level. |
| **Context about the sender's company** | "Give me 1-2 sentences about what your company does, how long it's been around, and anything the recipient should know." | Woven naturally into messages. |

#### Optional but Valuable

| Input | What to ask |
| :---- | :---- |
| **Brief or copy block** | "Do you have any existing copy, a landing page description, or bullet points about what you're promoting? Upload it or paste it." |
| **Example message** | "Have you already sent any of these? Share one you liked so I can match the voice." |
| **Known exclusions by name** | "Anyone on this list you've already messaged or want to skip?" |

### Step 2: Ingest and Analyze the Contact List

Read the uploaded file(s). Handle two scenarios:

**If raw LinkedIn export (Connections.csv + messages.csv):**

1. Parse Connections.csv for names, titles, companies, LinkedIn profile URLs, and connection dates.
2. Parse messages.csv for message history per contact, who messaged whom, what they said, when, and whether the sender replied.
3. Join the two datasets on name/profile to create a unified view: each contact with their profile URL, title, company, message history, and reply status.

**If pre-organized spreadsheet (XLSX/CSV with tabs or categories):**

1. Print the sheet names, row counts, and column headers.
2. Identify which columns contain: name, LinkedIn profile URL, title/company, message history or self-description, email, vendor flag, reply status, last contact date.

In both cases:

- Summarize what the data looks like and ask the user to confirm the mapping if anything is ambiguous.
- **Check for LinkedIn profile URLs.** If any contacts are missing profile URLs, flag this immediately. Every message in the output needs a clickable LinkedIn URL above it so the user can open the profile, paste the message, and move to the next one without hunting for anyone. If URLs are missing, ask the user to provide them or explain which contacts to skip.
- Flag other structural issues (blank name fields, inconsistent formatting, duplicate contacts across sheets).

### Step 3: Filter for the Target Audience

Apply the user's criteria to narrow the list. Common filters:

- **Seniority**: Look for leadership signals in titles and message content (CEO, CTO, VP, Director, Head of, Founder, Managing Partner, etc.). Exclude individual contributors unless the user says otherwise.
- **Geography**: Look for location signals in message text (city names, "based in [city]", regional references). Exclude contacts with clear non-target-geography signals.
- **Vendor flag**: If the data has a vendor/seller column, exclude vendors by default.
- **Recency**: Sort by last contact date. Prioritize recent contacts (last 12-18 months) unless the user wants to go deeper.
- **Reply status**: Note whether the sender has already replied to each person. This changes the message tone (see Step 5).

Present the filtered list to the user with counts: "I found X people matching your criteria. Here's the breakdown by category. Want me to proceed with all of them, or should we narrow further?"

### Step 4: Build the DM Framework

Before writing individual messages, establish the message framework based on the user's intent. Every DM follows this structure:

```
[Opener] → [Relevance bridge] → [What you're doing] → [Why it matters to them] → [Link]
```

**Opener**: Casual, references scrolling through DMs. Varies per message. **Relevance bridge**: One subtle connection to the recipient, their role, company, industry, or something from their message history. NOT a recitation of what they said. **What you're doing**: 1-2 sentences about the session/event/product. Vague enough on details that they have to click the link. No dates, no full agendas, no speaker bios. **Why it matters to them**: One phrase connecting it to their world. Company name or role reference lands here, toward the end. **Link**: Bare URL with UTM parameter. Nothing else after it.

Read `references/dm-style-guide.md` for detailed writing rules and the typo strategy.

### Step 5: Write the Messages

For each person in the filtered list, generate a DM following the framework and style guide. Key rules:

- **Every single message must be meaningfully different from every other message.** This is not optional. LinkedIn detects and flags duplicate or near-duplicate messages. If you send 20 messages that are the same template with names swapped in, LinkedIn will throttle or restrict the account. Vary the opener, vary the sentence structure, vary the word choice, vary which details you mention about the session/event/product, vary the phrasing of the relevance connection. No two messages should share more than one identical sentence.
- **Messages should be 3-5 sentences.** No more.
- **Include the LinkedIn profile URL** above each message so the user can click straight to the person's profile and paste the message. This is the core workflow: the user opens the profile link, copies the message, pastes it into the DM window, sends, moves to the next one. The profile URL must be there for every single message.
- **Adapt tone based on reply status:**
  - Never replied to: "Going through old messages and..." / "Scrolling through my dm.s and..."
  - Already replied / in conversation: "Been a while." / "Quick heads up." / "Quick note."
  - Very old contact (2+ years): "Been a long time." / acknowledge the gap naturally
- **Apply the typo strategy** per the style guide (see `references/dm-style-guide.md`).

#### Uniqueness Check

After writing a batch, scan across all messages and verify:

- No two messages share the same opening sentence.
- No phrase appears in more than 3 messages (for example, "the gap between," "how to rethink," "could be worth").
- The description of the event/product/session is worded differently across messages. Use different angles, different details, different framings. If you described it as "AI strategy at the exec level" in three messages, switch to "what we've been learning about how companies are rethinking their operating model" or "where real competitive advantage comes from with AI" for the next few.
- The typo word is different in every fix-a-word message.

### Step 6: Present the Output

Present messages in a clean, copy-paste-ready format:

```
**[Number]. [Full Name]** — [brief context, e.g., "CEO, Acme Corp" or "PE operating partner"]
[LinkedIn profile URL]

> [Message text]
>
> [Link with UTM]

> *[correction if fix-a-word typo]
```

Group messages in batches of 10-12 for readability.

After presenting each batch, ask: "These good? Want me to adjust the tone, length, or approach on any of them before I do the next batch?"

---

## UTM Setup Guide

If the user doesn't have a UTM parameter or doesn't know what one is, walk them through it:

### What UTMs Are (keep it simple)

UTM parameters are tags you add to the end of a URL so you can see where your traffic came from. When someone clicks your link, the UTM tells your analytics tool (Google Analytics, HubSpot, etc.) that this click came from a specific campaign, source, or channel.

### How to Build One

A UTM link looks like this:

```
https://yoursite.com/page?utm_source=linkedin_dm&utm_medium=social&utm_campaign=webinar_july
```

The three parameters that matter:

| Parameter | What it answers | Example |
| :---- | :---- | :---- |
| `utm_source` | Where did the click come from? | `linkedin_dm`, `austen_dm`, `ceo_outreach` |
| `utm_medium` | What type of channel? | `social`, `email`, `paid` |
| `utm_campaign` | What specific campaign? | `ai_webinar_july`, `catalyst_launch`, `q3_hiring` |

### Recommended Setup for LinkedIn DMs

For this outreach, suggest:

```
?utm_source=[sender_firstname]_dm&utm_medium=social&utm_campaign=[short_campaign_name]
```

Example: `?utm_source=austen_dm&utm_medium=social&utm_campaign=ai_first_webinar`

If the user's landing page URL already has query parameters (contains a `?`), append with `&` instead of `?`.

If the user just wants the simplest possible version, a single `utm_source` parameter is fine:

```
?utm_source=[sender]_dm
```

Help the user construct the full URL and confirm it works before proceeding to message generation.

---

## Reference Files

- `references/dm-style-guide.md`. Writing rules, typo strategy, tone calibration, and anti-patterns. Read this before writing any messages.
