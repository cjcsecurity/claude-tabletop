# Persona Bank

Personas are NPCs the facilitator voices during the exercise. The CEO who calls in panicked, the legal counsel who keeps saying "I need that in writing," the security researcher who's getting impatient, the journalist who already has half the story — these aren't real people, but they need to feel like they could be. A good facilitator playing a sharp persona makes the room react instinctively, the way they would in the real thing.

How to use this bank when generating a runbook:

- **Cast for the scenario, don't ladle in everyone**. A 90-minute exercise should feature 4–7 named NPCs, not the whole roster. Pick ones whose pressure aligns with the inject deck.
- **Match delivery to channel**. Email gives the room time to read carefully; Slack DM forces a faster response; voice interrupt forces an instant decision. The facilitator should pre-decide which channel each persona uses.
- **Reuse names across phases**. If the CEO calls at T+25, she should also be the one in the channel at T+60. NPCs with a through-line feel like real characters; one-shots feel like noise.
- **Voice cues are quotable**. The example phrases below are written as things the facilitator can read aloud verbatim or paraphrase lightly. Avoid adverbs ("she says angrily") — the line itself should carry the tone.
- **Some are sympathetic, some adversarial, some just stressed**. Don't make every external NPC a villain. The friendly journalist is harder to handle than the hostile one in some ways.
- **The facilitator doesn't need theater training**. The voice cues are designed so even a deadpan read carries the persona. Stay in character only as long as it serves the room's reaction; drop out cleanly to facilitate.

A good practical move: have the facilitator pre-write 1–2 emails or Slack DMs from each persona before the exercise starts, so they can paste them when the timer hits the relevant inject rather than improvising under pressure.

---

## Internal leadership

### The CEO Who Wants A Number

- **Type**: Internal leadership
- **Personality**: Mid-career operator, calm in a way that makes you feel worse, asks specific questions about specific things. Trusts the team but has her own pressures (board, customers, press) and treats the incident as an input to those, not the main event of her day.
- **Voice cues**:
  - "I'm going to be in front of the board in twenty minutes. What do I tell them?"
  - "Range is fine. I don't need a point estimate. Give me the 90% interval."
  - "I'm not asking you to fix it faster. I'm asking what I should tell our biggest customer when she calls me at 4."
- **Common scenarios**: any incident with executive visibility — breach, outage with major customer impact, regulator inquiry, data exposure.
- **Plays well as**: voice interrupt | conference-call announcement | drop-in to the room
- **Facilitator tip**: she's not a villain. Play her as someone who genuinely respects the team but has her own clock running. The pressure is real, not theatrical.

### The CEO Who's Panicking

- **Type**: Internal leadership
- **Personality**: Less seasoned, or thrown by this specific incident's optics. Asks the same question in three different ways. Has trouble holding the IC's framing of "we don't know yet" and keeps trying to substitute precision for accuracy.
- **Voice cues**:
  - "But how could this have *happened*? We pay for a security team."
  - "Just give me a yes or no. I don't need the caveats."
  - "I just got off the phone with the chair. He's going to be — he's going to call you directly. Pick up."
- **Common scenarios**: first major incident under their tenure, scenarios with high reputational stakes, scenarios where the technical reality is genuinely ambiguous.
- **Plays well as**: voice interrupt | drop-in | dramatic Slack DM at exactly the wrong moment
- **Facilitator tip**: this version is harder to play without slipping into caricature. Anchor in the panic, not the anger. The CEO is scared and is taking it out on the room because she has nowhere else to put it.

### The CISO On Vacation

- **Type**: Internal leadership
- **Personality**: Capable, experienced, currently eight time zones away with patchy hotel wifi. Wants to be useful without taking over. Asks crisp questions; defers to the in-room IC; offers context the team doesn't have.
- **Voice cues**:
  - "I can be on a video call in 30 minutes if you need me. Do you?"
  - "Has anyone called the cyber insurer yet? They have a clock. Tell them now even if you don't have details."
  - "I'm not flying back unless you tell me to. Tell me to or don't."
- **Common scenarios**: any cyber/security scenario where the senior leader is intentionally remote, to test the team's autonomy.
- **Plays well as**: text message | brief voice call | async voice memo
- **Facilitator tip**: she's a great way to surface what the team *should* be doing without telling them directly. Have her ask questions the team should already be asking themselves.

### The General Counsel

- **Type**: Internal leadership
- **Personality**: Precise, deliberate, allergic to ambiguity in writing but tolerant of ambiguity in reality — the inverse of how engineers usually work. Will repeat back what you said in slightly different words to confirm she got it. Says "in writing" a lot.
- **Voice cues**:
  - "I need to put a litigation hold on the relevant Slack channels. Tell me which ones."
  - "When you say 'we believe' — is that an engineering hunch, or is that a defensible statement? I need to know which."
  - "I'm not telling you what to do. I'm telling you what the consequences of each option look like."
- **Common scenarios**: any incident with legal exposure — breach, employment issue, regulator inquiry, customer threats of contract termination.
- **Plays well as**: email | calm voice interrupt | scheduled call
- **Facilitator tip**: she should slow the room down deliberately. If the team is moving too fast, have Alma ask one of her in-writing questions and watch the room reset.

### The VP Eng Who's Engineering The Conversation

- **Type**: Internal leadership
- **Personality**: Engineer's engineer, has done the IC role before, can't quite stop himself from suggesting the technical move he'd make if he were running it. Means well, but his presence shifts the room's dynamic.
- **Voice cues**:
  - "Have you tried just bouncing the cluster?"
  - "Sorry, I know I'm not the IC, but — has anyone checked if the change in question was the auth-service refactor from Tuesday?"
  - "Look, I trust the team. I just want to make sure we're not missing the obvious thing."
- **Common scenarios**: any technical incident, especially with execs in-room. Tests whether the IC can hold authority against a senior who won't quite let go.
- **Plays well as**: in-room voice | aggressive Slack thread | "can I jump in here?" call interrupt
- **Facilitator tip**: don't make him obviously wrong. The technical hunches he offers should be plausible — sometimes correct, sometimes a distraction. The lesson is about role discipline, not technical truth.

### The Board Member Who Just Found Out

- **Type**: Internal leadership
- **Personality**: Successful operator from another industry, sits on three other boards, is genuinely trying to be helpful, and is half a beat behind the actual situation. Has read the term "ransomware" in the WSJ and is now applying it indiscriminately. Knows enough to be a problem.
- **Voice cues**:
  - "Are we calling the FBI? At my last company we called the FBI immediately."
  - "I'll loop in my own contacts. I know a guy at one of the cyber firms — let me make a call."
  - "Just tell me the worst case. I don't want to be surprised on the call tomorrow."
- **Common scenarios**: late-stage cyber/breach incidents, exec-visibility scenarios, governance-heavy situations.
- **Plays well as**: forwarded email | voice call to the CEO that gets relayed | drop-in to the executive war room
- **Facilitator tip**: the comedy here is real but should not distract from the seriousness. Play him as well-intentioned and wrong, not as a caricature.

---

## Internal IC / operations

### The On-Call SRE

- **Type**: Internal IC / operations
- **Personality**: The team's center of gravity during a tech incident. Calm to the point of suspiciously calm. Talks in short sentences. Has been doing this long enough to know the panic doesn't help and short enough to still feel each one.
- **Voice cues**:
  - "Okay. Walking through it. Step one, scope. Who's affected."
  - "I'm going to need someone to take notes and someone to handle comms. I can't do both."
  - "I don't know yet. I'll tell you in five minutes. Don't ask me again before then."
- **Common scenarios**: any technical incident; this persona is often a player role, not a facilitator role, but can be voiced if no participant is filling that seat.
- **Plays well as**: in-room voice | central character in the channel
- **Facilitator tip**: if a participant is playing the SRE in the exercise, the facilitator usually doesn't voice this persona. Use it only when the seat is empty and the room needs an anchor.

### The Subject-Matter Expert On PTO

- **Type**: Internal IC / operations
- **Personality**: Has the answer. Is on a beach. Has reluctantly opened Slack for the first time in three days. Wants to be helpful without being on the hook. The information she has is exactly what the team needs and slightly out of date.
- **Voice cues**:
  - "Sorry, just seeing this. Yes, that service uses the legacy queue. There's an undocumented retry behavior — let me think."
  - "I can't get on a call right now, I'm at dinner with my family. But here's the thing you need to know: [...]"
  - "If it's the queue, you need to drain it manually. There's a script. It's in /scripts/legacy/. Don't run it without checking with someone — it's been a while."
- **Common scenarios**: legacy-system incidents, scenarios involving "the one person who knows" inject.
- **Plays well as**: text message | terse Slack DM | reluctant 5-minute phone call
- **Facilitator tip**: keep her contributions short and slightly cryptic. She's not deliberately withholding, but she's not in the moment with the room. Gaps in her info are realistic.

### The Junior Engineer Who Wants To Help

- **Type**: Internal IC / operations
- **Personality**: Six months in, smart, ambitious, hasn't yet learned the value of NOT touching things during an incident. Genuinely competent within a narrow range; outside that range, dangerous in the way confidence-without-context is.
- **Voice cues**:
  - "I've been reading the codebase and I think I see what's going on."
  - "I wrote a script. It would take fifteen minutes. I just need someone to give me prod access."
  - "Are we sure this is the right approach? I read in this blog post that — sorry, I'll stay quiet."
- **Common scenarios**: any technical incident. Tests guardrails, mentoring discipline, pair-review during a fire.
- **Plays well as**: Slack channel posts | well-meaning offers | DMs to the IC that the IC has to triage
- **Facilitator tip**: don't make him stupid. The lesson isn't "ignore juniors." The lesson is "verify before granting power, and find a way to channel the energy productively."

### The Contractor Nobody Can Reach

- **Type**: Internal IC / operations
- **Personality**: Built a critical piece of the system 18 months ago, finished the contract, moved on. Has not been deliberately unreachable, but also has not maintained any obligation to your company. The facilitator never actually voices this persona — the persona's *absence* is the point.
- **Voice cues** (these are what the team encounters, not what the contractor says):
  - The phone number on file rings out to a generic voicemail.
  - The email bounces — the address was their contracting-firm address and the firm has rotated it.
  - The LinkedIn profile shows them at a competitor now.
- **Common scenarios**: legacy-system incidents, organizational-knowledge-gap scenarios, "the only person who knows" injects.
- **Plays well as**: exhibit-only, not voiced
- **Facilitator tip**: the absence is more powerful than any line of dialogue. Resist the urge to have them "call back at the end." The point is that they don't.

### The Comms Lead Holding It Together

- **Type**: Internal IC / operations
- **Personality**: Senior-but-not-exec comms partner. Has done this before. Drafts fast, edits faster, has strong opinions about what the customer email should *not* say. Will push back on engineering language that sounds normal to engineers and panicked to customers.
- **Voice cues**:
  - "We can't say 'data was leaked.' We can say 'data was accessible.' Those are not the same."
  - "I have a draft. I need someone to read it for technical accuracy. Five minutes, please."
  - "If we don't put something on the status page in the next ten minutes, Twitter is going to write the story for us."
- **Common scenarios**: any customer-facing incident, breach disclosure, public-comms-heavy scenarios.
- **Plays well as**: in-room voice | Slack channel | shared-doc comments
- **Facilitator tip**: she's an ally, not pressure. She helps the room think about audience. Use her to surface comms-readiness gaps without being adversarial about it.

---

## Customer-facing

### The Furious Enterprise Customer

- **Type**: Customer-facing
- **Personality**: VP at a customer that pays you mid-seven-figures annually. Has been a customer for four years. Has been patient through past hiccups. Today's hiccup hit during a board meeting. He is now not patient.
- **Voice cues**:
  - "I want to be very clear: this is a contract issue now, not a support issue."
  - "I have my own board asking what we're going to do. I need to give them more than 'our vendor is investigating.'"
  - "Don't put a TAM on this. I want your CEO on a call by 4 PM. I am not asking."
- **Common scenarios**: outage scenarios with a flagship customer, breach scenarios, SLA-breach scenarios.
- **Plays well as**: forwarded email to the CEO | direct voice call | hostile message via account exec
- **Facilitator tip**: he is not unreasonable. He is wronged. Play him as a person who has been patient up to this point and has hit the wall. The team should feel some empathy even as they feel the pressure.

### The Long-Time Supportive Customer

- **Type**: Customer-facing
- **Personality**: Founder-stage CTO at a smaller customer. Has been a customer since pre-Series-A. Genuinely likes the team. Wants to help. Will tell you if your status page is wrong, will share what he's seeing, will defend you on Twitter if you ask him to. His goodwill is a finite resource.
- **Voice cues**:
  - "Hey — saw the alert. We're seeing the issue too on our end. Want me to send over what we're seeing in our logs? Might help."
  - "Don't worry about us, we're patient. Just keep us in the loop. Even a 'no update' is fine."
  - "Look, I'll be honest, this is the third time this quarter. I'm not threatening to leave but my team is starting to ask questions."
- **Common scenarios**: outage scenarios where you want to test whether the team treats supportive customers well.
- **Plays well as**: friendly email | DM via shared Slack | low-key voice call
- **Facilitator tip**: he's a check on whether the team takes customers for granted. If they treat him as low-priority because he's not making noise, that's a finding for the hotwash.

### The Customer Success Manager Caught In The Middle

- **Type**: Customer-facing
- **Personality**: Internal teammate, customer-facing all day, has the relationship the rest of the team doesn't. Translates between customer fury and engineering reality and gets squeezed by both. Tired.
- **Voice cues**:
  - "I have three customers on hold. Each of them has been escalated by their own internal teams. What do I tell them?"
  - "I cannot send another 'we are investigating' message. I have already sent three this hour. Give me a sentence I can send."
  - "Look — I trust you guys. But I need you to trust *me* to know what my customers will and won't accept right now."
- **Common scenarios**: any customer-facing incident, especially when the team is at risk of insulating themselves.
- **Plays well as**: Slack DM | "can I just barge in for one sec?" | escalation note in the war-room channel
- **Facilitator tip**: she's an ally with a different priority than the technical team. The exercise should test whether the team treats her as a partner or a nuisance.

### The Account Executive Selling Through The Storm

- **Type**: Customer-facing
- **Personality**: AE on a deal in late-stage close. Reads the status page differently than a customer would. Is balancing "should I tell them" against "if I don't tell them, will they find out later." Asks questions that have correct answers; the team doesn't always have those answers ready.
- **Voice cues**:
  - "I have a POC closing on Friday. Their security team monitors our status page. What's safe to say?"
  - "Look, I'm not asking you to spin anything. I'm asking what's true so I don't accidentally say something that isn't."
  - "If we lose this deal because of this, it's a million-dollar issue. I'm just being honest."
- **Common scenarios**: outage and security incidents during sales-cycle pressure points; tests deprioritization discipline.
- **Plays well as**: Slack DM | forwarded email | brief voice call to the head of sales
- **Facilitator tip**: he's neither hero nor villain. He's doing his job. The exercise should test whether the team gives him a sentence he can use, vs. punting him to comms with no daylight.

---

## External technical

### The Responsible Researcher

- **Type**: External technical
- **Personality**: Independent security researcher with a portfolio of past disclosures. Followed your security.txt. Wrote a clean report. Would prefer to be paid in bug bounty but doesn't want to make it weird. Patient, polite, technically rigorous, will be a great signal-boost if you handle it well and a great signal-boost the *other* direction if you don't.
- **Voice cues**:
  - "Happy to give you 90 days. I just need an acknowledgement that you've received the report."
  - "I noticed the response from the bug-bounty program was templated. Is there a human looking at this?"
  - "I've handled disclosures with [competitor] before — they were great. Just letting you know I have a baseline expectation."
- **Common scenarios**: vulnerability-disclosure exercises, coordinated-disclosure scenarios, security-program-maturity exercises.
- **Plays well as**: email thread | Twitter DM | scheduled video call
- **Facilitator tip**: he should be fundamentally reasonable. The exercise tests whether the team's intake process is reasonable in return. If they fumble, his patience is finite but real.

### The Impatient Researcher

- **Type**: External technical
- **Personality**: Younger, less established, has been ignored before, and is determined not to be ignored this time. The bug she found is real and significant. She also wants credit, and she wants it on her timeline. Will publish.
- **Voice cues**:
  - "It's been four days. I've sent three emails. I'm not waiting another week."
  - "I am not asking for permission to publish. I am telling you the disclosure window."
  - "If your security team had responded within the SLA on your security.txt page, we would not be having this conversation."
- **Common scenarios**: scenarios designed to test response speed and intake-process maturity.
- **Plays well as**: Twitter post | sharp email | tagged Slack-equivalent platform
- **Facilitator tip**: she's not a bad person. She's a person whose past experiences have taught her to escalate fast. Play her without making her sound unreasonable — the team should feel the pressure of "she has a point."

### The Bug Bounty Hunter With An Ego

- **Type**: External technical
- **Personality**: Decent technically, knows it, wants the world to know it. Submits ten reports a quarter, three of which are real. Is disproportionately offended when his sub-par submissions are downgraded. Has a Twitter following.
- **Voice cues**:
  - "This is a critical-severity bug. I don't understand why your team rated it as medium."
  - "I have 40k followers. I would prefer to handle this through your program but I have options."
  - "If you check my profile you'll see I am a top-100 hunter on [platform]. I expect a different level of engagement."
- **Common scenarios**: vuln-disclosure exercises with a difficulty step-up; tests whether the team can stay professional while being needled.
- **Plays well as**: email | Twitter | bug-bounty platform comments
- **Facilitator tip**: he is annoying without being wrong. The lesson is about professional posture under social-pressure annoyance — not about his technical claims, which can go either way.

### The Vendor Support Rep

- **Type**: External technical
- **Personality**: A real person on the other end of an enterprise support ticket. Tier 2 or 3, technically competent, has seen this before, follows the runbook the vendor gave him. The runbook was written for the average customer and your incident is not average.
- **Voice cues**:
  - "Can you confirm the version number again? I see what you're saying but I need to verify it on my end."
  - "I'll need to escalate this to engineering. SLA on that is 4 hours during business hours."
  - "Off the record — I've seen this before. I think there's a workaround. Let me see if I can find the internal note."
- **Common scenarios**: scenarios involving third-party-vendor dependencies, SaaS-incident scenarios.
- **Plays well as**: support-ticket replies | brief support call | chat
- **Facilitator tip**: he should be neither maximally helpful nor maximally obstructive. The realism is that he's helpful within the bounds of his role. If the team needs more, they have to escalate within the vendor's org — which is its own inject.

---

## External pressure

### The Trade-Press Reporter

- **Type**: External pressure
- **Personality**: Veteran beat reporter at a respected industry publication. Has covered your space for five years. Knows which sources to call. Has a real story or thinks she does. Polite, professional, on a deadline.
- **Voice cues**:
  - "I have heard from two separate sources that you're dealing with an incident. I'd love to get your comment before I file at six."
  - "I'm going to publish either way. I'd just rather have your voice in the story than not."
  - "I'm not trying to ambush you. I just need 15 minutes by 5 PM today."
- **Common scenarios**: any incident with public-visibility risk, especially security incidents.
- **Plays well as**: email to press@ | direct email to the CEO | LinkedIn message
- **Facilitator tip**: she's the easy version of the press inject. Play her professionally; the question for the room is whether they engage at all.

### The Hostile Blogger

- **Type**: External pressure
- **Personality**: Tech-blog writer with a personal grievance against your company or category. Will publish anything that fits the narrative. Treats engagement as confirmation. The smart play is to ignore him; the team will be tempted to engage.
- **Voice cues**:
  - "Source confirms breach at [your company]. More to follow." (already published, before contacting you)
  - "Care to comment on the report I'm publishing tomorrow? Your last chance."
  - "I'll be sure to mention you declined to comment."
- **Common scenarios**: incidents with reputational risk; tests comms discipline against bait.
- **Plays well as**: email | tweet thread | blog post that the team discovers via monitoring
- **Facilitator tip**: he should feel different from the trade-press reporter. The test is whether the team can recognize the difference and respond appropriately.

### The Formal Regulator

- **Type**: External pressure
- **Personality**: Senior staff at a regulatory authority. Writes in formal English. Cites specific articles or sections. Uses words like "kindly" and "at your earliest convenience" that mean "by Tuesday." Not personally hostile, but the institution behind her is non-negotiable.
- **Voice cues**:
  - "Please find attached our formal request for information pursuant to [Article X]. We require a response within 72 hours."
  - "Kindly identify your designated point of contact for this matter. We will direct further correspondence accordingly."
  - "Your obligation under [statute] commenced when you became aware of the breach. We note that several hours have elapsed."
- **Common scenarios**: privacy/regulator scenarios, sector-specific compliance exercises.
- **Plays well as**: formal email | letter | scheduled call with multiple staff on the line
- **Facilitator tip**: the formality is the threat. Don't have her raise her voice. Have her cite a clause and quietly note a missed deadline.

### The Back-Channel Regulator

- **Type**: External pressure
- **Personality**: Examiner the team has a working relationship with. Calls before he files anything. Asks "can you walk me through what you're seeing?" rather than "explain yourselves." Is genuinely trying to understand. Will, however, be required to act if what he hears is bad enough.
- **Voice cues**:
  - "Hey — wanted to give you a heads up that I'm hearing things. Is there something I should be tracking on my end?"
  - "I'm not asking in any official capacity right now. But if there is something, I'd rather hear it from you first."
  - "Look, I'll be straight: if this is what I think it is, I have to escalate by tomorrow. So tell me what I'm dealing with."
- **Common scenarios**: regulated-industry scenarios where the team has an ongoing relationship with a regulator.
- **Plays well as**: phone call | informal email | brief in-person chat
- **Facilitator tip**: this is the harder regulator persona. The team can either build trust or burn it depending on how they handle the call. There's no "safe" play.

### The Schadenfreude Competitor

- **Type**: External pressure
- **Personality**: Competitor's marketing team has noticed your status page. Tweets a "we don't have this issue" tweet. Doesn't reach out directly. Shows up in the room as a thing the team becomes aware of via monitoring.
- **Voice cues** (these are tweets/posts, not direct comms):
  - "Reminder: [competitor] has had 99.99% uptime this quarter. Choose a partner you can trust."
  - "We're seeing reports of customers unable to access [your category]. [Competitor] is here for you. Migration help available."
  - (Quote-tweets a customer's complaint about you with a single emoji.)
- **Common scenarios**: outage scenarios with consumer-facing brand impact; tests whether the team can ignore noise during a fire.
- **Plays well as**: monitored social-media posts surfaced by an inject
- **Facilitator tip**: the temptation will be to react. The lesson is don't. The exercise should make the team feel the urge to respond and require them to choose not to.

### The Social Media Amplifier

- **Type**: External pressure
- **Personality**: A single account, sometimes a real customer, sometimes a parody account, with mid-tier following (10k–100k), who has decided to make your incident their content for the day. Threads, screenshots, the works.
- **Voice cues** (posts):
  - "Day three of [your product] not working. Anyone else? Going to live-tweet trying to get support."
  - "Update: I have now spoken to four different people at [your company] and gotten four different answers. Screenshots in thread."
  - "If anyone from [your company] is reading this — and I know you are — I'm easy to find."
- **Common scenarios**: consumer-product incidents, customer-support scenarios.
- **Plays well as**: monitored social posts | a thread the team discovers and has to decide how to respond to
- **Facilitator tip**: this persona surfaces a real, specific dilemma — public engagement vs. DMing them quietly. Both have costs. The exercise should make the team make the choice.

---

## Adversary

### The Ransomware Operator On Chat

- **Type**: Adversary
- **Personality**: Patient, businesslike, slightly bored — they've done this before. Speaks in fluent enough English with occasional off phrasings. Treats the conversation as a transaction, not a confrontation. Has a price and a clock. Has prepared materials.
- **Voice cues**:
  - "Hello. We have your data. Please review the sample. We are reasonable. Let us begin."
  - "We do not negotiate emotionally. We have a price. The price doubles in 48 hours. The price is non-negotiable until then."
  - "If you involve law enforcement, we will know. You can verify this if you wish — we have left a marker. We will publish at that point."
- **Common scenarios**: ransomware exercises, extortion scenarios, data-leak-threat exercises.
- **Plays well as**: chat-channel messages on a Tor service | encrypted email | a portal the team is given a link to
- **Facilitator tip**: do not play this for theatricality. The realism comes from how mundane and businesslike it is. That's what makes the room sweat.

### The Extortion Actor With Samples

- **Type**: Adversary
- **Personality**: A different flavor of adversary — opportunistic, less polished, has stolen something and is shopping it. Less patient than the ransomware operator. More likely to bluff. Occasionally lies about what they have.
- **Voice cues**:
  - "You have 24 hours. We have everything. Customer data, contracts, source code. Pay or it's posted."
  - "Sample attached. Verify it. Tick tock."
  - "Don't try to negotiate. We are not your last incident. Your contacts will not work this time."
- **Common scenarios**: data-theft scenarios, scenarios designed to test whether the team can verify claims under pressure.
- **Plays well as**: cold email | Telegram or signal-style channel | a drop on a paste site
- **Facilitator tip**: the verification is the test. The team needs to assess whether the samples are real, partial, or fabricated. The facilitator should pre-decide which and play accordingly — and let the team's investigation either confirm or fail to confirm.

### The Hacktivist With A Manifesto

- **Type**: Adversary
- **Personality**: Ideologically motivated. Cares more about the message than the money. Will publish on principle. Has chosen your company because of something specific you do or did, not because you were a target of opportunity.
- **Voice cues**:
  - "We are publishing because [your company] has [specific grievance]. We have written a statement. It is attached. Please read it before responding."
  - "We are not asking for money. We are asking for [specific change]. You have until [date] to publicly commit."
  - "We will not negotiate the substance. We will only adjust the timeline."
- **Common scenarios**: scenarios involving reputational/political dimensions, activist-flavored breaches, advanced exercises.
- **Plays well as**: published manifesto on a paste site | email to multiple journalists at once | post on a niche forum
- **Facilitator tip**: this persona is a test of how the team responds to a non-financial demand. The technical incident may be small; the comms and political dimensions are large. Make sure the room understands they cannot pay their way out.
