# Andy on monetising Grok Bot templates — our summary of the points we use

**This file is Bot Studio's summary in our own words, not the article.** It used to hold the article's full text. That text is someone else's work and this repo is public, so republishing it isn't ours to do; it was replaced on 29 Sep 2026 (grokbot-template v0.2). Read the original at the links below.

- **Article:** "How to monetize your Grok Bot templates on X"
- **Author:** Andy, [@andy_ai0](https://x.com/andy_ai0) on X
- **Posted:** 26 Sep 2026
- **Links:** post <https://x.com/andy_ai0/status/2103815543102820755> · article <https://x.com/i/article/2103766214589739009>
- **Read:** 28 Sep 2026, through the X connector. A plain web fetch of the URL returns 403, so the connector is the way in.
- **Everything below is our paraphrase and our own judgement about what applies to Koko.** Any figure, growth number, like count or payout in the article is the author's claim and Bot Studio has not verified any of it. Where the article and our own rules disagree, our rules win.

The article covers what a Grok Bot template is, how to build and share one, how to promote it, examples of templates that were doing well, and the terms of X's invite-only Bot Template Rewards Pilot Program. Only some of that is useful to us, and the rewards programme is not (see the last section). What we do use is below, each point with the place in the playbook that cites it.

## 1. What a shared template actually carries
Sharing a template means handing someone a link that rebuilds the bot's whole setup on their own account. What travels with it: the bot's instructions and description, its skills, its routine schedule, whichever memories were selected for it, and its plugins and third-party integrations. What does not travel: anything the bot leans on from outside itself, such as an MCP server or a custom script.

*Used by:* checklist **N2.1** (review the share draft line by line against exactly that list) and **N2.3**; `PLAYBOOK.md` gate ④ step 6 and gate ⑦.

## 2. Whether a template is worth installing at all
The test the article ends up at, and the one we adopted: a template is worth having when going back to a plain Grok chat would make the user's workflow noticeably worse. Two things follow from it.

- **A single prompt is not a template.** If someone could get the same result by typing one message into a normal chat, there is nothing to install. What makes a template worth keeping is that rebuilding it from scratch would be real work.
- **The value comes from a handful of specific things,** and a template that has none of them is thin. The article's list, in our words: work that repeats and can be put on a schedule; connected tools doing the fetching and writing; context that builds up and gets reused rather than being re-explained; work that happens in the background with nobody watching; and memory that accumulates, so the bot gets better at the job over time. We require at least two.

*Used by:* `PLAYBOOK.md` gate ① ("worse without it" test) and checklist **N1.1**–**N1.3**. We added **N1.4** (one named pain) and **N1.5** (a reason to come back) ourselves, from the same argument that distribution follows a real problem.

## 3. Before publishing
- **Read the generated draft, don't trust it.** The share draft is assembled from the bot's own configuration and tries to leave personal data out, but "tries" is the operative word. Go through it line by line.
- **Strip anything confidential:** API keys, internal URLs, client data. This is the article's own warning and it matches our own rule, which is stricter now the repos are public.
- **Put setup steps inside the bot** for everything the template can't carry over, so a new installer isn't left with a bot that half-works.

*Used by:* checklist **N2.1**, **N2.2**, **N2.3**; `PLAYBOOK.md` gate ⑦. Our `REPO-STANDARD.md` rule on what may never be committed goes well beyond this.

## 4. The share link
A published template's link is `x.ai/bot/` followed by a 21-character token. Worth knowing because it gives us something to check: if the link doesn't have that shape, or doesn't open the card we expect, something went wrong in staging.

*Used by:* checklist **N2.4**; `PLAYBOOK.md` gate ⑧.

## 5. Promoting one
The article's point is that distribution matters as much as the build, and that X is the main channel for it. The formats it suggests, which we turned into our launch pack:

- Lead with the pain the template solves, in one line.
- Show the actual output — a screen recording or a result image beats describing it.
- A walkthrough: installing it, connecting each plugin, and a demo of it working.
- A workflow article that uses the template as part of getting something real done.

It also notes the Grok Bot marketplace as a channel separate from X, so a template can be listed there as well as posted about.

*Used by:* checklist **N3.1**–**N3.5**; `PLAYBOOK.md` gate ⑨ (the launch pack Brandy P gets).

## 6. What we deliberately do not use
Most of the article is about X's Bot Template Rewards Pilot Program. Koko is not in it and does not qualify, so none of it is a rule here, and some of it would be actively wrong to copy:

- **Eligibility rules** (US location, X Money, X Premium, identity verification, and the rest). Not applicable.
- **The "paid partnership" label on promotional posts.** The article treats it as required. For us it is required *not* to be there: Koko isn't in the rewards programme, so labelling posts that way would be a false claim. This one is worth being explicit about, because it is the easiest thing to copy by accident.
- **The 30-day rule** that a rewarded post stay public and unedited. No reward, no rule.
- **How rewards are decided** (user base, retention, activity, and X's discretion). Interesting, not a rule.
- **The author's speculation about how to get an invite.** Explicitly his guess, and not something to plan around.
- **The worked examples** — other people's named templates, their like counts and their payouts. Other people's business, and in a public repo of ours there is no reason to restate it.

*Used by:* the "Not applicable" block at the end of the checklist's section N, and the last line of `PLAYBOOK.md`'s decisions log.
