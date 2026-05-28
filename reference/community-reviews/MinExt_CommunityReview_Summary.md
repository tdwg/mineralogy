# MinExt Draft Terms Review — Summary

## Community Review vs. Public Review

The reviews documented here represent a **community review**, which is distinct from the formal TDWG public review process. The community review was conducted specifically to support the ongoing effort to bring new voices from the earth sciences collections community into TDWG, and to gather targeted expert feedback from earth science collection specialists who might otherwise be difficult to engage through standard TDWG channels. Participants were individually solicited based on their domain expertise and institutional reach — they were not self-selected respondents to a public call.

The formal TDWG public review, by contrast, is an open process conducted through official TDWG infrastructure and is open to any member of the broader community.

Because of this expertise gap, the bar for term ratification was deliberately set higher than it would be for a typical TDWG standard. While the TDWG community includes an abundance of highly knowledgeable paleontological and biological collection experts, it currently lacks consistent depth across many earth sciences subdomains — notably astromaterials and metamorphic petrology, among others. Without a sufficient baseline of domain expertise distributed across the broader voting community, a standard open ratification process risks approving or rejecting terms on grounds that do not reflect the realities of those disciplines. The targeted community review was designed to compensate for this gap by ensuring that expert judgment was gathered directly and deliberately before terms advance.

---

## How It Worked

The community review was coordinated by Rachel Walcott with logistical support from Ben Norton. Each solicited reviewer or group was sent a unique copy of the draft terms list — not a shared document. Reviewers were asked to fill out their individual copy and return it. A six-week reconvening window was planned for discussing feedback.

Outreach was channeled through three main routes: the MinExt Task Group itself, SMMP (Society for the Management of Mineral Pathways), and GCG/CETAF-ESG (Geological Curators Group / Consortium of European Taxonomic Facilities Earth Sciences Group). Rachel Walcott coordinated several of the community outreach invitations. Technical reviewers received an alternate, extended version of the terms list that included mappings to existing standards, in addition to the simplified version sent to the geosciences community.

Each reviewer rated every term across four dimensions: applicability (whether they currently capture this data), whether the definition is acceptable, a priority ranking (1–59), and free-text comments including suggestions for missing terms.

---

## Who Participated

### Community Reviewers (returned files)

| Initials | Name | Institution |
|----------|------|-------------|
| MR | Mike Rumsey | Head of Mineralogy, Natural History Museum, England, UK |
| JH | Jana Horak | Petrologist, Head of Geosciences, National Museums Wales, UK |
| VC | Veronica di Cecco | Collections Technician, Royal Ontario Museum, Canada |
| CE | Carrie A. Eaton | Museum Curator, Madison, WI, USA |
| RS | Roy Starkey | Independent mineral collector and researcher, Russell Society UK |
| MJ | Mary Johnson | USA (comments only, no full term-by-term review) |
| SJ | Stéphane Jouve, Robert Emmanuel, François Dusoulier, Jérôme Thomas, Pierre Sans-Jofre | Récolnat team, France |
| DM | Duncan Murdock | Curator, Oxford University Museum of Natural History, UK |
| YW | Yakov Weiss | Senior Lecturer, Hebrew University of Jerusalem, Israel |
| MA | Marie Angel | Curatorial Assistant, Geology, California Academy of Sciences, USA |

### Technical Reviewers

| Name | Institution | Status |
|------|-------------|--------|
| David Fichtmüller | Botanic Garden Berlin | Returned review |
| Gary Motz | Yale Peabody Museum | Uncommitted but providing examples |

### Pending / No Response

- Oskar Lindenmayer — Museums Victoria, Australia
- Mike Howe — British Geological Survey, UK
- Edward Zbik — Min Soc NSW, Australia
- Adam Mansur — Smithsonian Institution, USA
- Una Farrell — Trinity College Dublin, Ireland

**Total:** 10 community reviewers and at least 1 technical reviewer returned substantive feedback.

---

## Outcomes

### Term Priorities

The Summary Priorities sheet aggregated priority rankings across all reviewers. The most consistently high-priority terms (frequently ranked #1 or top-3) were:

- **Name** (Mineral Name class) — nearly universally ranked as the most critical term
- **Mineral Description** and **Specimen Description** — very high priority, though many institutions conflate the two in a single free-text field
- **Mineral ID** — essential for linking constituent parts to compound specimens
- **Associated Minerals** and **Predicated Name** — ranked highly
- **Crystal Habit** and **Crystal Form** — flagged as very important by Yakov Weiss and the Récolnat team

Terms with lower or more variable priority included **Twinning Law**, **Classification Code**, **Language**, **Verbatim Mass**, and **Maximum Axial Dimension**.

---

### Recurring Concerns

1. **Too many terms:** Multiple reviewers (YW, CE, MR) expressed that the list is too long and many fields would remain empty in practice. YW wrote that in his opinion the committee should try to shorten it substantially.

2. **Conflation of Specimen Description vs. Mineral Description:** Several institutions (CE, DM, MA) noted that these two concepts are currently merged into a single description field in their CMS, making the separation conceptually useful but practically difficult to migrate.

3. **Proportion, Role, and crystallographic terms likely to be unpopulated:** MR noted that Proportion is "fairly unrealistic" to populate accurately, and that Crystal Habit, Crystal Form, Aggregate Form, and Twinning Law would be hard to parse from legacy data migrations.

4. **Classification Codes questioned:** MR observed that alphanumeric classification schemes (Strunz, Dana) are falling out of favor in mineralogy and that no active body maintains them consistently.

5. **Name Type definition confusing:** Both MR and MA were unclear on what the term was capturing, and MR suggested it should be renamed or clarified (e.g., to reflect IMA approval status).

6. **Name Confirmation Status too binary:** MR requested a middle ground for "dubious" identifications that need checking — a simple true/false boolean doesn't cover real-world collection states.

7. **Associated Minerals definition error:** MR flagged that the word "secondary" has a specific technical meaning in mineralogy and needs to be removed or reworded.

8. **Name ID and Classification Code not currently in use:** CE and DM noted their institutions use picklists for mineral names rather than formal record identifiers, making Name ID inapplicable in its current form.

---

### Missing Terms Suggested

| Suggested By | Term / Category | Notes |
|---|---|---|
| MJ | Social history terms | Provenance, prior collection history, exhibition history, research history, links to publications (including popular books) |
| MR | Material science / crystallography | Stable isotopes, unit cell parameters, trace element chemistry |
| MR | Type specimen terms | Currently no terms covering type specimens |
| MR | Availability flag | Whether sample is available for study, loan, or exhibition |
| MR | Level of crystallinity | Degree of crystallinity of the specimen |
| SJ / Récolnat | Verbatim Name | Original textual description of the name (analogous to verbatimEventDate in Darwin Core) |
| SJ / Récolnat | Vernacular Name | A common or vernacular name |
| SJ / Récolnat | associatedNameConfirmationTechnique | List of identifiers for analyses associated with Name Confirmation Technique |
| SJ / Récolnat | Alteration Type, PreservationAlterationText, Pseudomorph | Terms used in ABCD-EFG, not currently covered |
| JH | Hey classification | Should be included in the Classification Code According To value domain |
| Multiple | Analytical report links | XRF data, Raman spectra, links to lab reports |

---

### General Disposition

Overall, reviewers broadly affirmed the direction and definitions — most terms received "Definition OK = Yes" — but the community feedback strongly signaled that **scope reduction**, **clarification of overlapping terms**, and **better accommodation of legacy data migration** are needed before the extension moves forward.

The technical review from Fichtmüller engaged the extended mappings version, while community reviewers largely reflected the practical realities of heterogeneous collection management systems across the UK, North America, Europe, Australia, and Israel.
