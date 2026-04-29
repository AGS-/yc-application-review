---
company: Bedrock (Standard Treasury)
batch: S13
outcome: accepted
source_url: https://blog.zactownsend.com/our-yc-s13-application
form_version: 2013
verbatim: true
partial: true
notes: |
  Zac Townsend published the application he and Dan Kimerling submitted
  for "Bedrock" — which became Standard Treasury, YC S13. Pre-product,
  pre-revenue, banking-API thesis. The 2013 form predates the current
  "Are people using your product? How many?" question and lacks the
  current 50-character description. Some founder-detail fields have been
  redacted by the author (phone numbers, video URLs, incorporation
  details). Note the candor of the answers — useful eval signal because
  the rubric weights specificity and named users heavily.
---

# YC Application — Bedrock / Standard Treasury (S13)

## Company

**Company name:**
bedrock (we're working on it)

**Company URL:**
(none provided)

**YC usernames of all founders:**
zt dkimerling

**YC usernames of all founders who will live in the Bay Area June through August if we fund you:**
zt dkimerling

**What is your company going to make?**
We are building APIs for commercial banking services by building on top of multiple large banks. If someone needs advice they can call Goldman. If they just need to transact then they can use one of our APIs. We will build commercial banking middleware that will sit on top of banks just like Twilio sits on top of multiple phone carriers.

(1) Delivered programmatically using good APIs. (2) Narrow to start (probably ACH), ultimately broad services including ACH, F/X, wires, factoring, short-term loans. (3) Multiple banking partners, with verbal agreement from Wells Fargo and progress with JPMorgan and Capital One.

## Founders

**Founder details (zt):**
Zachary Townsend, 27, 2009, Brown, AB Applied Math & Economics. Currently at Stripe, mostly on Risk.
ztownsend@gmail.com / zactownsend.com / facebook.com/zactownsend / @ztownsend

**Founder details (dkimerling):**
Daniel Kimerling, 27, 2008, UChicago, AB Political Science, AM International Relations (and half-way through UChicago Booth MBA). Currently COO at giftly.com.
facebook.com/dkimerling / @dkimerling

**Most impressive thing other than this startup that each founder has built or achieved:**
ZT reorganized child welfare investigations in New York City. He got tons and tons of data, wrote R code to analyze it, set up ethnographic research conducted by his team, etc. He sniffed out details, wrote a report, and then helped implement the changes to a staff of 2000, and a budget in the tens of millions.

Dan built Giftly, particularly the proprietary stored value product, from a regulatory, legal, risk, etc., perspective.

**Time you (zt) most successfully hacked some (non-computer) system to your advantage:**
When I started in Newark, I didn't have a computer or an email, and City Hall didn't have wireless. So I tracked down one of the wireless networks I could find — owned by a bails bondsman close to the court — and negotiated with them for their wireless password.

I once spent hours looking at floorplans and historic housing lottery data so that my roommate and I could pick a HUGE double with our own bathroom despite having a terrible pick at Brown.

**Interesting project two or more of you created together:**
deciens.com — We raised the money, we have made investments. We have been to YC demo days and invested in Keychain Logistics.

**How long have the founders known one another and how did you meet?**
We've known each other since we were 16, when we met at Harvard summer school. All founders have met in person.

## Idea

**Why did you pick this idea to work on? Do you have domain expertise in this area?**
We started by thinking about ACH, which is a problem that Dan actually had in his work. Zac sees how hard it is for even Stripe to deal with Wells Fargo on F/X, wires, etc.

Dan knows a ton about payments. Zac won finance prizes @ Brown. We both want to disrupt banking and have been talking about it for years.

**What's new about what you're making? What substitutes do people resort to?**
When most businesses want to do something financial they have to call their bank and talk to a person — except for getting a MID. That doesn't make sense. Getting a wire, as an example, often involves twenty minutes, a painful conversation, and $30. Even non-quant hedge funds needing to convert EURO to GBP have to pick up the phone and talk to a bank's trading desk.

No one has built developer-friendly bank back-end processing, so you have to deal with banks, which overcharge, are slow, and are not developer friendly.

**Who are your competitors, and who might become competitors? Who do you fear most?**
Possible competitors: Square, Stripe, Braintree, Wells Fargo, JP Morgan, Bloomberg, Intuit, PayPal.

Banks cannot innovate on technology. A senior exec at JPMC told us that even if building good APIs was a Jamie Dimon priority it couldn't get done before 2017.

Commercial banking broadly — including every service we're imagining other than ACH (F/X, Wires, Factoring, Lending, Account Creation/Deletion, etc) — is not something that the innovative payments companies plan to provide to others, although they're all services they themselves need.

So, who do I fear most? I fear regulators the most. Banks can't beat us on technology but we might be so successful they beat us with the law.

**What do you understand about your business that other companies in it just don't get?**
People who run banks don't care about providing high-quality technology services, and the people who care about technology don't want to work with (or buy) a bank. Schlep blindness, as it were.

Also, there is great power in abstracting away thinking about your particular bank. Take ACH: since we are willing to suffer through forming eight banking relationships, we can provide next-day payouts to 80% of checking accounts in the US. Everyone else can only do next-day payouts on their one bank.

**How do or will you make money? How much could you make?**
We make money on transactions.

For a (very, very) rough guide, profits at ten biggest banks last year were $120b. Let's call 50% of that transactional/FICC/pure commercial banking as we define it.

- Total addressable market: O(100s of billions)
- Serviceable available market through APIs: O(10s of billions)
- Share of market: O(10s of billions)

## Progress

**If you've already started working on it, how long have you been working?**
Pre-development. We've incorporated. I'm still at Stripe. Dan's still at Giftly. It didn't make sense to start until one of the banks signalled a willingness to sign a commercial agreement as there was nothing to integrate with. Ready to start now. Raising money because of non-trivial commercial and regulatory costs. Far along with recruiting the rest of the early team and considering raising a seed round.

**How far along are you? Do you have a beta yet?**
We're far along on regulatory/commercial contract/legal stuff. Once we have that settled, there is a lot of backend, unsexy stuff to do to make it as pretty/smooth as we'd like: settlement files over SFTP, testing required by the banking partner, automatic underwriting built on Microbilt/LexusNexus/Iovation, etc, and then launch.

**If you have an online demo, what's the url?**
No online demo yet. It might be awhile before we have a dashboard and mocking up a fake API for you doesn't seem worth it.

**How will you get users?**
Working the network, undercutting others on price and (especially) ease, directly reaching out to every startup that needs banking services beyond payments that exists or is founded for traction.

We've focused our user research on three customer segments: (a) Corporate treasury departments (a heretofore undisrupted part of most enterprises) (b) hedge, private equity, and venture funds (minus quants/HF) and their back offices (c) technically inclined SMEs and startups who aren't served well by big banks.

## Other

**If you're already incorporated, when were you? Who are the shareholders?**
(Redacted by the author when he published the application.)

**If we fund you, which of the founders will commit to working exclusively on this project for the next year?**
zt dkimerling — we've envisioning this being a, uh, five-ten year project at least.

**For founders who can't commit exclusively, why not?**
—

**Do any founders have other commitments between June and August 2014 inclusive?**
No.

**Do any founders have commitments in the future?**
No.

**Where do you live now, and where would the company be based after YC?**
SF. SF.

**Are any of the founders covered by noncompetes or intellectual property agreements?**
We both have CIIAA's that could cover this work. Dan's company is pretty far away. Zac declared this idea when he signed his at Stripe. He's asked Stripe for an IP waiver letter, or whatever it's called.

I also described this entire idea in a youtube video I sent to you in December before we didn't accept a late interview, so… there is a lot of documentary evidence that I had this IP before Stripe.

**Was any of your code written by someone who is not one of your founders?**
No.

**If you had any other ideas you considered applying with, please list them:**
(Left blank.)

**Please tell us something surprising or amusing that one of you has discovered:**
"The failure, if it was one, lay in the fact that, having too much to hold on to, they slowly lost what they had. On the whole, it was those who had least who were able to move most freely to the new world which was coming into existence." — That reading *The Making of the Middle Ages* can make you think of everything from startups to the state of America in the world (this happened in December).
