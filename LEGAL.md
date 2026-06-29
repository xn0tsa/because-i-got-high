# Legal Correspondence

On June 24, 2026, I received a demand letter from Reid Attorneys Inc. (Cape Town / Johannesburg) acting on behalf of Cannabis Club Systems. The full letter is included in this repository as `lawyer_stuff.pdf`.

Publishing demand letters is standard practice in security research. You can read why at the [EFF](https://www.eff.org/issues/coders/researcher-faq). The short version: transparency is the correct response to legal pressure on factual reporting.

---

## The Demands and My Responses

### A. The "94% Medicinal" figure

**Their demand:** Correct the 94% figure to ~12%, remove all references to "medical records."

**Partially accepted.** The 94% figure reflected what the API returned, not what was stored in the database. CCS Nube identified a PHP bug (`isset() == 1` always evaluates to true) that caused the API to return "Medicinal" for nearly all records regardless of stored value. The README has been updated to reflect this accurately.

**Not accepted:** the demand to remove the GDPR Article 9 framing. Under *CJEU C-21/23 (Lindenapotheke, 2024)*, the Article 9 prohibition applies to what was transmitted at the API layer, not only what was stored. A bug does not create a legal exemption. The lawyers are welcome to take that up with the Court of Justice of the European Union.

As for *"the system does not store diagnoses, treatment records, prescriptions, or clinical histories"* — correct. Neither does a pharmacy loyalty card, which the CJEU also found to constitute health data in *C-21/23*. The bar is not "clinical record." It is "data that reveals information about health status." A field called `usageType` returning "Medicinal" in the context of a cannabis platform crosses that bar whether or not it was accurate.

---

### B. The Consumption Data

**Their demand:** Clarify that consumption fields are administrative estimates, not verified consumption logs.

**Accepted.** The README has been updated. "30g" entered at registration is a self-declared estimate, not a tracked record. Still personal data. Still exposed without authentication. Just not a surveillance log.

---

### C. Club Names in the Infographic

**Their demand:** Remove or anonymise all club names from the infographic and report.

**Declined.**

The clubs' members have a right to know which specific club their data came from. "A large Barcelona club" does not help someone determine whether to file a GDPR complaint with their national DPA. "The Bulldog" does.

The argument that "the clubs did not create or manage the affected infrastructure" is precisely why their names should remain — their members were harmed by a vendor choice the clubs made. That is not a reason for anonymity. It is an argument for accountability.

Additionally, GDPR Article 34(3)(c) mandates substitute public communication when individual notification is disproportionate. This report is that communication. Suppressing the club names would undermine the legal purpose it serves.

The letter notes that *"other publications which initially included this information have since removed it upon request."* Good for them.

---

### D. The Underage Member Records

**Their demand:** Remove the conclusion that 721 records under 18 "suggests either fraudulent registrations or a verification failure."

**Declined.**

The report said "suggests *either* fraudulent registrations *or* a verification failure." That is a hedged observation with two possible explanations, not a legal finding. CCS Nube has since provided three alternative explanations: data duplication, legacy migration artefacts, and age validation controls that they claim exist. These are plausible. They are also unverified from the outside.

The record exists. The age field says under 18. The report said what it could reasonably say from external observation. If the explanation is "legacy migration from a third-party system," that is worth knowing — it means CCS Nube imported unvalidated minor records into a system they then failed to secure. That is not an exculpatory fact.

---

### E. The Legal Threat

**Their threat:** High Court of South Africa proceedings if demands not met by June 30, 2026.

A South African law firm threatening a French/Spanish researcher over a GitHub report about an Irish company is an interesting jurisdictional exercise. The SA Constitutional Court formally recognized the SLAPP doctrine in *Mineral Sands Resources v Reddell* [2022] ZACC 37. Litigation whose purpose is to silence accurate reporting rather than vindicate a genuine right qualifies.

The ICO is investigating. Five data protection authorities have open files. The Irish DPC has confirmed contact with CCS Nube. The correct venue for any dispute about the accuracy of this report is not the High Court of South Africa. It is the facts.

The demands that were factually justified have been corrected above, voluntarily, without legal compulsion — because accuracy matters more than winning an argument. The demands that were not factually justified have been declined — for the same reason.

---

*All original findings and supporting documentation remain available. The lawyer_stuff.pdf is reproduced here in full in the public interest and in accordance with standard security research disclosure practice.*
