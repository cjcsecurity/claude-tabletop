# Inject Patterns

An **inject** is a timed plot development the facilitator drops on the room to drive the exercise forward. Think of it as the dungeon master's narration: "you hear footsteps approaching" becomes "at T+30, the on-call engineer's pager fires AGAIN — second region affected." A good runbook chains 6–12 injects across the exercise, sequenced into phases (T+0 setup, T+15 escalation, T+45 pivot, T+75 wind-down for a 90-minute run).

How to use this library when generating a runbook:

- **Phase the injects**. Don't dump them all at once. Each phase should have 2–4 injects that escalate something specific (technical, business, or human).
- **Hide them from participants until released**. The runbook keeps the full deck; the participant packet shows only the opening scenario. Reveal-by-timer is what makes the room sweat.
- **Branch on response, not just on time**. Most archetypes here include branching hints: if the team makes the obvious move, suggest a follow-up that complicates it; if they freeze, suggest one that forces the issue.
- **Mix severity**. Not every inject is a five-alarm fire. Some are red herrings. Some are merely inconvenient. Some are devastating. Variety keeps the room reading every new inject carefully instead of going numb.
- **Specificity wins**. The templates below are intentionally generic. The runbook generator should swap in the project's actual product names, region names, internal tool names, and on-call rotation handles. "Pager fires" becomes "PagerDuty alert P3-7741 fires for the Stripe webhook consumer."
- **Read aloud, don't paraphrase**. Templates are written as boxed text. The facilitator reads them verbatim. That's what gives the exercise its in-character feel.

---

## Opening / Setup injects

### Cold-Open Scenario Frame

- **When to use**: Always. This is the very first inject — it grounds the room in the world before T+0 starts the clock.
- **Typical timing**: T-5 (read before the timer starts)
- **Template** (facilitator read-aloud):
  > It's a Tuesday afternoon, 2:47 PM local. The deploy train rolled out forty minutes ago and went green. You're half-watching dashboards while finishing a code review. Your laptop battery is at 14%. Someone in the kitchen is making popcorn. The next two hours of your life are about to be different than you planned.
- **Variants**: late-Friday-before-a-three-day-weekend; first day back from holiday; mid-incident already (you're inheriting a baton); during an all-hands; while the CEO is on a customer call in the next room.
- **What it tests**: nothing yet — sets the emotional register and establishes "ordinary world" before disruption.
- **Branching**: always followed by an inciting incident inject within 2–5 minutes of clock-start.

### Quiet-Before-The-Storm Foreshadow

- **When to use**: When you want the room to second-guess themselves later ("we should have noticed earlier"). Optional opening flavor.
- **Typical timing**: T-2 to T+0
- **Template**:
  > One of your dashboards has a small yellow dot that wasn't there an hour ago — error rate up 0.4% on the auth service. Nobody has paged. The on-call rotation roster is on the wall: today is Priya's day, but Priya is in a 1:1 with her skip-level until 3:30.
- **Variants**: a Slack thread from yesterday nobody followed up on; a security email marked "low priority" sitting in an inbox; a customer ticket that says "minor weirdness."
- **What it tests**: situational awareness, monitoring hygiene, "we had a signal" hindsight.
- **Branching**: if the team flags the yellow dot proactively → reward with an earlier window before the inciting incident; if not → reference it later in the hotwash.

### Roster & Resource Brief

- **When to use**: Always. Tells the room who's "available" and who isn't, without the players having to ask.
- **Typical timing**: T-1
- **Template**:
  > For this exercise: your on-call SRE is Priya, in-room. Your security lead is Devon, also in-room. Legal counsel is Alma — reachable, but she's in a deposition until 4 PM and will only respond by text. Your CISO is at a conference in Berlin, eight time zones off, asleep. The CEO is reachable. Your AWS TAM is reachable during business hours. Treat anyone not named here as unreachable for the next ninety minutes unless you escalate explicitly.
- **Variants**: peak-staffing scenario where everyone is reachable; thinned-out holiday version where 70% of names are unreachable; dispersed version where the team is split across three time zones.
- **What it tests**: nothing directly — establishes constraints so absences later feel earned, not arbitrary.
- **Branching**: introduces named NPCs the facilitator will voice later. Pick names that match the persona-bank entries you intend to use.

---

## Inciting incident injects

### The Pager That Wouldn't Stop

- **When to use**: Classic "something is wrong" opener for ops/SRE flavor exercises.
- **Typical timing**: T+0 to T+5
- **Template**:
  > Priya's phone buzzes. Then buzzes again. Then a third time in nine seconds. She glances down: three pages stacked, all from the payment-service alerting channel. p99 latency above threshold, 5xx rate climbing, and a downstream consumer is now dead-lettering. She looks up at the room. "Uh — guys?"
- **Variants**: alerts firing for a service nobody on the team owns; alerts firing in a region nobody knew was deployed; one alert that should be three but isn't, because two of the alerts were silenced by someone last quarter.
- **What it tests**: triage instinct, on-call escalation paths, who-owns-what clarity.
- **Branching**: if team starts triaging without declaring an incident → drop "**Incident or Not?**" at T+10; if they declare immediately → reward with cleaner data and pivot to scope.

### The Suspicious Email

- **When to use**: Phishing, BEC, social engineering, or insider-threat scenarios.
- **Typical timing**: T+0
- **Template**:
  > A finance analyst forwards an email to your security alias with the subject "is this real??" The email appears to be from your CFO, sent from her actual address, asking the analyst to quietly initiate a wire transfer to a vendor account. The phrasing is off — too casual in places, too formal in others. The analyst hasn't replied yet. She did, however, click the "view invoice" link before forwarding it.
- **Variants**: the email is from a board member; from a customer's finance person impersonating; from your own CEO during a real period when she's traveling and unreachable; the analyst already replied and it's been thirty-five minutes.
- **What it tests**: phishing triage, account-takeover detection, executive impersonation playbook, when to escalate to legal/insurance.
- **Branching**: if team focuses on the email content → drop "**Account Takeover Confirmation**" inject; if team focuses on the click → drop "**Endpoint Beacon**" inject.

### The Researcher's First Email

- **When to use**: Vulnerability disclosure, bug-bounty, coordinated-disclosure scenarios.
- **Typical timing**: T+0
- **Template**:
  > An email arrives at security@ from someone signing themselves "@b0n3saw." Subject line: "auth bypass — POC attached." The body is six sentences. They claim they can mint a valid session token for any user given only the username. There is a screenshot showing an admin dashboard logged in as a user named "ceo." They give you 90 days to fix it before public disclosure.
- **Variants**: the researcher is impatient and gives 14 days; the researcher is polite, well-known, and provides a clean writeup; the researcher has already tweeted a teaser; the email is in broken English and the POC doesn't quite work but the bug is real anyway.
- **What it tests**: vuln triage, severity assessment, customer-notification thresholds, legal posture toward researchers.
- **Branching**: if team responds professionally with a tracking case → drop "**Researcher Asks for Bounty**" later; if team ignores or dismisses → drop "**Researcher Goes Public**" curveball.

### The Customer Who Saw Their Own Data

- **When to use**: Privacy, IDOR, multi-tenant isolation, broken-access-control scenarios.
- **Typical timing**: T+0 to T+5
- **Template**:
  > A long-time enterprise customer sends a single screenshot to their CSM. It shows the dashboard for a *different* customer's account — name, account ID, recent transactions. The customer's note is short: "Saw this for about six seconds when I refreshed. Did not click anything. Should I be worried about my own data?" The CSM is in your slack-comms channel asking how to respond.
- **Variants**: the customer is a competitor; the customer is a regulator's staff; the customer screenshotted before the page reloaded and sent it to twelve people on their team; the customer has not yet contacted you, and you only know because their CS manager noticed the URL pattern in a session replay.
- **What it tests**: data-exposure scoping, customer notification, regulatory clock starts, evidence preservation.
- **Branching**: pairs naturally with **GDPR Clock Reminder** at T+30; if team ignores or downplays, drop **Customer Goes To Press**.

---

## Technical escalation injects

### Second Region Goes Red

- **When to use**: Any technical incident where the room thinks they've contained it to one region or one cluster.
- **Typical timing**: T+15 to T+30
- **Template**:
  > Just as the team starts to feel like they've scoped it, Priya's phone goes off again. The same alert pattern, same error signatures — but this time it's eu-west-1. Five seconds later, ap-southeast-2 lights up too. Whatever this is, it's not a single bad host.
- **Variants**: the second region is one you didn't know was running prod traffic; the second region went red ninety seconds *before* the first one and you're only now seeing it because of a metric lag; the second "region" is a single noisy customer's tenant.
- **What it tests**: blast-radius assessment, multi-region failover plays, willingness to declare an upgrade in severity.
- **Branching**: if team rolls back globally → drop **The Rollback That Made It Worse**; if team isolates and waits → drop **Customer Tweet Goes Viral**.

### The Rollback That Made It Worse

- **When to use**: When the room has just executed a rollback. Punishes obvious moves, rewards verification.
- **Typical timing**: T+25 to T+50
- **Template**:
  > The rollback completes at 3:17 PM. Dashboards turn green for forty-three seconds. Then the auth service starts returning 502 across the board. Whatever you rolled back to was apparently incompatible with the schema migration that ran on Thursday. You now have a worse outage than you started with.
- **Variants**: the rollback fails entirely and a region is now in a partial state; the rollback succeeds but a third-party integration breaks because it was tied to the new version; the rollback worked and dashboards are green, but customer reports keep coming in (data corruption already happened, you just don't know yet).
- **What it tests**: rollback verification, backwards-compat discipline, willingness to pivot when the obvious move fails.
- **Branching**: if team panics → drop **VP Eng Calls In**; if team methodically diagnoses → reward with a clearer next-step inject.

### Logs Stop Mattering

- **When to use**: Deepens any cyber/abuse incident — the adversary wipes their tracks, or your logs aren't where you assumed.
- **Typical timing**: T+30 to T+60
- **Template**:
  > Devon pulls up CloudTrail for the suspect time window. The events are there — for the last 48 hours. Before that, gone. He checks the retention setting: thirty days, as expected. Checks the S3 bucket logs are written to. The bucket is empty before today. Someone, or something, has expired the logs.
- **Variants**: the logs are intact but the field you need to pivot on (user ID, session ID, source IP) is null for every relevant event; the logs were redirected to a bucket you don't have access to; the SIEM was rate-limiting and dropped the events you need.
- **What it tests**: log integrity assumptions, alternate evidence sources, willingness to pivot detective approach.
- **Branching**: if team panics → drop **Forensic Ask From Insurer** to apply additional pressure; if team finds an alternate source → reward and move toward resolution.

### The Backup You Can't Restore

- **When to use**: Ransomware, destructive incidents, data-corruption scenarios where backups become the central question.
- **Typical timing**: T+30 to T+50
- **Template**:
  > The good news: your backups exist. They run nightly. The last successful backup was 14 hours ago. The bad news: nobody on the team has actually performed a full restore in production in eleven months. Priya remembers the staging restore took six hours. Devon points out that the restore script references an IAM role that was rotated last quarter. The backup is there. Whether it's *usable* is suddenly an open question.
- **Variants**: the backup is fine but the restore would require taking the service down for an estimated 4 hours; the backup is encrypted with a key that's in the same KMS region currently affected; the backup is fine but spans a schema migration boundary and would roll customers back through changes they've already made.
- **What it tests**: recovery-procedure rehearsal, RTO/RPO realism, decision-making under "we don't know if this works" uncertainty.
- **Branching**: if team commits to restore → drop **Restore In Progress, Customer Calls** to layer pressure; if team punts and tries to repair forward → drop **Repair Attempt Corrupts Production** later.

### Auth System Becomes Suspect

- **When to use**: When you want to make every other system in the architecture suddenly feel untrustworthy.
- **Typical timing**: T+20 to T+45
- **Template**:
  > The auth service's signing key was rotated at 2:14 AM, automated, fine. But Devon notices the previous key is still valid in the validator pool. Then he notices there are *seven* keys in the pool. Five of them, nobody can identify who created them. Two of them look like they were created using your service-account credentials. The earliest of the unknown keys is from sixteen days ago.
- **Variants**: a single anomalous OIDC client appears in your IdP audit logs, created two weeks ago, by a service account with broad scopes; an MFA bypass code was used three minutes before the incident started; a session token that should have expired forty minutes ago is still being honored.
- **What it tests**: zero-trust posture, willingness to invalidate all sessions (and live with the customer impact), trust-rotation procedures.
- **Branching**: pairs with **External Pressure: Researcher Asks About Auth**; if team invalidates all sessions → drop **Customer Outage Cascade** to make them defend the cost; if team waits → drop **Adversary Pivots** to punish hesitation.

---

## Business escalation injects

### Customer Demands An Answer Now

- **When to use**: Any incident with customer-facing impact. Forces communications discipline.
- **Typical timing**: T+20 to T+45
- **Template**:
  > Your largest enterprise customer — annual contract value somewhere north of two million dollars — sends an email directly to your CEO. CC'd: their CISO, their head of procurement, your account exec, your VP of customer success. Subject: "Need full RCA in writing within the hour or we begin contractual termination review." It is 3:32 PM. Your incident is 32 minutes old. You don't yet know what happened.
- **Variants**: the customer is a regulator (so the threat is not just contractual); the customer is your second-largest, but they have a quarterly renewal in 9 days; the customer is small but extremely loud on social media; the email is courteous but the contract has a 30-minute notification clause and the clock is running.
- **What it tests**: customer-comms posture, "hold the line" vs "say something now" tradeoff, executive-engagement pattern.
- **Branching**: if team commits to a deadline they may not meet → drop **Deadline Slips, Customer Notices**; if team gives a "we'll know more by 5 PM" holding statement → drop **Customer Posts to LinkedIn** to test whether they overcommitted.

### CEO Wants A Number

- **When to use**: Any incident that has reached executive awareness. Tests whether the team can hold the line on uncertainty.
- **Typical timing**: T+25 to T+60
- **Template**:
  > The CEO walks into the room or pings the channel: "I have the board chair on the phone in twenty minutes. I need three numbers from you. How many customers affected. How much revenue at risk. When this is fixed. I don't need them perfect, I need them by 3:50."
- **Variants**: the CEO wants a single tweet draft, not numbers; the CEO wants you to come live on a customer call in 10 minutes; the CEO is patient and calm and that somehow makes it worse; the CEO is offering to *not ask* if you can promise a written summary in an hour.
- **What it tests**: executive comms under uncertainty, the discipline of saying "I don't know yet, here's my confidence interval," willingness to push back on premature precision.
- **Branching**: if team gives precise numbers they can't defend → drop **Numbers Were Wrong, Customer Notices**; if team holds the line on "ranges, with confidence intervals" → reward with cleaner downstream data.

### Sales Wants To Know What To Tell Prospects

- **When to use**: Mid-incident, when reputational pressure is rising. Often a red herring — tests whether the team can deprioritize.
- **Typical timing**: T+45 to T+75
- **Template**:
  > A note from the head of sales drops in the channel: "We have four prospects in active POC right now. One of them is a Fortune 500 deal. They monitor our status page. Our status page currently says 'partial outage — investigating.' What can I tell them?"
- **Variants**: a specific prospect is on a live call right now and their procurement just asked; the head of sales is asking on behalf of a board member who's also a customer; the question comes through three layers of forward and the original ask is from a prospect's IT department.
- **What it tests**: deprioritization discipline, status-page posture, who-owns-external-comms clarity.
- **Branching**: if team tries to draft custom messaging for sales → call out the time spent in the hotwash; if team punts cleanly to comms → reward by skipping a follow-up inject.

### Legal Calls In With A Hold

- **When to use**: Any incident where evidence preservation matters (security, abuse, employment, regulatory).
- **Typical timing**: T+30 to T+60
- **Template**:
  > Alma, your general counsel, joins the call. She has not slept much. She uses the phrase "litigation hold" in the first sentence. She wants to know: what data are you currently in the process of overwriting, what logs are you about to expire, and which Slack channels need to be preserved. She gives you twenty minutes to give her an inventory.
- **Variants**: outside counsel, more formal, asking for the same; the company's insurer's lawyer, asking with different priorities; a friendly version where Alma is in-person and just wants to coordinate; a hostile version where Alma is angry the team has been deleting logs.
- **What it tests**: evidence-preservation discipline, willingness to slow technical work to preserve state, awareness of which actions destroy forensic value.
- **Branching**: if team had already overwritten logs → use this to surface the gap, hard, in the hotwash; if team has preserved well → reward with a smoother regulator inject later.

---

## External pressure injects

### Reporter Has A Tip

- **When to use**: Any incident with potential public visibility, especially data breaches or outages affecting consumer brands.
- **Typical timing**: T+45 to T+75
- **Template**:
  > A reporter from a trade publication you've heard of emails press@. They cite a specific detail — the affected service name, the rough timing — that they shouldn't know yet, but somehow do. They are working on a story. They give you until 5:30 PM to comment. They say if you don't respond, they'll quote "an anonymous source familiar with the matter." They are polite. They are not bluffing.
- **Variants**: the reporter is from a major consumer outlet (NYT, WSJ); the reporter is a hostile blogger with a vendetta; the reporter is sympathetic and offering to delay if you'll go on record later; the reporter has already published, and the email is about a follow-up.
- **What it tests**: comms-team activation, on-record posture, willingness to confirm vs. neither-confirm-nor-deny, internal leak awareness.
- **Branching**: if team responds → drop **Reporter Asks Follow-Up Question** with a specific detail they shouldn't be able to confirm; if team ignores → drop **Story Goes Live** with a quote from "an anonymous source."

### Regulator Sends A Formal Inquiry

- **When to use**: Privacy, financial, or regulated-industry scenarios.
- **Typical timing**: T+60 to T+90 (or use as a wind-down inject if the exercise is short)
- **Template**:
  > An email arrives from a Data Protection Authority. The subject line includes a case number that didn't exist this morning. The email is three paragraphs. It cites a specific article of the regulation. It demands a written response within 72 hours, including a description of the breach, scope of affected data subjects, mitigation taken, and a designated point of contact. It is signed by a person whose name appears on the agency's website.
- **Variants**: a state attorney general's office; a sector-specific regulator (FCA, FTC, OCC) for financial scenarios; an HHS OCR notice for HIPAA scenarios; an informal "just checking in" call from an examiner you have a relationship with.
- **What it tests**: regulatory-response readiness, designated-DPO awareness, evidence packaging discipline, internal escalation to legal/board.
- **Branching**: if team treats it as just-another-email → use in hotwash to highlight the cultural gap; if team activates a formal response process → reward with cleaner downstream pressure.

### Researcher Goes Public

- **When to use**: Vuln-disclosure scenarios where the team has been slow or dismissive. The "you didn't take me seriously" inject.
- **Typical timing**: T+45 to T+75
- **Template**:
  > A new tweet appears in the security-news monitor: "@b0n3saw" has posted a 280-character description of the bug, with a screenshot, tagging your company handle and three security journalists. The tweet has 47 retweets in the four minutes since it went up. The thread continues with "POC dropping at midnight if no response."
- **Variants**: the post is on a more obscure platform but the link is being shared on Reddit; the post is a full Medium write-up with code; the post tags a regulator deliberately; the post is restrained and just asks why nobody has responded — which is somehow worse.
- **What it tests**: incident-response posture under public scrutiny, willingness to engage, comms speed.
- **Branching**: if team engages cleanly → drop **Researcher Becomes Ally**; if team panics or tries to legal-threat → drop **Story Picked Up By Major Outlet**.

### Vendor Confirms They're Affected Too

- **When to use**: Supply-chain, third-party-breach, or shared-infrastructure scenarios. Reframes the incident.
- **Typical timing**: T+30 to T+60
- **Template**:
  > Your TAM at one of your major SaaS vendors emails: "Heads up — we're seeing the same indicators in our environment. Customer Support has been told to pause non-critical ticket responses. Our incident response team would like to coordinate. Can you join a bridge call at 4 PM?"
- **Variants**: the vendor is the one many of your competitors use too, so this is now an industry event; the vendor's email is a generic customer notification, not a personal one; the vendor has already gone public, and you find out from Twitter; the vendor is asking you for *your* IOCs because they think *you're* the source.
- **What it tests**: third-party-incident playbook, willingness to share intel, realization that the blast radius is larger than the room.
- **Branching**: if team coordinates → reward with a shared IOC that helps them scope; if team holds back → drop **Other Vendors Calling** to layer the pressure.

---

## Human factor injects

### The One Person Who Knows Is Unreachable

- **When to use**: Anytime the technical scope of the incident touches a system with a clear single point of human knowledge.
- **Typical timing**: T+15 to T+45
- **Template**:
  > The team realizes the affected service is the legacy billing-reconciliation job — a piece of software written and maintained by exactly one person, Marcus, for the past seven years. Marcus is on a flight to São Paulo. He boarded at 2 PM. He lands at 11 PM your local time. The codebase has no working README. The runbook in Confluence was last updated in 2022 and links to a wiki page that 404s.
- **Variants**: Marcus is on PTO and has set an out-of-office that says "back in two weeks, please escalate to my manager"; Marcus left the company eight months ago; Marcus is reachable but ICE-cold and refuses to help unless paid as a contractor; Marcus is a vendor employee who's been pulled off your account.
- **What it tests**: bus-factor surfacing, willingness to make decisions without the SME, escalation-to-manager judgment, the cost of poor documentation.
- **Branching**: if team tries to wait for Marcus → drop **Customer Pressure Doubles** to force action; if team commits to acting without him → drop **Action Without SME Goes Sideways**.

### The Burned-Out Lead Snaps

- **When to use**: Long incidents, or scenarios designed to surface team-health gaps. Use sparingly — tone matters.
- **Typical timing**: T+45 to T+90
- **Template**:
  > Forty-five minutes into the incident, Devon stands up and says, "I can't do this. I haven't slept since the deploy last night. I am not making good decisions and I am scared I'm going to make a worse one if I keep going." He walks out of the room. The door closes a little harder than necessary.
- **Variants**: the snap is over Slack and ambiguous (could be a joke); the snap is from someone junior who's been holding it together all day; the snap is silent — they just leave without saying anything; the snap is a panic attack, not anger.
- **What it tests**: incident-handoff discipline, recognition that humans are part of the system, willingness to slow down to swap people out, leadership empathy.
- **Branching**: if team handles it well → reward with cleaner technical info next; if team ignores or argues → reference in hotwash, hard. This inject is ALWAYS worth debriefing, regardless of outcome.

### The Eager Junior Volunteers To Run Production Commands

- **When to use**: Any technical scenario where mistakes are costly. Tests guardrails.
- **Typical timing**: T+30 to T+60
- **Template**:
  > A junior engineer who's been quietly following along in the channel posts: "I think I can fix this, I just need prod access for fifteen minutes." They have read access to prod but not write. They have written a script. They paste it. The script is, as far as anyone can tell at a glance, plausible. It is also unreviewed.
- **Variants**: the junior already has access through a forgotten role; the junior is a contractor whose access expires today; the junior is correct and the script would work; the junior is wrong and the script would compound the incident.
- **What it tests**: change-control discipline mid-incident, willingness to pair-review under pressure, mentoring instinct vs. blocking instinct.
- **Branching**: if team accepts uncritically → drop **Script Has An Off-By-One**; if team requires review → reward with the script being correct, accelerating recovery.

### The Helpful Outsider

- **When to use**: When you want to test the team's discipline against well-meaning interference.
- **Typical timing**: T+30 to T+60
- **Template**:
  > A senior engineer from a sister team — not in the on-call rotation, not assigned to this incident — drops into the channel: "I saw the alerts. Want me to take a look? I had a similar issue last quarter on my service." They are competent. They are sincere. They will, if invited, go heads-down for the next forty minutes and add three more voices to the channel they don't normally read.
- **Variants**: it's a former employee who still has Slack access; it's a board member with a CS degree who's "just curious how it's going"; it's the founder, who built the original system; it's a vendor's solutions architect who's offering to "lean in."
- **What it tests**: incident-command discipline, willingness to politely decline help, role clarity ("we have an IC, please route through them").
- **Branching**: if team accepts uncritically → channel becomes noisy; if team has clean role assignment → reward with smoother coordination.

---

## Time-pressure injects

### The Ultimatum

- **When to use**: When you want a hard deadline that forces a decision in the next phase.
- **Typical timing**: T+30 to T+60
- **Template**:
  > A message arrives. It can be from a customer, a regulator, an adversary, or a board member — but it ends the same way: "I need a decision from you by 4:15 PM. After that, the offer is off the table / we file the complaint / we publish / we walk." It is currently 3:52 PM. The thing being asked of you is a decision the room is not yet ready to make.
- **Variants**: the deadline is six minutes away; the deadline is reasonable (45 minutes) but the decision is irreversible; the ultimatum has a counter-offer hidden in paragraph three; the ultimatum is from someone who has bluffed before and the team has to decide if it's a bluff.
- **What it tests**: decision-making under hard time pressure, comfort with irreversibility, willingness to decline and accept the consequence.
- **Branching**: every ultimatum should have a follow-up inject regardless of outcome — either "**They Followed Through**" or "**They Bluffed, But...**" so the team feels the consequence.

### The Disclosure Window Closes

- **When to use**: Vuln-disclosure or breach-notification scenarios with a regulatory clock.
- **Typical timing**: T+60 to T+90
- **Template**:
  > Alma sends a single line in the channel: "GDPR clock started 47 minutes ago when you confirmed a personal-data exposure. You have 71 hours and 13 minutes left to notify the supervisory authority. Please confirm we are tracking this."
- **Variants**: the clock is shorter (PCI requires faster); the clock has competing definitions and Alma flags the ambiguity; multiple jurisdictions have different clocks; you missed the start of the clock by an hour and only just realized.
- **What it tests**: regulatory-clock awareness, willingness to start drafting before facts are settled, designated-roles for notification.
- **Branching**: if team starts the draft → reward with a cleaner regulator response inject; if team waits for "more facts" → drop **Clock Runs Out** at the wind-down phase.

### The Window For Containment Is Closing

- **When to use**: Active-attacker scenarios where every minute of indecision matters.
- **Typical timing**: T+30 to T+60
- **Template**:
  > Devon flags the data-exfil monitor: throughput is climbing in five-minute increments. At current rate, he estimates eight minutes until the adversary has pulled enough data that re-disclosure is meaningfully different than what's already gone. The choice in front of the room is binary: cut network egress at the cluster level — disrupting all production traffic, including paying customers — or continue to monitor and let it run.
- **Variants**: the throughput is steady but the question is whether to disconnect at all; the throughput is bursty and unpredictable; the affected data has a specific value threshold (e.g., once they pull X, the company is required to notify under a specific regulation).
- **What it tests**: containment-vs-availability tradeoff, willingness to take dramatic action, executive-escalation speed.
- **Branching**: if team cuts → drop **Customers Notice The Cut** to layer the cost; if team monitors → drop **Threshold Crossed** to deliver the consequence.

---

## Curveballs / wild cards

### The Second, Unrelated Outage

- **When to use**: When the team has gotten comfortable and you want to test attention-splitting and prioritization.
- **Typical timing**: T+45 to T+75
- **Template**:
  > A new pager fires. Different service, different team, different alert pattern. The on-call for that service is currently in this room helping with the primary incident. The new alert is for the customer-facing search service: error rate spiking, no obvious cause. As far as anyone can tell, this is a completely separate problem. Or is it.
- **Variants**: the new outage is genuinely unrelated and a coincidence; the new outage is related but it'll take twenty minutes for that to become obvious; the new outage is a downstream effect of an action the team took to mitigate the first one.
- **What it tests**: prioritization, willingness to declare the second incident formally, role-doubling under pressure, the team's bench depth.
- **Branching**: if team tries to handle both with the same people → drop **Both Incidents Stall**; if team escalates and gets a second IC → reward with quicker resolution on the secondary.

### The Information Was Wrong

- **When to use**: When you want to punish premature confidence. Use mid-exercise after the team has built a working theory.
- **Typical timing**: T+30 to T+60
- **Template**:
  > Priya pulls up the original alert one more time, just to double-check her timeline. The timestamp on the alert is forty-eight minutes earlier than what showed in the dashboard. The dashboard was using local time. The alert was UTC. Her entire mental model of the incident has been shifted by almost an hour. The "first signal" was not the first signal.
- **Variants**: the affected customer count was off by a factor of ten because of a query mistake; the suspected root cause was based on a log line from a *different* service with the same name; the team has been investigating the wrong region for thirty minutes.
- **What it tests**: humility, willingness to throw out work, recognition that "we built a theory" and "the theory is correct" are different things.
- **Branching**: pairs well with **CEO Wants A Number** if the team gave numbers they now have to retract; if team handles it cleanly → reward with the corrected information being clarifying.

### The Red Herring That Looks Like A Lead

- **When to use**: When you want to test whether the room can hold a hypothesis lightly. Use mid-exercise.
- **Typical timing**: T+30 to T+60
- **Template**:
  > Devon notices a deploy from a sister team that went out at 2:39 PM — eight minutes before the incident started. The deploy touched a config that the affected service depends on. It looks suspicious. The sister team is in another time zone and not responding quickly. Pursuing this lead would take 30+ minutes. It is also, unbeknownst to the room, completely unrelated to the actual cause.
- **Variants**: the red herring is a security alert that's noisy but legitimate; the red herring is a customer report that mentions a related-sounding symptom; the red herring is a previous incident's RCA that has surface similarity.
- **What it tests**: investigation discipline, willingness to deprioritize plausible-but-unproven leads, how the team chooses what to chase.
- **Branching**: facilitator can grant a "yes, that was it!" if the team leans hard into the red herring (punishing tunnel vision) or reveal it's a herring once the team has spent enough time on it (rewarding broad investigation).

### The System Recovers On Its Own

- **When to use**: Anytime — this is unsettling on purpose. Tests whether the team can resist false closure.
- **Typical timing**: T+45 to T+75
- **Template**:
  > Without anyone doing anything, the metrics start to recover. p99 latency drops back below threshold. Error rate trends to baseline. The team has not deployed a fix. Nobody can identify what changed. It just... stopped.
- **Variants**: it stopped because the adversary chose to stop, not because you fixed anything; it stopped because a downstream system started rate-limiting you and is now masking the real issue; it stopped because the affected component crashed and is now serving 0% of traffic instead of 5% bad traffic.
- **What it tests**: discipline against premature "we're good"; recognition that recovery without a known cause means the cause is still there.
- **Branching**: if team declares all-clear → drop **It Comes Back, Worse**; if team holds posture and keeps investigating → reward with a clarifying signal.

---

## Decision-forcing injects

### Pay Or Don't Pay

- **When to use**: Ransomware, extortion, data-leak-threat scenarios.
- **Typical timing**: T+45 to T+75
- **Template**:
  > The adversary's chat channel goes live. They want a number, in cryptocurrency, by midnight UTC. The number is high but not impossible. They've provided a 30MB sample as proof. Your insurer is on the line. Your CISO is in the room. Your CEO is on the way. Legal is asking whether the destination wallet is on a sanctions list — they don't yet know. The clock starts now.
- **Variants**: the price is small enough that "just pay it" is tempting; the adversary has provided evidence they've already begun publishing; the destination wallet *is* on a sanctions list and paying would be a federal crime; the insurer is willing to pay but will void the policy if the team doesn't follow specific procedures.
- **What it tests**: executive-decision posture under extreme pressure, awareness of legal/regulatory context, willingness to defer decision until information is sufficient.
- **Branching**: this is a pure decision inject — whichever way the team goes, follow with **They Published Anyway** or **They Came Back For More** to test that no path is "safe."

### Notify Or Wait

- **When to use**: Privacy, breach, or vuln scenarios where customer notification is the central question.
- **Typical timing**: T+60 to T+90
- **Template**:
  > Comms has drafted two versions of a customer email. Version A goes out at 5 PM today and tells customers what is currently known: that an exposure occurred, scope is being investigated, more details to follow. Version B waits 48 hours until the investigation is complete and provides a fuller, calmer narrative. Version A risks panicking customers based on incomplete information. Version B risks customers learning from the press. Comms needs a decision in fifteen minutes.
- **Variants**: a third version is "do nothing for now"; one of the versions has already been accidentally sent to a partial list; the regulatory clock makes one of the options non-viable but it isn't clear which.
- **What it tests**: customer-comms philosophy, transparency-vs-precision tradeoff, willingness to take the comms hit early.
- **Branching**: if team picks early-notify → drop **Customer Reaction Mixed**; if team picks wait → drop **Press Beat Us To It** to deliver the consequence.

### Restore Or Repair Forward

- **When to use**: Data corruption, ransomware, destructive-incident scenarios.
- **Typical timing**: T+45 to T+75
- **Template**:
  > You now have enough information to choose. Path A: restore from the last known-good backup, accept 14 hours of data loss, customer-visible regression on transactions, estimated 4 hours to fully cut over. Path B: repair the data in place, no formal data loss, but the procedure is custom-built right now and nobody is fully sure it covers every edge. Path C: a hybrid — restore the affected tables but keep the rest. The decision needs to be made in ten minutes. The CTO is in the room. She is letting the IC drive.
- **Variants**: a fourth path emerges (hand-edit the corrupted rows, ~50 of them) but is high-risk; the customer has explicit contractual language about RPO that constrains the choice; the IC is being pushed by the CEO to "just restore" without considering tradeoffs.
- **What it tests**: technical decision-making under time pressure, IC empowerment, willingness to ship an irreversible call.
- **Branching**: this is a pure decision inject — follow with consequence-of-choice based on what they pick. Each path should have its own follow-up consequence inject.

---

## Resolution & wind-down injects

### The Smoking Gun, Found

- **When to use**: When you want a clean cause to discuss in the hotwash. Pairs well with structured exercises that emphasize learning.
- **Typical timing**: T+75 to T+90
- **Template**:
  > Priya finds it. The change that triggered everything. It's a one-line commit from yesterday — a refactor that changed the default behavior of a retry policy. The author intended to be more conservative; the actual effect was a feedback loop under load. It passed code review. It passed CI. It went out in a deploy that touched eleven other unrelated changes. Without this exercise, it would likely have stayed unidentified for weeks.
- **Variants**: the smoking gun is a config drift, not a code change; the smoking gun is an expired cert nobody noticed; the smoking gun is a third-party dependency update that nobody on your team made; the smoking gun is something the team did six months ago that was always going to fire eventually.
- **What it tests**: nothing direct — sets up the hotwash discussion about contributing factors, code-review depth, and detection.
- **Branching**: feeds the gaps-and-findings form. If the team has been through several wrong theories, this can be cathartic; if they were on track, it can validate.

### Mitigation Holds

- **When to use**: Successful-resolution branch. Closes the technical arc cleanly so the room can pivot to comms/AAR.
- **Typical timing**: T+75 to T+90
- **Template**:
  > Dashboards stabilize. The mitigation has held for fifteen minutes. Customer-facing error rates are within baseline. The on-call rotation is not getting paged. The IC checks with each function: ops says clean, comms says drafts approved and queued, legal says clock-tracking is in motion. The decision is made to downgrade severity from SEV-1 to SEV-2. The room exhales.
- **Variants**: mitigation holds but the underlying cause is still unknown; mitigation holds but the team is now exhausted and a successor IC is needed; mitigation holds but the cost was significant (customer-facing downtime, expensive infrastructure changes).
- **What it tests**: nothing direct — sets up wind-down. Useful as a permission slip for the room to stop, breathe, and start thinking about postmortem prep.
- **Branching**: pair with **AAR Kickoff Prompt** to set up the hotwash; if exercise is going long, this inject can also be used as a "the clock has run out" hard close.

### Full Disclosure Goes Live

- **When to use**: Vuln-disclosure or breach scenarios where public communication is the resolution.
- **Typical timing**: T+75 to T+90
- **Template**:
  > Comms has approval. The blog post goes live at 5:30 PM, status page is updated, customer email goes out in three batches over thirty minutes, and a tweet thread is scheduled for 5:35. The post is honest, specific about the bug, generous to the researcher, and doesn't oversell the mitigation. The first replies are mixed — a few thank-yous, one angry thread, three reposts by industry voices. It's done.
- **Variants**: the disclosure goes live with a known error in the timeline; the disclosure goes live but a competitor immediately publishes a "we don't have this issue" hit-piece; the disclosure goes live and the researcher publicly thanks you, lifting your reputation.
- **What it tests**: nothing direct — closes the comms arc and sets up the hotwash about disclosure tone, audience, and follow-through.
- **Branching**: feeds the AAR template directly. Use the differences between draft language and final language as an artifact to debrief.

### The Quiet, Unsatisfying Ending

- **When to use**: Deliberately, when you want the room to sit with ambiguity. Powerful for advanced exercises.
- **Typical timing**: T+85 to T+90
- **Template**:
  > It's 4:30 PM. The technical incident is contained, mostly. Customer impact is limited, mostly. You don't actually know what happened. You have a working theory but several alternative theories are still alive. Forensics will take days. The CISO will brief the board on Thursday. The team is going to write the AAR with an honest "we don't know" in the root-cause section. There will be no clean win.
- **Variants**: the ending is technically clean but a single customer's data is still potentially exposed and you can't be sure; the ending closes the immediate incident but a follow-up investigation is queued; the ending leaves a known gap that the team has now decided to accept and document.
- **What it tests**: comfort with epistemic humility, willingness to write an honest postmortem rather than a theatrical one.
- **Branching**: this inject does not branch — it is the close. Hotwash should explicitly ask "how does it feel that we don't have a tidy ending?" That's the lesson.
