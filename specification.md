# Mineralogy Extension for Darwin Core
## Comprehensive Technical Documentation

**Version:** DRAFT  
**Date:** January 21, 2026  
**Document Type:** Technical Documentation  
**Prepared By:** Based on TDWG Mineralogy Extension Task Group Resources

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Introduction](#introduction)
3. [Background and Motivation](#background-and-motivation)
4. [Organizational Structure](#organizational-structure)
5. [Technical Architecture](#technical-architecture)
6. [Core Classes and Terms](#core-classes-and-terms)
7. [Data Model and Relationships](#data-model-and-relationships)
8. [Implementation Guidelines](#implementation-guidelines)
9. [Controlled Vocabularies](#controlled-vocabularies)
10. [Use Cases and Examples](#use-cases-and-examples)
11. [Appendices](#appendices)

---

## Executive Summary

The Mineralogy Extension (MinExt) is a specialized data standard developed by the Mineralogy Extension Task Group under the Biodiversity Information Standards (TDWG) Earth Sciences and Paleobiology (ESP) Interest Group. This extension addresses a critical gap in biodiversity informatics by extending the Darwin Core Archive standard to support mineralogical collections data.

### Key Features

- **Comprehensive mineral specimen documentation** at both specimen and constituent part levels
- **Support for compound specimen models** with multiple minerals in a single specimen
- **Integration with existing standards** including Darwin Core and Chronometric Age Extension
- **Specialized vocabularies** for mineralogical properties, chemical composition, and geological context
- **Classification system support** for both Dana and Nickel-Strunz systems
- **Type locality tracking** and locality-based information management

### Target Audience

- Museum curators and collections managers
- Geoscience data managers
- Database developers working with earth sciences collections
- Researchers requiring standardized mineralogical data
- Developers of collection management systems

---

## 1. Introduction

### 1.1 Purpose and Scope

The Mineralogy Extension provides a standardized lexicon for describing mineralogical specimens, enabling improved data sharing, discovery, and integration across institutions. The extension comprises:

- A normative term list with formal definitions
- Controlled vocabularies for mineralogical properties
- Support for complex specimen models (compound specimens)
- Integration with multiple classification systems
- Enhanced geological context descriptions

### 1.2 Document Status

This document describes the DRAFT version of the Mineralogy Extension. All content is subject to review and ratification by the TDWG community following the organization's standard development processes.

**Key Standards Referenced:**
- Darwin Core (DwC): http://rs.tdwg.org/dwc/terms/
- Darwin Core Chronometric Age Extension: http://rs.tdwg.org/chrono/terms/
- TDWG Standards Documentation Standard (SDS)

### 1.3 RFC 2119 Key Words

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

---

## 2. Background and Motivation

### 2.1 The Need for Mineralogy Extension

#### Knowledge Domain Gap

The TDWG community has historically focused on biological collections, with standards like Darwin Core reflecting this biological orientation. While earth sciences collections share some commonalities with biological specimens, mineralogical collections present unique challenges:

1. **Non-hierarchical classification**: Unlike biological taxonomy, minerals are classified using semi-hierarchical systems (Dana, Nickel-Strunz)
2. **Chemical composition focus**: Mineral identification relies heavily on chemical and crystallographic properties
3. **Compound specimens**: Single specimens may contain multiple mineral species
4. **Geological context complexity**: Collection locality information requires geological features not present in biological contexts

#### Strategic Importance

Extending TDWG's reach to mineralogy serves multiple strategic goals:

- **Community expansion** into earth sciences domains
- **Foundation for future extensions** to petrology, meteoritics, and other geosciences
- **Comprehensive collections coverage** across natural history museums
- **Enhanced interoperability** between biological and geological collections data

### 2.2 Historical Context

The Mineralogy Extension Task Group was established under the ESP Interest Group, following the successful models of:

- Darwin Core Chronometric Age Extension
- Extension for Geosciences (EFG)

These precedents established best practices for:
- Community engagement and consensus building
- Technical development using GitHub repositories
- Standards documentation following TDWG guidelines
- Crosswalk development between related standards

### 2.3 Design Principles

The extension adheres to the following principles:

1. **Darwin Core compatibility**: Build upon existing Darwin Core architecture
2. **Minimal redundancy**: Reuse existing terms where appropriate
3. **Semantic clarity**: Provide unambiguous definitions for all terms
4. **Practical utility**: Focus on specimen-level data commonly collected by institutions
5. **Extensibility**: Design to accommodate future expansion

---

## 3. Organizational Structure

### 3.1 Task Group Composition

#### Conveners

| Name | Affiliation | Role |
|------|-------------|------|
| Ben Norton | Independent, Raleigh, NC, USA | Data Scientist, Lead Convener |
| Dr. Rachel Walcott | National Museums, Scotland | Principal Curator (Earth Systems), Co-Convener |

#### Core Members

The task group comprises 9 core members representing diverse institutions:

- Natural History Museum Bern, Switzerland
- North Carolina Museum of Natural Sciences, USA
- Natural History Museum of Geneva, Switzerland
- Tallinn University of Technology, Estonia
- Smithsonian National Museum of Natural History, USA
- Natural History Museum Basel, Switzerland
- Mindat.org
- Independent geoinformatics specialists

This international representation ensures the extension addresses diverse institutional practices and regional variations in mineralogical collections management.

### 3.2 Governance and Process

#### Development Phases

**Phase 1: Community Building**
- Recruitment of mineralogical collections experts
- Engagement with underrepresented TDWG domains
- Establishment of task group structure and communication channels

**Phase 2: Standard Development**
- Survey of existing data standardization efforts
- Community deliberation on vocabulary terms
- Development of normative term list and documentation
- Crosswalk creation with related standards

**Phase 3: Review and Ratification**
- Submission to TDWG for community review
- Incorporation of feedback
- Final ratification following TDWG By-laws

#### Development Infrastructure

- **GitHub Repository**: https://github.com/tdwg/mineralogy
- **Documentation Site**: https://tdwg.github.io/mineralogy/
- **Issue Tracking**: GitHub Issues for term proposals and discussions
- **Version Control**: Git for tracking changes and maintaining history

---

## 4. Technical Architecture

### 4.1 Namespace and Prefixes

The Mineralogy Extension uses the following namespace structure:

**Primary Namespace:**
- URI: `http://rs.tdwg.org/mineralogy/terms/`
- Recommended Prefix: `minext:`
- Alternative Prefix: `geoext:` (used in current documentation)

**Borrowed Vocabularies:**

| Vocabulary | Prefix | Namespace URI |
|------------|--------|---------------|
| Darwin Core | dwc: | http://rs.tdwg.org/dwc/terms/ |
| Chronometric Age | chrono: | http://rs.tdwg.org/chrono/terms/ |
| Dublin Core Terms | dcterms: | http://purl.org/dc/terms/ |
| RDF Schema | rdfs: | http://www.w3.org/2000/01/rdf-schema# |
| RDF | rdf: | http://www.w3.org/1999/02/22-rdf-syntax-ns# |
| SKOS | skos: | http://www.w3.org/2004/02/skos/core# |

### 4.2 Extension Architecture

The Mineralogy Extension follows the Darwin Core star schema pattern:

```
MaterialEntity (Core)
    ↓
    ├─→ ConstituentPart (Extension)
    │       ├─→ Name (Multiple instances per ConstituentPart)
    │       ├─→ Chemistry
    │       └─→ MaterialAssertion (Mineral properties)
    │
    ├─→ GeologicContext
    ├─→ Location
    ├─→ ChronometricAge
    ├─→ Conservation
    └─→ Hazard
```

### 4.3 Material Categories

Terms in the extension are assigned to one of two material categories:

1. **Specimen**: Terms applicable to the entire physical specimen
2. **Constituent Part**: Terms applicable to individual minerals within a specimen

This distinction is critical for implementing the compound specimen model.

---

## 5. Core Classes and Terms

### 5.1 Class Definitions

#### ConstituentPart (geoext:ConstituentPart)

**Definition:** A physically discernable part of a compound specimen that has a distinct proportion and role relative to the parent object and a discrete determination based on physical and chemical characteristics.

**Purpose:** Enables documentation of individual minerals within specimens containing multiple mineral species.

**Key Properties:**
- constituentPartID: Unique identifier for the constituent part
- constituentPartType: General classification (Mineral, Fossil, Rock)
- constituentPartProportion: Quantitative or qualitative abundance
- constituentPartRole: Relationship to parent specimen (matrix, phenocryst, vein, etc.)
- materialEntityID: Links to parent specimen record

**Usage Context:** Essential for specimens with multiple minerals, such as:
- Quartz crystals on calcite matrix
- Pegmatites with multiple mineral species
- Ore specimens with multiple sulfides

#### Name (geoext:Name)

**Definition:** The designation of a mineral by a linguistic expression including both informal (verbatim) and formal (classification) types.

**Purpose:** Accommodates multiple naming conventions including:
- Formal classification names (e.g., "Quartz")
- Variety names (e.g., "Smoky Quartz")
- Synonyms and historical names
- Group names (e.g., "Garnet Group")

**Key Properties:**
- name: The actual mineral name
- nameIdentifier: Unique ID for this name instance
- nameType: Classification of name type (Classification, Variety, Synonym, etc.)
- classificationCode: Dana or Strunz code
- nameConfirmationTechnique: Analytical method used for identification
- catalogedName: Administrative name for specimen-level use

**Multiplicity:** One ConstituentPart may have multiple Name instances, enabling documentation of:
- Primary classification name
- Varietal names
- Historical synonyms
- Alternative classification systems

#### Chemistry (geoext:Chemistry)

**Definition:** Properties that describe the chemical composition of a geological material (mineral).

**Purpose:** Documents chemical analyses and formulas critical to mineral identification.

**Key Properties:**
- measuredChemistry: Chemical formula or composition
- measuredChemistrySource: Citation for composition data
- mineralogicalAnalysisProtocol: Analytical technique used
- chemistryRemarks: Additional notes on composition

**Example:**
```
measuredChemistry: "SiO2 (65.76), TiO2 (32.120), Al2O3 (2.21)"
mineralogicalAnalysisProtocol: "Electron probe microanalysis"
measuredChemistrySource: "Smith et al. 2020"
```

#### MaterialAssertion (dwc:MaterialAssertion)

**Definition:** Assertions about physical and morphological properties of specimens and constituent parts.

**Scope:** Contains the most extensive vocabulary for describing:

**Physical Dimensions:**
- measuredWidthInMillimeters
- measuredHeightInMillimeters
- measuredDepthInMillimeters
- measuredMassInGrams
- verbatimSize / verbatimMass

**Mineral Properties:**
- color: Intrinsic color under natural light
- luster: Surface reflectance quality
- crystalHabit: General morphology (tabular, fibrous, etc.)
- crystalForm: Geometric shape (cube, scalenohedron, etc.)
- aggregateForm: Crystal assemblage patterns (botryoidal, radial, etc.)
- cleavage: Breakage characteristics
- twinningLaw: Twin crystal descriptions
- inclusions: Foreign bodies within crystals
- exsolutionTexture: Phase separation features
- luminescence: Fluorescence and phosphorescence

**Contextual Properties:**
- associatedMinerals: Co-occurring species
- alterationDescription: Secondary modifications
- mineralDescription: Distinguishing features at mineral level
- specimenDescription: Distinguishing features at specimen level

#### GeologicContext (dwc:GeologicContext)

**Definition:** Geological information that qualifies a region or place.

**Purpose:** Provides geological framework for understanding specimen formation and occurrence.

**Key Properties:**
- geologicProvince: Broad physiographic/tectonic regions
- lithodemicUnit: Unstratified geological units
- geologicEvent: Formation or modification events
- mineralSequence: Temporal order of mineral formation
- tectonicUnits: Tectonic framework elements

**Example:**
```
geologicProvince: "Blue Ridge"
geologicEvent: "Alleghanian orogeny"
mineralSequence: "Calcite > Quartz > Sphalerite > Pyrite"
```

#### Location (dwc:Location)

**Definition:** A spatial region or named place (extends Darwin Core Location).

**Mineralogy-Specific Properties:**
- sampledFeature: Type of physical feature sampled (outcrop, mine pit, float)
- namedPlace: Named anthropogenic localities (mines, quarries)
- isTypeLocality: Boolean flag for type locality status

**Usage Notes:**
- namedPlace for anthropogenic features (mines, quarries)
- geologicProvince (in GeologicContext) for natural features
- isTypeLocality critical for mineral species type specimens

#### ChronometricAge (chrono:ChronometricAge)

**Definition:** Temporal position supported by evidence (from Chronometric Age Extension).

**Mineralogy Addition:**
- chronometricAgeGeologicProcess: Associated geological process (e.g., "Igneous Crystallization", "magmatic cooling")

**Integration:** Links mineral ages with geological processes, critical for understanding formation history.

#### Conservation (geoext:Conservation)

**Definition:** Processes, protocols, and techniques for protection and preservation.

**Key Properties:**
- treatments: Curatorial actions taken
- handlingRequirements: Safe handling procedures
- damageRemarks: Description of deterioration

**Examples:**
```
handlingRequirements: "Handle with gloves; avoid contact with water"
damageRemarks: "Pyrite oxidation causing specimen fragmentation"
treatments: "Stabilized with paraloid B-72"
```

#### Hazard (geoext:Hazard)

**Definition:** Sources of potential damage, harm, or adverse health effects.

**Key Properties:**
- hazardType: Classification of hazard (Carcinogen, radioactive, toxic)
- hazardRemarks: Specific context for the hazard

**Examples:**
```
hazardType: "Carcinogen"
hazardRemarks: "Contains asbestos fibers"
```

---

## 6. Data Model and Relationships

### 6.1 Compound Specimen Model

The extension implements a sophisticated compound specimen model:

```
Specimen (MaterialEntity)
    materialEntityID: "SPEC-001"
    catalogedName: "Quartz on Calcite"
    specimenDescription: "Exceptional clarity"
    ↓
    Constituent Part 1 (Mineral)
        constituentPartID: "CP-001"
        materialEntityID: "SPEC-001"
        constituentPartType: "Mineral"
        constituentPartRole: "matrix"
        constituentPartProportion: "70%"
        ↓
        Name 1
            nameIdentifier: "NAME-001"
            constituentPartID: "CP-001"
            name: "Calcite"
            nameType: "Classification"
            classificationCode: "05.AB.05"
        ↓
        Chemistry 1
            measuredChemistry: "CaCO3"
    ↓
    Constituent Part 2 (Mineral)
        constituentPartID: "CP-002"
        materialEntityID: "SPEC-001"
        constituentPartType: "Mineral"
        constituentPartRole: "phenocryst"
        constituentPartProportion: "30%"
        ↓
        Name 2
            nameIdentifier: "NAME-002"
            constituentPartID: "CP-002"
            name: "Quartz"
            nameType: "Classification"
            classificationCode: "04.DA.05"
        ↓
        Chemistry 2
            measuredChemistry: "SiO2"
```

### 6.2 Cardinality Rules

| Relationship | Cardinality | Notes |
|--------------|-------------|-------|
| MaterialEntity → ConstituentPart | 1:n | Specimens may have multiple minerals |
| ConstituentPart → Name | 1:n | Each mineral may have multiple names |
| ConstituentPart → Chemistry | 1:1 | One chemistry record per mineral |
| MaterialEntity → GeologicContext | 1:1 | Single geological context per specimen |
| MaterialEntity → Location | 1:1 | Single collection location per specimen |
| MaterialEntity → Conservation | 1:1 | Single conservation record per specimen |
| MaterialEntity → Hazard | 1:1 | Single hazard assessment per specimen |

### 6.3 Identifier Strategy

**Required Identifiers:**
- materialEntityID: Links specimens to constituent parts
- constituentPartID: Unique ID for each mineral instance
- nameIdentifier: Unique ID for each name instance

**Best Practices:**
- Use globally unique identifiers (UUIDs) when possible
- Maintain persistent identifiers across system migrations
- Document identifier assignment schemes in institutional policies

---

## 7. Implementation Guidelines

### 7.1 Minimum Metadata Requirements

For basic compliance, implementations MUST include:

**Specimen Level:**
- materialEntityID
- catalogNumber (from Darwin Core)
- institutionCode (from Darwin Core)

**Constituent Part Level:**
- constituentPartID
- materialEntityID (linking to parent)
- constituentPartType

**Name Level:**
- nameIdentifier
- constituentPartID (linking to parent)
- name

### 7.2 Recommended Best Practices

#### Use of Controlled Vocabularies

Many terms recommend controlled vocabularies:

**High Priority:**
- constituentPartType: Use consistent mineral/rock/fossil categories
- constituentPartRole: Use GeoSciML vocabulary (http://resource.geosciml.org/classifier/cgi/compoundmaterialconstituentpartrole)
- constituentPartProportion: Use CGI proportion terms (http://resource.geosciml.org/classifier/cgi/proportionterm)
- mineralogicalAnalysisProtocol: Use ARDC analytical methods (https://vocabs.ardc.edu.au/viewById/650)

#### Data Quality Considerations

1. **Consistency**: Apply terms consistently across collections
2. **Completeness**: Populate all available relevant terms
3. **Accuracy**: Verify technical terms against authoritative sources
4. **Documentation**: Maintain clear documentation of local practices

### 7.3 Integration with Existing Systems

#### Darwin Core Archive Structure

Hypothetical Standard Darwin Core Archive with extension:

```
Archive Root/
├── meta.xml
├── occurrence.txt (MaterialEntity core)
├── constituentpart.txt (ConstituentPart extension)
├── name.txt (Name extension)
├── chemistry.txt (Chemistry extension)
├── geologiccontext.txt (GeologicContext extension)
└── eml.xml (Metadata)
```

#### Example meta.xml snippet:

```xml
<extension encoding="UTF-8" 
           fieldsTerminatedBy="," 
           linesTerminatedBy="\n" 
           fieldsEnclosedBy='"' 
           ignoreHeaderLines="1" 
           rowType="http://rs.tdwg.org/mineralogy/terms/ConstituentPart">
    <files>
        <location>constituentpart.txt</location>
    </files>
    <coreid index="0"/>
    <field index="1" term="http://rs.tdwg.org/mineralogy/terms/constituentPartID"/>
    <field index="2" term="http://rs.tdwg.org/mineralogy/terms/materialEntityID"/>
    <field index="3" term="http://rs.tdwg.org/mineralogy/terms/constituentPartType"/>
    <!-- Additional fields... -->
</extension>
```

### 7.4 Database Implementation Patterns

#### Normalized Relational Model

```sql
-- Specimen table (Darwin Core MaterialEntity)
CREATE TABLE compoundSpecimen (
    materialEntityID VARCHAR(50) PRIMARY KEY,
    catalogNumber VARCHAR(50),
    institutionCode VARCHAR(20),
    specimenDescription TEXT
);

-- Constituent Part table
CREATE TABLE constituentPart (
    constituentPartID VARCHAR(50) PRIMARY KEY,
    materialEntityID VARCHAR(50) REFERENCES specimen(materialEntityID),
    constituentPartType VARCHAR(50),
    constituentPartRole VARCHAR(100),
    constituentPartProportion VARCHAR(50)
);

-- Name table (multiple names per constituent part)
CREATE TABLE mineral_name (
    nameID VARCHAR(50) PRIMARY KEY,
    constituentPartID VARCHAR(50) REFERENCES constituent_part(constituentPartID),
    name VARCHAR(200),
    nameType VARCHAR(50),
    classificationCode VARCHAR(20)
);

-- Chemistry table
CREATE TABLE chemistry (
    chemistryID VARCHAR(50) PRIMARY KEY,
    constituentPartID VARCHAR(50) REFERENCES constituent_part(constituentPartID),
    measuredChemistry TEXT,
    mineralogicalAnalysisProtocol VARCHAR(200)
);
```

---

## 8. Controlled Vocabularies

### 8.1 Classification Systems

#### Dana Classification

**Format:** XX.XX.XX.XX (hierarchical numeric)

**Example Codes:**
- 04.DA.05: Quartz (Silicates)
- 05.AB.05: Calcite (Carbonates)
- 02.CA.05a: Pyrite (Sulfides)

**Reference:** Gaines, R.V. et al. (1997) Dana's New Mineralogy

#### Nickel-Strunz Classification

**Format:** XX.XX.XX (hierarchical alphanumeric)

**Example Codes:**
- 9.AD.25: Quartz
- 5.AB.05: Calcite
- 2.EB.05a: Pyrite

**Reference:** Strunz, H. & Nickel, E.H. (2001) Strunz Mineralogical Tables

### 8.2 Material-Specific Vocabularies

#### Constituent Part Roles

Source: GeoSciML Compound Material Constituent Part Role
(http://resource.geosciml.org/classifier/cgi/compoundmaterialconstituentpartrole)

**Common Values:**
- matrix
- groundmass
- phenocryst
- xenolith
- vein
- inclusion
- alteration product

#### Proportion Terms

Source: CGI Proportion Term
(http://resource.geosciml.org/classifier/cgi/proportionterm)

**Qualitative Terms:**
- all
- dominant (>75%)
- major (25-75%)
- minor (5-25%)
- trace (<5%)

**Quantitative:** Percentage values with appropriate precision

### 8.3 Crystal Morphology Vocabularies

#### Crystal Habits

**Common Terms:**
- acicular (needle-like)
- bladed
- botryoidal
- columnar
- dendritic
- drusy
- equant
- fibrous
- foliated
- granular
- massive
- platy
- prismatic
- pyramidal
- reticulated
- tabular

#### Crystal Forms

**Common Forms:**
- cube
- octahedron
- dodecahedron
- tetrahedron
- hexagonal prism
- rhombohedron
- scalenohedron
- dipyramid
- sphenoid

#### Luster Types

**Metallic Lusters:**
- metallic
- submetallic

**Non-Metallic Lusters:**
- adamantine
- vitreous (glassy)
- resinous
- silky
- pearly
- greasy
- dull
- earthy

---

## 9. Use Cases and Examples

### 9.1 Simple Mineral Specimen

**Specimen:** Single quartz crystal

```json
{
  "materialEntity": {
    "materialEntityID": "NCSM-MIN-12345",
    "catalogNumber": "MIN-12345",
    "institutionCode": "NCSM",
    "catalogedName": "Quartz",
    "specimenDescription": "Doubly terminated crystal with exceptional clarity"
  },
  "constituentPart": [{
    "constituentPartID": "NCSM-MIN-12345-CP-001",
    "materialEntityID": "NCSM-MIN-12345",
    "constituentPartType": "Mineral",
    "constituentPartProportion": "100%",
    "constituentPartRole": "sole constituent"
  }],
  "name": [{
    "nameIdentifier": "NCSM-MIN-12345-NAME-001",
    "constituentPartID": "NCSM-MIN-12345-CP-001",
    "name": "Quartz",
    "nameType": "Classification",
    "classificationCode": "04.DA.05"
  }],
  "chemistry": {
    "constituentPartID": "NCSM-MIN-12345-CP-001",
    "measuredChemistry": "SiO2"
  },
  "materialAssertion": {
    "constituentPartID": "NCSM-MIN-12345-CP-001",
    "color": "colorless",
    "luster": "vitreous",
    "crystalHabit": "prismatic",
    "maxCrystalDimensionInMillimeters": 45
  }
}
```

### 9.2 Compound Specimen

**Specimen:** Fluorite on quartz

```json
{
  "materialEntity": {
    "materialEntityID": "SI-NMNH-98765",
    "catalogNumber": "98765",
    "institutionCode": "SI",
    "catalogedName": "Fluorite on Quartz",
    "measuredWidthInMillimeters": 120,
    "measuredHeightInMillimeters": 85,
    "measuredDepthInMillimeters": 65
  },
  "constituentPart": [
    {
      "constituentPartID": "SI-NMNH-98765-CP-001",
      "materialEntityID": "SI-NMNH-98765",
      "constituentPartType": "Mineral",
      "constituentPartRole": "matrix",
      "constituentPartProportion": "60%"
    },
    {
      "constituentPartID": "SI-NMNH-98765-CP-002",
      "materialEntityID": "SI-NMNH-98765",
      "constituentPartType": "Mineral",
      "constituentPartRole": "phenocryst",
      "constituentPartProportion": "40%"
    }
  ],
  "name": [
    {
      "nameIdentifier": "SI-NMNH-98765-NAME-001",
      "constituentPartID": "SI-NMNH-98765-CP-001",
      "name": "Quartz",
      "nameType": "Classification",
      "classificationCode": "04.DA.05"
    },
    {
      "nameIdentifier": "SI-NMNH-98765-NAME-002",
      "constituentPartID": "SI-NMNH-98765-CP-002",
      "name": "Fluorite",
      "nameType": "Classification",
      "classificationCode": "03.AB.25"
    }
  ],
  "materialAssertion": [
    {
      "constituentPartID": "SI-NMNH-98765-CP-002",
      "mineralDescription": "Pink fluorite cubes on drusy quartz",
      "color": "pink",
      "crystalForm": "cube",
      "maxCrystalDimensionInMillimeters": 18,
      "luminescence": "Purple under short wave UV"
    }
  ]
}
```

### 9.3 Type Locality Specimen

**Specimen:** Mineral from type locality with chemical analysis

```json
{
  "materialEntity": {
    "materialEntityID": "NMBE-MIN-T-001",
    "catalogNumber": "T-001",
    "institutionCode": "NMBE"
  },
  "constituentPart": [{
    "constituentPartID": "NMBE-MIN-T-001-CP-001",
    "materialEntityID": "NMBE-MIN-T-001",
    "constituentPartType": "Mineral"
  }],
  "name": [{
    "nameIdentifier": "NMBE-MIN-T-001-NAME-001",
    "constituentPartID": "NMBE-MIN-T-001-CP-001",
    "name": "Lengenbachite",
    "nameType": "Classification",
    "mineralNamePublishedIn": "Graeser, S. & Schwander, H. (1987): Mineralien und Erzbildung in den Dolomiten am Lengenbachtal (Binnatal, Kt. Wallis)",
    "nameConfirmationTechnique": "X-ray Diffraction"
  }],
  "chemistry": {
    "constituentPartID": "NMBE-MIN-T-001-CP-001",
    "measuredChemistry": "Pb6(Ag,Cu)2As4S13",
    "mineralogicalAnalysisProtocol": "Electron probe microanalysis",
    "measuredChemistrySource": "Graeser & Schwander (1987)"
  },
  "location": {
    "materialEntityID": "NMBE-MIN-T-001",
    "namedPlace": "Lengenbach Quarry",
    "isTypeLocality": true,
    "country": "Switzerland",
    "stateProvince": "Valais"
  },
  "geologicContext": {
    "materialEntityID": "NMBE-MIN-T-001",
    "formation": "Binn Formation",
    "geologicProvince": "Penninic Alps"
  }
}
```

### 9.4 Hazardous Material

**Specimen:** Radioactive mineral requiring special handling

```json
{
  "materialEntity": {
    "materialEntityID": "NHMG-MIN-RAD-056",
    "catalogNumber": "RAD-056",
    "institutionCode": "NHMG"
  },
  "constituentPart": [{
    "constituentPartID": "NHMG-MIN-RAD-056-CP-001",
    "materialEntityID": "NHMG-MIN-RAD-056",
    "constituentPartType": "Mineral"
  }],
  "name": [{
    "nameIdentifier": "NHMG-MIN-RAD-056-NAME-001",
    "constituentPartID": "NHMG-MIN-RAD-056-CP-001",
    "name": "Autunite",
    "nameType": "Classification"
  }],
  "hazard": {
    "materialEntityID": "NHMG-MIN-RAD-056",
    "hazardType": "radioactive",
    "hazardRemarks": "Contains uranium; alpha and beta radiation emitter"
  },
  "conservation": {
    "materialEntityID": "NHMG-MIN-RAD-056",
    "handlingRequirements": "Store in lead-lined container; handle with gloves; minimize exposure time",
    "damageRemarks": "Dehydration causing loss of yellow-green color and fluorescence"
  }
}
```

### 9.5 Mineral Sequence Documentation

**Specimen:** Showing paragenetic sequence

```json
{
  "geologicContext": {
    "materialEntityID": "NCMNS-MIN-SEQ-789",
    "formation": "Carolina Slate Belt",
    "geologicEvent": "Acadian orogeny",
    "mineralSequence": "Pyrite > Sphalerite > Chalcopyrite > Quartz > Calcite"
  },
  "materialAssertion": {
    "specimenDescription": "Displays clear paragenetic sequence with early pyrite overgrown by sphalerite, followed by chalcopyrite, late-stage quartz, and final calcite veinlets"
  }
}
```

---

## 10. Appendices

### Appendix A: Complete Term Index

#### Classes (9 total)

1. geoext:Chemistry
2. chrono:ChronometricAge
3. geoext:Conservation
4. geoext:ConstituentPart
5. dwc:GeologicContext
6. geoext:Hazard
7. dwc:Location
8. dwc:MaterialAssertion
9. geoext:Name

#### Properties by Class

**Chemistry (4 terms)**
- geoext:chemistryRemarks
- geoext:measuredChemistry
- geoext:measuredChemistrySource
- geoext:mineralogicalAnalysisProtocol

**ChronometricAge (1 term)**
- chrono:chronometricAgeGeologicProcess

**Conservation (3 terms)**
- geoext:damageRemarks
- geoext:handlingRequirements
- geoext:treatments

**ConstituentPart (5 terms)**
- geoext:constituentPartID
- geoext:constituentPartProportion
- geoext:constituentPartRole
- geoext:constituentPartType
- geoext:materialEntityID

**GeologicContext (5 terms)**
- geoext:geologicEvent
- geoext:geologicProvince
- geoext:lithodemicUnit
- geoext:mineralSequence
- geoext:tectonicUnits

**Hazard (2 terms)**
- geoext:hazardRemarks
- geoext:hazardType

**Location (3 terms)**
- geoext:isTypeLocality
- geoext:namedPlace
- geoext:sampledFeature

**MaterialAssertion (22 terms)**
- geoext:aggregateForm
- geoext:alterationDescription
- geoext:associatedMinerals
- geoext:cleavage
- geoext:color
- geoext:crystalForm
- geoext:crystalHabit
- geoext:exsolutionTexture
- geoext:inclusions
- geoext:luminescence
- geoext:luster
- geoext:maxCrystalDimensionInMillimeters
- geoext:measuredDepthInMillimeters
- geoext:measuredHeightInMillimeters
- geoext:measuredMassInGrams
- geoext:measuredWidthInMillimeters
- geoext:mineralDescription
- geoext:specimenDescription
- geoext:twinningLaw
- geoext:verbatimMass
- geoext:verbatimSize

**Name (9 terms)**
- geoext:catalogedName
- geoext:classificationCode
- dcterms:language
- geoext:mineralNamePublishedIn
- geoext:name
- geoext:nameConfirmationTechnique
- geoext:nameIdentifier
- geoext:nameRemarks
- geoext:nameType

**Total: 59 terms across 9 classes**

### Appendix B: Crosswalk with Extension for Geosciences (EFG)

The Mineralogy Extension is designed to be compatible with the Extension for Geosciences (EFG). Key relationships:

| MinExt Term | EFG Equivalent | SKOS Relationship |
|-------------|----------------|-------------------|
| geoext:constituentPartType | abcd-efg:RockMineralUsage | skos:broadMatch |
| geoext:geologicProvince | Pending EFG review | Under development |
| geoext:sampledFeature | abcd-efg:SamplingFeature | skos:exactMatch |

**Note:** Complete crosswalk under development by task group

### Appendix C: Metadata Term Definitions

The standard uses the following metadata qualifiers:

| Metadata Term | Definition | Qualifier |
|---------------|------------|-----------|
| Term | Machine-readable representation | rdf:label |
| Label | Human-readable label | skos:prefLabel |
| Class | Parent class | rdfs:Class |
| Material Category | Applicable scope (Specimen/Constituent Part) | tdwg:materialCategory |
| Definition | Complete explanation | skos:definition |
| Examples | Usage examples | skos:example |
| Usage Note | Implementation guidance | vann:usageNote |
| RDF Type | Category in RDF Schema | rdf:type |
| Datatype | Data type constraint | cv:DataType |
| Is Required | Mandatory flag | tdwg:isRequired |
| Note | General annotation | skos:note |
| Namespace IRI | Preferred namespace | vann:preferredNamespaceURI |
| Modified | Version date | dcterms:modified |

### Appendix D: References and Resources

#### Primary Documentation

- **Task Group Page**: https://www.tdwg.org/community/esp/mineralogy/
- **GitHub Repository**: https://github.com/tdwg/mineralogy
- **Documentation Site**: https://tdwg.github.io/mineralogy/
- **Term List**: https://tdwg.github.io/mineralogy/terms/index.html

#### Related Standards

- **Darwin Core**: https://dwc.tdwg.org/
- **Chronometric Age Extension**: https://tdwg.github.io/chrono/
- **Extension for Geosciences**: Petersen et al. (2018) DOI: 10.5194/fr-21-47-2018

#### Classification Systems

- Gaines, R.V., Skinner, H.C.W., Foord, E.E., Mason, B., Rosenzweig, A. (1997) Dana's New Mineralogy: The System of Mineralogy of James Dwight Dana and Edward Salisbury Dana. 8th Edition. John Wiley & Sons, Inc.

- Strunz, H. & Nickel, E.H. (2001) Strunz mineralogical tables: Chemical structural mineral classification system. 9th Edition. Stuttgart: Schweizerbart.

#### Controlled Vocabularies

- **GeoSciML Vocabularies**: http://resource.geosciml.org/
- **CGI Vocabularies**: https://cgi.vocabs.ga.gov.au/
- **ARDC Analytical Methods**: https://vocabs.ardc.edu.au/viewById/650

#### Semantic Web Standards

- **SKOS**: https://www.w3.org/TR/skos-reference/
- **RDF Schema**: https://www.w3.org/TR/rdf-schema/
- **Dublin Core Terms**: http://purl.org/dc/terms/

### Appendix E: Acknowledgments

This standard was developed by the Mineralogy Extension Task Group under the TDWG Earth Sciences and Paleobiology Interest Group.

**Task Group Members:**
- Ben Norton (Convener)
- Dr. Rachel Walcott (Convener)
- Thomas Burri
- Allison Dombrowski
- Nicolas Greber
- Olle Hints
- Adam Mansur
- André Puschnig
- Jolyon Ralph
- Stephen Richard
- Chris Tacker

**Contributing Organizations:**
- National Museums Scotland
- Natural History Museum Bern, Switzerland
- North Carolina Museum of Natural Sciences, USA
- Natural History Museum of Geneva, Switzerland
- Tallinn University of Technology, Estonia
- Smithsonian National Museum of Natural History, USA
- Natural History Museum Basel, Switzerland
- Mindat.org

**License:**
This documentation is licensed under Creative Commons Attribution 4.0 International License (CC BY 4.0).

---

## Document History

| Version | Date | Changes | Author |
|---------|------|---------|--------|
| DRAFT 0.1 | 2025-04-22 | Initial term list created | Task Group |
| DRAFT 0.2 | 2025-12-17 | Documentation website published | Task Group |
| DRAFT 1.0 | 2026-01-21 | Comprehensive technical documentation | Compiled from task group resources |

---

**End of Document**

*For questions, comments, or to contribute to this standard, please visit the GitHub repository at https://github.com/tdwg/mineralogy or contact the task group conveners.*
