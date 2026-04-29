---
company: Dropbox
batch: S07
outcome: accepted
source_url: https://www.ycombinator.com/apply/dropbox
form_version: 2007
verbatim: true
partial: true
notes: |
  Drew Houston applied as a sole founder. Quoted text comes from the
  application as published on YC's own site. Some answers as published
  appear truncated (the YC page presents the application as a structured
  form, not always full prose). The 2007 form was very different from
  today's: no "are people using your product" question, no "how many
  active users" question, no "are you incorporated" prompt phrased the
  same way, and several answer fields are short labels rather than
  paragraphs. Where an answer field had no equivalent in the 2007 form,
  it is omitted here rather than fabricated. Treat this as the historical
  record, not a draft against the 2026 form.
---

# YC Application — Dropbox (S07)

## Company

**Company name:**
Dropbox

**Company URL:**
http://www.getdropbox.com/

**Demo URL:**
http://www.getdropbox.com/screencast/ — Windows build at http://www.getdropbox.com/u/2/DropboxInstaller.exe

**What is your company going to make?**
Dropbox synchronizes files across your/your team's computers. It's much better than uploading or email, because it's automatic, integrated into Windows, and fits into the way you already work.

There are tons of interesting features — e.g. taking advantage of the fact we have a copy of everyone's data, like a web interface ("oh crap, I need that file I'm working on, and I'm not at my computer"), or making sharing a folder with someone else trivial (vs. setting up a fileserver/permissions/etc.). And we use Amazon S3 for storage so you have an offsite backup at no additional cost (encrypted with a key only you know).

I have a long laundry list of things people want for this — porting to OS X and Linux, integrating with Word/Excel sharing features, plug-ins for Photoshop/Aperture/etc., support for working with people who don't have the client (web uploading), syncing iTunes libraries...

## Founders

**YC usernames of founders:**
dhouston

**YC usernames of founders moving to Bay Area June–August 2007:**
dhouston

**Founder details:**
dhouston; Drew Houston; 24; 2006, MIT, SB computer science; Bit9, Inc — project lead/software engineer

**Most impressive thing each founder has built or achieved:**
Programming since age 5; startups since age 14; 1600 on SAT; started profitable online SAT prep company in college (Accolade, http://accoladeprep.com — see also press release at http://web.mit.edu/newsoffice/2004/sat-1208.html). For fun last summer reverse engineered the software protecting the country's largest poker site and wrote a real-money playing poker bot (it was about break-even, alas; never deployed it for moral reasons.)

**Joint project example:**
N/A (single founder; the Accolade Online SAT prep product launched in 2004 and a poker bot project are listed under prior work)

**How long have the founders known one another and how did you meet?**
There's a joke in here somewhere.

## Progress

**If you've already started working on it, how long have you been working and how many lines of code (if applicable) have you written?**
3 months part time. About ~5KLOC client and ~2KLOC server of python, C++, Cheetah templates, installer scripts, etc.

**How long will it take before you have a prototype? A beta? A version you can charge for?**
Prototype — done in Feb. Beta — in people's hands now. Version I can charge for: 6–8 weeks?

## Idea

**What's new about what you're making?**
Most small teams have a few basic needs: (1) team members need their important stuff in front of them wherever they are, (2) everyone needs to be working on the latest version of a given document (and ideally can have older versions at their fingertips), (3) and team data needs to be protected from disaster. There are sync tools (e.g. beinsync, FolderShare), there are backup tools (Carbonite, Mozy), there are storage tools (Amazon S3, Strongspace), there are server-based offerings (Xythos, sharepoint), and there's "Joe sets up a fileserver and we use VPN/rsync/scp." But there's no good integrated solution.

**Who are your competitors?**
Carbonite and Mozy do a good job with hassle-free backup, and a move into sync would make sense. Sharpcast has been working on a sync tool called Hummingbird for at least a year. (Their CEO is the founder of Mirra, which sold to Seagate.) FolderShare (a Microsoft acquisition) and beinsync provide hassle-free sync but no online backup component. Google's coming GDrive looms large, but I'm skeptical that it will be any good — Gmail, Reader, and Apps are excellent, but Google has consistently bungled its desktop software offerings (toolbar, desktop search, Picasa). Hopefully if anyone else, like Microsoft, eventually approaches this with similar ambitions, my product will be far enough along to be acquired or hold its own.

**What do you understand about your business that other companies in it just don't get?**
Competing products work at the wrong layer of abstraction and/or force the user to constantly think and do things (instead of having the human do what humans are good at — working on stuff — and having the computer do what computers are good at — moving data around.) Rather than provide an abstraction (like a network filesystem), they tend to be solutions glued onto existing filesystems (often using FTP or WebDAV, or they don't bother with integration at all). Backup is a separate app or service from sharing or accessing your own data remotely. The result is something a layperson can't figure out or doesn't trust.

**How will you make money?**
The current plan is a freemium approach, where we give away free 1GB accounts and charge for additional storage (maybe ~$5/mo or less for 10GB). For a rough comparison, Carbonite charges $5/mo for unlimited backup (but backup only). At ~$1/GB/year my margins on the storage are big, even after backing everything up to S3. Down the road I can use the lessons of running the freemium-based service to build an enterprise offering (the holy grail in this space — just look at how much Sharepoint makes Microsoft).

## Other

**Are you incorporated?**
Not incorporated — but ready to incorporate at the drop of a hat.

**Equity plan:**
Drew, presently sole owner but saving some stock (a couple percent?) for work done by Jeff & Tom (former Accolade co-workers helping me out occasionally) and a couple advisors.

**Are any of the founders covered by noncompetes?**
I consulted an attorney and have a signed letter indicating Bit9 has no stake/ownership of any kind in Dropbox.

**Was any of your code written by someone who is not one of your founders?**
No.

**If you had any other ideas you considered applying with, please list them:**
One click screen sharing — like a stripped down WebEx with none of the BS and adapted for things like "hey, look at this!" moments between friends, or for tech support, or for impromptu meetings. A wiki with version-controlled drawing canvases instead of pages. Some ideas surrounding better web analytics for newbies.

**Where do you live now, and where would the company be based after YC?**
Cambridge, MA / SF Bay Area.

**Please tell us something surprising or amusing that one of you has discovered.**
The ridiculous things people name their documents to do versioning, like "proposal v2 good revised NEW 11-15-06.doc", continue to crack me up.
