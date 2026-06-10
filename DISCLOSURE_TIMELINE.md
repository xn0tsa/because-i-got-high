# Disclosure Timeline — CCS Nube / Nefolutions

This is the chronology of contact between me (Sammy Azdoufal, independent security researcher) and CCS Nube / Cannabis Club Systems regarding the vulnerabilities published in the [README](README.md).

Every line attributed to the vendor below is quoted **verbatim** from the email thread. No employee names beyond what they signed. Timestamps are CET/CEST.

---

## Part 1 — Twenty-Six Days of Silence (April 22 → May 18)

The audit started on **April 26, 2026**. Within two hours I had confirmed an unauthenticated IDOR returning full member PII. Within twelve hours I had 1,082,680 records and 985,841 accessible ID document paths. The data was severe enough that I sent a disclosure before I had finished writing the report.

But the responsible disclosure process didn't start on April 26. It started four days earlier.

On **April 22, 2026** I sent the following email to `info@cannabisclub.systems`:

> *Hey,*
> *I am a security researcher and I have discovered critical vulnerabilities in your system.*
> *I would like to report these findings responsibly. Could you please let me know:*
> *- Does your company operate a bug bounty or vulnerability reward program?*
> *- If yes, what is the compensation policy for critical-level findings?*
> *- What is the preferred secure channel for submitting vulnerability reports?*
> *Thank you for your time.*

Standard disclosure etiquette. No alarm, no technical details, no leverage. A polite knock on the door asking where to send a report.

No response.

On **April 25** I followed up:

> *Please answer to me this is super critical*

Still nothing.

On **April 26** — the day after my overnight enumeration run confirmed the full scope of the breach — I forwarded to three addresses that I'd identified as belonging to people actually running the platform:

- `ahab@cannabisclub.systems`
- `berrern@gmail.com`
- `andreas@nefolutions.com`

No response from any of them.

The GDPR Article 33 clock started ticking the moment a data controller becomes aware of a personal data breach. I had now made three contacts explicitly flagging critical vulnerabilities to the company's general inbox and to individuals by name. Whatever argument they might later make about not having received the technical report, the notification of a serious problem landed on April 22. The 72-hour window to notify the supervisory authority closed on **April 25, 2026** — three days before they would acknowledge that anything existed at all, and twenty-three days before they would respond to anyone.

On **April 30** I sent what I intended to be the final notice before regulatory escalation:

> *Since you have failed to act in good faith, I am now proceeding to contact all relevant regulatory authorities.*
> *I will be filing formal complaints with the CNIL, the ICO (UK), and all applicable data protection authorities under the GDPR and other relevant frameworks. You were given the opportunity to resolve this matter fairly... you chose not to.*
> *The financial and reputational consequences of these complaints, including significant fines, will be entirely of your own making. This is your final notice.*

No response.

---

## Part 2 — Enter The Verge (May 13 → May 18)

Twenty-six days after my first email, I still had not received a single reply from CCS Nube. The GDPR notification window had expired. 985,841 passport scans were still sitting on a public URL. 1,082,680 health records were still returnable via unauthenticated HTTP GET.

I had learned from the DJI and Meari disclosures that media leverage is not a last resort — it is a tool. Vendors who ignore researchers reply to journalists. The dynamic is different when the question comes with a publication date attached.

I contacted Sean Hollister, Senior Editor at The Verge. Sean had covered both of my previous major disclosures: the DJI Romo MQTT vulnerability and the Meari/CloudEdge baby monitor breach. He understood the context. He sent the following email to `info@cannabisclub.systems` on **May 13**:

> *Hi CCS!*
> *I'm a reporter with The Verge. We're working with Sammy Azdoufal, a security researcher. We understand that your system is so vulnerable right now that your system is leaking passports, drivers licenses, and more on the public internet.*
> *Are you aware of the issue? Can you please confirm that you are taking action, and describe which actions you are taking to secure your databases? Are you reporting a data breach to all your customers, to the EU, and to other governments? Can you provide us with a copy of your data breach notification?*
> *Thank you very much.*
> *Sammy recently worked with us on these two stories:*
> *https://www.theverge.com/tech/926487/meari-technology-hack-baby-monitor-security-camera*
> *https://www.theverge.com/tech/879088/dji-romo-hack-vulnerability-remote-control-camera-access-mqtt*

No response for five days.

On **May 18**, Sean followed up:

> *Hi CCS! Can you please take action on this before we publish a story? It would be much better for everyone if the passports and other photo IDs are removed from the public internet.*

Twenty-six days after my first email, twenty-two days after the GDPR notification window closed, five days after The Verge's first contact: CCS Nube replied. Not to me. To Sean.

> *Hi Sean,*
> *Thank you for reaching out and bringing this to our attention.*
> *We are currently investigating the claims as a matter of urgency, and reviewing our systems and storage configurations. Protecting user data is extremely important to us.*
> *We would appreciate any additional technical details or indicators you can share that may help us identify and remediate the issue as quickly as possible.*
> *We will continue to assess the situation internally and take appropriate action based on our findings.*

Notice the last sentence of the second paragraph: they are asking Sean — a journalist — for technical details. The company that had not responded to a security researcher for twenty-six days was now asking the reporter to explain the vulnerability to them.

Sean forwarded the thread to me and connected us:

> *Hi! I'm putting you in touch with Sammy who discovered the vulnerabilities. He's CCd and can explain more.*
> *After you've discussed (with or without me on the thread, your preference), please let us know how you plan to proceed, including with notifications to your customers, their clients, and the authorities.*

On **May 18 at 21:38** I replied on the thread, with the full technical report attached:

> *Hey, you finally answer... Involving press was the ultimate option as you keep ignoring my mails.*
> *You will find the full report attached to this email.*

---

## Part 3 — The Missing Report (May 21)

Three days passed. On **May 21** the following arrived from `andreas@cannabisclub.systems`:

> *Hi Sean and Sammy,*
> *I haven't heard back from either of you yet, and wanted to follow up.*
> *We have been actively reviewing our systems and storage configurations internally since receiving your emails. However, in order to properly validate and remediate the alleged issue, we'd like to ask for specific technical details regarding the exposure you identified.*
> *Could you please provide:*
> *A sample affected URL, endpoint, or storage path*
> *The method by which the files were accessible*
> *Any example indicators that would help us identify the affected area*

Read this carefully. Andreas claimed to have been *"actively reviewing our systems and storage configurations internally since receiving your emails."* But in the same message he claimed not to have received the technical report I had attached three days earlier — the report that would have answered every one of his bullet points in exhaustive detail. He was asking me, again, to explain where the vulnerability was, three days after I had sent a 15-page technical document describing it.

Sean resent the attachment:

> *Hi Andreas,*
> *Did you not receive Sammy's email containing a document titled PUFFPAL_PENTEST_REPORT.md? I've attached it again here, thanks.*

I was more direct:

> *Andreas playing with time Sean, don't trust him.*

I meant it. A company that had ignored four emails over twenty-six days, then claimed to be urgently reviewing systems, then claimed not to have received the attached report — while simultaneously asking for the information the report contained — was not acting in good faith. The pattern is standard: run down the clock, create ambiguity, force the researcher to resend the same evidence repeatedly while the remediation window narrows.

---

## Part 4 — The Third-Party Agency Defence (May 22)

On **May 22**, Andreas wrote back. This time he confirmed receipt of the report:

> *Hi Sean and Sammy,*
> *Thank you for forwarding the report - I had not received this previously which is why I reached out.*
> *We have now reviewed the findings internally and have escalated the matter immediately with our engineering team and external development partners. We are actively investigating the reported issues, validating scope and impact, and prioritising remediation of the most critical items.*
> *Several of the reported findings relate to legacy API architecture and mobile application configurations developed by a third-party agency, and we are currently working through them on an urgent basis.*

*"A third-party agency."*

This is a common vendor response to a serious security finding. It is also legally irrelevant. Under GDPR Article 28, a data controller who engages a data processor — a third-party agency — remains fully responsible for ensuring that the processor provides sufficient guarantees about technical and organisational measures. The controller cannot outsource compliance. The club operators who deployed PuffPal trusted CCS Nube with their members' health data. CCS Nube trusted a third-party agency with the architecture. The passport scans were on the public server regardless of who wrote the code.

Sean applied direct pressure:

> *Thank you Andreas.*
> *I think it will be mandatory, in many countries, for you to notify not only the authorities but also every affected user.*
> *I understand you may not have the whole plan right away, but please let us know when and how you intend to do so, and please share a copy of the communication you will send out to end users about the data breach at that time.*
> *How long do you expect to need to remove passport images from the public web and inform your customers?*

---

## Part 5 — Remediation Confirmed, Questions Avoided (May 26)

On **May 26**, four days after confirming receipt of the report:

> *Hi Sean,*
> *Thank you for your email.*
> *Since receiving the report, we have been working continuously with both our internal engineering team and the external mobile application agency responsible for parts of the PuffPal infrastructure.*
> *Several remediation measures have already been implemented or are currently in deployment, including:*
> *updates addressing the unauthenticated profile access issue*
> *removal/restriction of direct public access to sensitive identity image paths*
> *credential and authentication hardening measures*
> *and ongoing updates to the chat and related API modules*
> *Updated mobile application builds containing security fixes have already been submitted to both Apple and Google for review and release.*
> *At the same time, we are conducting a broader internal assessment to validate scope, review logs, and determine any notification obligations under applicable regulations. Given the nature of the findings and the number of jurisdictions potentially involved, we want to ensure any communication to customers or end users is accurate, responsible, and legally compliant.*
> *Our immediate priority has been containment and remediation of the reported issues, and we have been treating this matter with the highest urgency since receiving the technical details.*

"Since receiving the technical details" — the technical details they received on May 18, when Sean's email arrived. Not April 22, when I first wrote. Not April 26, when I named three individuals and flagged a critical vulnerability. Not April 30, when I warned about regulatory escalation.

The phrase *"determine any notification obligations"* is notable. Thirty days after the GDPR Article 33 72-hour window had closed, the vendor was still *"determining"* whether they had notification obligations. They did. They have. 1,082,680 health records were exposed without authentication. The obligation existed from the moment of breach, not from the moment a security researcher managed to get a journalist to generate a response.

Sean's question about when affected users would be notified and what the notification would say — unanswered.

I added my own question on the same thread:

> *Also I get no credit/bounty from you regarding the vulnz?*
> *Good job, but why I have to involve media to get an answer? Why did you don't answer to my original email?*

---

## Part 6 — No Bounty Programme, No Explanation (May 27)

The final email in the thread, from Andreas, on **May 27**:

> *Hi Sammy,*
> *Thank you for your follow-up and for bringing these issues to our attention.*
> *To clarify, we genuinely did not receive the original technical report prior to Sean forwarding it to us, otherwise we would have escalated it internally much earlier. The initial emails we received from you did not contain any technical details or personal information (not even a name), so unfortunately they were not recognised as a legitimate security disclosure at the time.*
> *That said, we do appreciate the work that went into identifying and documenting the issues, and we acknowledge the seriousness of the findings. Since receiving the report, we have been working continuously on remediation together with our internal team and external development partners.*
> *Regarding recognition/bounty, we do not currently operate a formal bug bounty programme, but we are discussing internally how best to handle responsible disclosures going forward once the immediate remediation work is stabilised.*
> *Best regards,*

The framing here is worth taking apart.

*"The initial emails we received from you did not contain any technical details or personal information (not even a name)."*

My April 22 email did not include my name or technical details. That is correct. It was an inquiry about their disclosure process — the standard first step in responsible disclosure practice. You ask where to send a report before you send it. That inquiry was ignored for four days before I sent a second message saying the matter was critical. That was ignored. I then contacted three named individuals directly. That was ignored for four more weeks. The fact that my initial inquiry didn't include my full name is not an explanation for why four separate emails over twenty-six days received zero response.

*"we are discussing internally how best to handle responsible disclosures going forward"*

985,841 passport scans on a public URL. 1,082,680 health records without authentication. No bounty program. No disclosure policy. No documentation of a security contact anywhere on their website. And the response to a researcher who identified and reported all of it is that they are *"discussing internally"* how to handle this kind of thing in the future.

Regarding credit: none given. Regarding payment: none offered.

---

## Part 7 — What Did Not Happen

A clean record, for clarity:

- **No GDPR Article 33 notification** was confirmed by any supervisory authority before the date of this report. The 72-hour window closed on April 25, 2026 — the day I sent my second email.
- **No GDPR Article 34 direct notification** was sent to any affected member. 1,082,680 people whose health data and, for the majority, identity documents were exposed on a public server have not been told.
- **No bug bounty and no credit** were offered by the vendor, despite the report covering 14 vulnerabilities including 5 rated Critical.
- **No response to a security researcher for 26 days**, until a journalist from The Verge attached a publication date to the question.
- **"Third-party agency" is not a legal defence.** The data controller bears full responsibility for the processing it delegates to processors under GDPR Article 28. The source of the vulnerable code does not change who was responsible for protecting the data.
- **Remediation was confirmed on May 26 for the most critical items.** Independent verification of the fixes has not been performed. The ID document photo endpoint and the member profile IDOR are the highest priority. Whether the fix is complete, whether all 985,841 image paths have been invalidated, and whether any logs were preserved to determine prior unauthorized access — none of this has been independently confirmed.

---

## Part 8 — June 5: The Garante Confirms It (Update)

On **June 3**, Sean Hollister contacted the Italian Garante for comment on the story, stating that I had filed a regulatory notification. On **June 5**, the Garante replied:

> *"Based on the information you have provided, the Italian Data Protection Authority currently has no record of having received the notification you mentioned."*

This requires a correction. Formal DPA notifications had not yet been filed at the time of publication. The statements in the original report describing notifications as filed were premature. The legal obligation to notify under GDPR Article 33 rests with **CCS Nube as data controller** — their 72-hour window closed on April 25, 2026, six weeks before the Garante's response. What I am filing is an Art. 77 complaint as an affected data subject, which is the correct instrument for a researcher in this role.

The Garante's response confirms the separate point: **CCS Nube has not notified the Italian DPA.** That is an independently actionable violation of Article 33, regardless of what a researcher files. The same is true for every other DPA in jurisdictions where affected members reside.

Art. 77 complaints and investigative tips are being filed with Garante (Italy), AEPD (Spain), CNIL (France), ICO (UK), and BfDI (Germany) as of June 5, 2026.

---

## Part 9 — June 5 → June 9: The ICO Responds

On **June 5, 2026 at 16:10**, I filed the following complaint with the ICO Press Office at `PressOffice@ico.org.uk`:

> *Dear ICO Press Office,*
>
> *I am writing as an independent security researcher and affected data subject to formally bring to your attention a serious personal data breach affecting UK residents, committed by Cannabis Club Systems / Nefolutions, operator of the platform ccsnubev2.com.*
>
> *Scope of the breach:*
> *- 49,812 UK residents with full personal data (name, address, phone, email, date of birth, passport/driving licence number) exposed via an unauthenticated IDOR endpoint in production — no login, no token, no rate limit*
> *- 49,812 identity document photographs (passports, driving licences, national ID cards) publicly accessible via a predictable URL with no authentication*
> *- All affected individuals are classified in the database as usage_type: Medicinal — constituting health data under UK GDPR Article 9*
> *- Global scope: 1,082,680 members across 377 clubs in 40+ countries*
>
> *Article 33 failure:*
> *The data controller was first notified on April 22, 2026. The 72-hour notification window closed on April 25, 2026. As of today, no supervisory authority has confirmed receiving any notification from Cannabis Club Systems. The Verge (Vox Media) is currently preparing a story on this breach in collaboration with me.*

On **June 9, 2026**, Rashana Sweidan Vigerstaff, Senior Communications Officer at the ICO, replied:

> *Hi Sammy, many thanks for your email. Just wanting to confirm that this was passed through to the relevant team at the ICO, who have confirmed receipt, and a colleague from that team will be in touch.*

The ICO is the first supervisory authority to confirm that the complaint has been formally received **and** routed to an investigations team. This is significant: it means the ICO has assessed the complaint as actionable and assigned it internally. CCS Nube has not, to my knowledge, filed any notification with the ICO. The investigations team will be working from a complaint from the researcher, not from the data controller — which is itself a recordable fact about the company's Article 33 compliance.

---

*Back to [README](README.md).*
