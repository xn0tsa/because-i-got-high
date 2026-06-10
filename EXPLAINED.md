# The whole story, explained to someone who doesn't know what an API is

*A cannabis club management platform left the passports of a million people in a unlocked filing cabinet on the street. Here's what happened.*

---

## First, what is a cannabis social club?

In Spain (and increasingly elsewhere), cannabis social clubs are legal membership organisations. You can't just walk in. You have to be invited by a member, fill in a registration form with your full name, home address, phone number, email, date of birth, and nationality — and crucially — **hand over your passport or ID card to be photographed**. The club files it all away. The law requires it. The whole model works because membership is documented, controlled, and verified. It's the thing that makes it defensible in court.

One company — **CCS Nube / Cannabis Club Systems** — built the software that hundreds of these clubs use to manage all of that. The database of members. The identity verification. The check-in system. The messaging between members. The payments. All of it ran through their platform, `ccsnubev2.com`. 377 clubs across Spain, South Africa, the UK, Ireland and elsewhere.

I joined one of those clubs in Barcelona. They gave me a membership card and mentioned, almost as an afterthought, that there was an optional app I could download — PuffPal.

I downloaded it. Then I took it apart.

---

## What does "taking apart an app" mean?

When you install an app on your phone, it's a file. And that file — if you know what you're doing — can be unzipped and read like a book. The code is all there. The instructions the app uses to talk to the servers. And sometimes, embarrassingly, the passwords too.

That's where the first problem was.

Inside the app code, on line 4 of a file called `Utils.java`, was this:

```
SECRET_KEY = "[REDACTED]"
```

That's a **Stripe secret key**. Stripe is the company that processes payments — the same one behind millions of online shops. A *secret* key is exactly what it sounds like: it's the master password to the payment account. With it you can see every transaction, every customer, every card on file. You can move money around.

It was sitting there, in plain text, inside a free app anyone could download.

That took twenty minutes.

---

## The main problem: the unlocked filing cabinet

But the Stripe key wasn't the big story. The big story was what I found next.

When an app talks to a server, it sends requests. Like asking a question: *"Hey server, can you show me the profile for member number 1234 of The Bulldog club?"* The server checks whether you have permission, and if yes, sends back the answer.

The key word there is **checks whether you have permission**.

CCS Nube's server didn't do that check.

I sent a request for member number 1234. It came back with a full name, home address, phone number, email, date of birth, nationality, monthly cannabis consumption, and strain preferences. No login. No password. No secret code. Just: the request, and the answer.

Then I tried member number 1235. Same thing.

1236. Same thing.

I wrote a small script to do this automatically, one member at a time, for every club, counting up from 1. I left it running overnight.

By morning I had **1,082,680 records**.

---

## What was in those records?

Everything the clubs collected during registration:

- Full legal name
- Home address
- Phone number
- Email address
- Date of birth
- Nationality
- Passport or national ID number
- Monthly cannabis consumption amount (e.g. "30g")
- Product preferences (strain names and quantities)
- QR code for physical check-in

And every single one of those 1,082,680 people had a field in their record that said:

```
usage_type: Medicinal
```

That last field matters legally. Under European data protection law (GDPR), **health data** gets special treatment — the highest level of protection, the biggest fines when it goes wrong. By classifying everyone as a medicinal user, the platform had turned a database of cannabis club members into a database of **medical records**. And then left the door open.

---

## The passport photos

It gets worse.

When you join a club, they photograph your passport or ID card. That photograph is stored on the server. It contains your face, your legal name, your date of birth, your document number, and your country.

Those photos were stored at a web address that looked like this:

```
https://ccsnubev2.com/v8/images/_[club]/ID/[number]-front.jpg
```

The club name came from the same place I was already getting everything else. The number was the same sequential member ID. No login. No password. No token. Just a web address you could type into any browser.

**985,841 identity document scans.** Passports. National ID cards. Driving licences. Publicly accessible on the internet, to anyone who knew the pattern.

---

## Why this is worse than most data breaches

Most data breaches expose email addresses and passwords. Annoying, fixable — you reset your password and move on.

This one exposed:

1. **Your legal identity**, proven to a government standard (because the club already verified it)
2. **Your face**, in a high-resolution scan of a government document
3. **A medical classification** connecting your real identity to cannabis use
4. **Your home address**

You can't change your passport number. You can't change your face. And you can't un-associate your name from a medical cannabis classification once it's been leaked.

---

## The geography problem

The clubs are mostly in Spain, but the *members* are from everywhere.

**130,623 Italian nationals** are in this database. **104,865 French nationals. 89,389 South Africans. 50,113 British nationals. 38,297 Germans.**

Many of these people joined clubs that are physically located outside Spain — there are large clubs in Cape Town, Johannesburg, London, and elsewhere, all running on the same platform.

Now think about what the leak means for different people:

For a Spanish person who joined a Barcelona club: embarrassing, potentially.

For a **British person**: cannabis remains a Class B drug in the UK. Personal possession carries up to 5 years' imprisonment. Their name, address, passport scan, and a record saying they're a medicinal cannabis user just became accessible to anyone.

For a **Saudi, Kuwaiti, or Emirati national**: cannabis possession can mean prison, flogging, or — for trafficking — death. The database contained hundreds of people from these countries, complete with their passport photographs, classified as medicinal cannabis users. That file was sitting on a public web server. The question isn't whether it was accessible. It was. The question is who accessed it before it was fixed.

And then there are the **721 minors** in the database. Cannabis clubs are legally required to restrict membership to adults. Those 721 records represent either a registration failure or fraud — either way, minors' identity documents and health classifications were in the same unlocked filing cabinet.

---

## What happened when I told them

I sent my first email to CCS Nube on **April 22, 2026**.

I was polite. I just asked: do you have a security disclosure process? Where should I send a vulnerability report?

Nothing.

I sent a follow-up three days later saying it was critical.

Nothing.

I forwarded to three named individuals at the company on April 26, the day after I'd confirmed the full scale of the breach.

Nothing.

On April 30, I sent a final warning: I would contact the data protection authorities if they didn't respond.

Nothing.

**Twenty-six days of silence.**

Eventually I called Sean Hollister, a journalist at The Verge — a major US tech publication. Sean had covered two of my previous security investigations. He sent an email to CCS Nube on May 13.

Nothing for five days.

On May 18, Sean followed up and said we were preparing to publish. CCS Nube replied within hours. Not to me. **To Sean.** Asking Sean — the journalist — to explain the technical details of the vulnerability.

I attached the full 30-page technical report to the thread that evening.

Three days later, the company said they hadn't received it.

Sean re-attached it.

---

## The "third-party agency" move

On May 22, the company finally confirmed they'd read the report. Their response included this sentence:

*"Several of the reported findings relate to legacy API architecture and mobile application configurations developed by a third-party agency."*

This is a classic move. The vulnerabilities were the fault of someone else they'd hired. Under European data protection law, this is legally irrelevant — if you hire someone to handle your data, you are still responsible for how they handle it. But it's a useful way to buy time and diffuse responsibility.

They listed some fixes they were working on. They said they were "determining notification obligations." This was May 22 — **27 days after the legal deadline to notify the authorities had already passed**.

When I asked about a bounty or credit for finding everything:

*"We do not currently operate a formal bug bounty programme, but we are discussing internally how best to handle responsible disclosures going forward."*

No payment. No credit.

---

## Where things stand now

**The Italian data protection authority** (Garante) confirmed in writing to The Verge on June 5 that they had no notification on record from CCS Nube. This confirmed what was already clear: the company had not notified any authority anywhere, weeks after the legal deadline.

**The UK Information Commissioner's Office** (ICO) confirmed on June 9 that my complaint had been received and routed to their investigations team.

Formal complaints have been filed with the data protection authorities in Italy, Spain, France, the United Kingdom, Germany, and South Africa.

The penalty for the kind of health data breach described in this report can reach **€20 million or 4% of the company's annual global revenue** — whichever is higher.

**The Verge is publishing a story** on this breach. It will be the third major security story they've published involving my research.

---

## If you're a member of one of these clubs

You don't need to have downloaded any app. The breach affects everyone who joined a club running on CCS Nube's platform.

**Contact your club in writing** and ask:
1. Has this vulnerability been fixed?
2. Has my data been involved in a breach?
3. I am requesting deletion of my identity document scan under GDPR Article 17.

**File a complaint with your national data protection authority** — they now have active investigations open. The links are in the main report.

Your club is also responsible. They chose the software. They handed your passport to a system that didn't protect it. Under GDPR, they are the "data controller" — the one legally accountable for making sure your data was safe. It wasn't.

---

## The one-sentence version

*A company that stores a million people's passports, home addresses, and medical records for cannabis clubs left the entire database accessible to anyone on the internet with no password, for what appears to be years, ignored the researcher who found it for 26 days, and still hasn't told any of those million people.*
