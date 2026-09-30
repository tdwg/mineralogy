# EFG 1.0 XSD Comparison Report

Compares the three ABCDEFG (ABCD Extension for Geosciences) 1.0 schema files in this folder:

| File | Lines | Bytes | `version` attribute |
|---|---|---|---|
| `EFG_1.0_DEV.xsd` | 1561 | 78,921 | `1.00_DEV` |
| `EFG_1.0_RC1.xsd` | 1564 | 79,299 | `1.00_RC1` |
| `EFG_1.0.xsd` | 1536 | 78,551 | `1.0` |

All three file timestamps are 2025-12-17, within 11 seconds of each other. That's probably when they were copied, not when they were written, so the timestamps don't show which version came first. The version labels suggest DEV → RC1 → 1.0, but the content doesn't follow a straight line (see [Summary](#summary)).

## Summary

The three files are **nearly identical in content**. Their 22 complex types have the same content models, and all three have the same 144 enumeration values and 220 documentation annotations. With whitespace and comments ignored, only 34 lines differ between DEV and RC1, 41 between RC1 and 1.0, and 65 between DEV and 1.0. All the real differences fall into four areas:

| # | Area | DEV | RC1 | 1.0 |
|---|---|---|---|---|
| 1 | Target namespace | `http://rs.tdwg.org/abcd/efg/DEV` | `http://www.synthesys.info/ABCDEFG/1.0` | `http://rs.tdwg.org/abcd/efg/1.0` |
| 2 | `elementFormDefault` / `attributeFormDefault` | *not set* (so `unqualified`) | `qualified` / `unqualified` | `qualified` / `unqualified` |
| 3 | ABCD 2.06 import `schemaLocation` | `ABCD_2.06.xsd` (local, relative) | BGBM URL | BGBM URL |
| 4 | Global (top-level) elements | 15 | 16 (adds `SiteStratigraphy`) | 7 (drops all Unit/Identification root elements) |
| 5 | Depositional environment vocabulary | Named types; **open** list (enum ∪ `xs:string`) | Anonymous inline type; **closed** enum | Anonymous inline type; **closed** enum |

Everything else is formatting: line breaks between adjacent `</xs:complexType><xs:complexType>` tags, trailing spaces, section-divider comments, and the editor credit comments in 1.0.

Because the content doesn't follow a straight line, the order may not be DEV → RC1 → 1.0:

- **DEV and 1.0 share** the `rs.tdwg.org/abcd/efg/...` namespace pattern.
- **RC1 and 1.0 share** qualified element form, the remote ABCD import, and the closed depositional-environment list.
- **Only DEV and RC1** declare the Unit-level global elements.
- **DEV alone** has the open (extensible) depositional-environment vocabulary.

DEV looks like a later working copy made from 1.0. It restores the global elements, makes the vocabulary extensible, and points to a local ABCD file. But the files themselves don't prove that order.

---

## 1. Schema header and namespace

### DEV
```xml
<xs:schema version="1.00_DEV"
    targetNamespace="http://rs.tdwg.org/abcd/efg/DEV"
    xmlns:efg="http://rs.tdwg.org/abcd/efg/DEV"
    xmlns:abcd="http://www.tdwg.org/schemas/abcd/2.06">
  <xs:import namespace="http://www.tdwg.org/schemas/abcd/2.06" schemaLocation="ABCD_2.06.xsd"/>
```

### RC1
```xml
<xs:schema version="1.00_RC1"
    targetNamespace="http://www.synthesys.info/ABCDEFG/1.0"
    xmlns:efg="http://www.synthesys.info/ABCDEFG/1.0"
    xmlns:abcd="http://www.tdwg.org/schemas/abcd/2.06"
    elementFormDefault="qualified" attributeFormDefault="unqualified">
  <xs:import namespace="http://www.tdwg.org/schemas/abcd/2.06"
      schemaLocation="http://www.bgbm.org/TDWG/CODATA/Schema/ABCD_2.06/ABCD_2.06.XSD"/>
```

### 1.0
```xml
<!-- edited with by Falko Glöckler (MfN) -->
<!-- edited with XMLSpy v2005 rel. 3 U (http://www.altova.com) by Markus Döring (BGBM) -->
<!-- edited with XMLSPY v2004 rel. 2 U (http://www.xmlspy.com) by Charles Copp (EIM) -->
<xs:schema version="1.0"
    targetNamespace="http://rs.tdwg.org/abcd/efg/1.0"
    xmlns:efg="http://rs.tdwg.org/abcd/efg/1.0"
    xmlns:abcd="http://www.tdwg.org/schemas/abcd/2.06"
    elementFormDefault="qualified" attributeFormDefault="unqualified">
  <xs:import namespace="http://www.tdwg.org/schemas/abcd/2.06"
      schemaLocation="http://www.bgbm.org/TDWG/CODATA/Schema/ABCD_2.06/ABCD_2.06.XSD"/>
```

### Implications
- **Namespaces are mutually incompatible.** An instance document valid against one file won't validate against the others without changing its namespace. RC1 uses the older SYNTHESYS project namespace. 1.0 uses the TDWG namespace.
- **Element form (DEV only).** DEV omits `elementFormDefault`, so it defaults to `unqualified`. The **locally declared** child elements (e.g. `RockUnit/…/DepositionalEnvironment`) must then appear *without* a namespace prefix in instance documents. RC1 and 1.0 require them to be namespace-qualified. This is a significant difference for instance documents, even though the type definitions are identical.
- **Import location.** DEV expects `ABCD_2.06.xsd` in the same directory as the schema. **That file isn't in this folder, and there's no `.xsd` under `abcd/` either**, so DEV can't resolve its import as stored. RC1 and 1.0 point to the BGBM URL, which needs network access and depends on that URL still being online.
- The editor credit comments (Glöckler / Döring / Copp) appear only in 1.0.

## 2. Global element declarations

A global element can be used directly, for example as content inside ABCD's `UnitExtension` or `GatheringExtension`, and validated against the EFG schema. Local elements can be used only inside their parent type.

| Global element | Type | DEV | RC1 | 1.0 |
|---|---|:-:|:-:|:-:|
| `EarthScienceSpecimen` | `EarthScienceSpecimenType` | ✔ | ✔ | — |
| `RockUnit` | `RockUnitType` | ✔ | ✔ | — |
| `PalaeontologicalUnit` | `PalaeontologicalUnitType` | ✔ | ✔ | — |
| `MineralogicalUnit` | `MineralogicalUnitType` | ✔ | ✔ | — |
| `AllocthonousMaterial` | `AllocthonousMaterialType` | ✔ | ✔ | — |
| `UnitHostRock` | `UnitHostRockType` | ✔ | ✔ | — |
| `Alteration` | `AlterationType` | ✔ | ✔ | — |
| `SiteStratigraphy` | `SiteStratigraphyType` | — | ✔ | — |
| `MineralRockIdentified` | `MineralRockIdentifiedType` | ✔ | ✔ | — |
| `IdentificationAnalysis` | `IdentificationAnalysisType` | ✔ | ✔ | ✔ |
| `NamedGeologicalFeature` | `xs:string` | ✔ | ✔ | ✔ |
| `DatingQualifier` | `xs:string` | ✔ | ✔ | ✔ |
| `StratigraphicMeasurementsOrFacts` | anonymous | ✔ | ✔ | ✔ |
| `AnalysisDateTime` | anonymous | ✔ | ✔ | ✔ |
| `AnalysisReferences` | anonymous | ✔ | ✔ | ✔ |
| `Certainty` | `xs:string` | ✔ | ✔ | ✔ |
| **Total** | | **15** | **16** | **7** |

### Placement
- **DEV and RC1** declare the Unit, Identification and Gathering root elements together at the top of the file, before the type library.
- **1.0** places `IdentificationAnalysis` and `NamedGeologicalFeature` *among the type definitions* under the section comments ("Elements extending ABCD Unit/Identifications/Identification/Result" and "Elements extending ABCD Gathering"). RC1 labels those sections "Types extending …" instead.

### Implications
- **In 1.0, the core EFG containers can't be used as root elements.** `RockUnit`, `MineralogicalUnit`, `PalaeontologicalUnit`, `EarthScienceSpecimen`, `MineralRockIdentified` and the rest have no global declaration. A cross-reference check shows the types below are defined but **never referenced** anywhere in 1.0:
  `EarthScienceSpecimenType`, `PalaeontologicalUnitType`, `MineralogicalUnitType`, `AllocthonousMaterialType`, `UnitHostRockType`, `AlterationType`, `SiteStratigraphyType`.
  (`RockUnitType` and `MineralRockIdentifiedType` still appear because other types reference them.) Instance content for these units therefore can't be strictly validated against 1.0. It would be accepted only through a lax wildcard or an `xsi:type` override.
- **DEV** declares `SiteStratigraphyType` but has no element that uses it, so the type is unreachable there too.
- **RC1** is the only file where every named type is reachable through a global element or a reference.
- No file has a dangling reference: every `efg:` `ref`/`type` resolves within its own file.

## 3. Depositional environment vocabulary

This is the only change to a content model. It affects `RockUnitType / DepositionalEnvironment / DepositionalEnvironmentType` (the keyword element, `maxOccurs="unbounded"`).

### DEV: named, extensible
```xml
<xs:element name="DepositionalEnvironmentType"
            type="efg:DepositionalEnvironmentEnumExtensionType" maxOccurs="unbounded"/>
...
<xs:simpleType name="DepositionalEnvironmentEnumExtensionType">
  <xs:union memberTypes="efg:DepositionalEnvironmentEnumType xs:string"/>
</xs:simpleType>
<xs:simpleType name="DepositionalEnvironmentEnumType">
  <xs:restriction base="xs:string">
    <xs:enumeration value="alluvial fan"/> ... <xs:enumeration value="wet floodplain"/>
  </xs:restriction>
</xs:simpleType>
```

### RC1 and 1.0: anonymous, closed
```xml
<xs:element name="DepositionalEnvironmentType" maxOccurs="unbounded">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:enumeration value="alluvial fan"/> ... <xs:enumeration value="wet floodplain"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

### Implications
- All three files have the **same 57 enumeration values in the same order**. The vocabulary itself didn't change.
- **In DEV, any string validates.** A union with `xs:string` accepts any value, so the list is only a recommendation. In RC1 and 1.0, only the 57 listed terms are valid.
- DEV's named types can be reused or restricted by other schemas. RC1 and 1.0 define the type inline, so it can't be reused.
- This is the only reason DEV has two `xs:simpleType` declarations at the top level while RC1 and 1.0 have none.

## 4. Unchanged content

All three files define the same 22 named complex types, with identical content models:

`EarthScienceSpecimenType`, `RockUnitType`, `PalaeontologicalUnitType`, `MineralogicalUnitType`, `AllocthonousMaterialType`, `UnitHostRockType`, `AlterationType`, `MineralRockIdentifiedType`, `SiteStratigraphyType`, `StratigraphicAttributionsType`, `ChronostratigraphicAttributionsType`, `LithostratigraphicAttributionsType`, `BiostratigraphicAttributionsType`, `MagnetostratigraphicDeterminationsType`, `IsotopeStratigraphicDeterminationsType`, `RadiometricDatesType`, `StratigraphicSectionType`, `IdentifiersType`, `IdentificationAnalysisType`, `AnalysisAtomisedType`, `AssociatedFossilAssemblageType`, `AssociatedMineralAssemblageType`.

| Metric | DEV | RC1 | 1.0 |
|---|---|---|---|
| Named complex types | 22 | 22 | 22 |
| Named simple types | 2 | 0 | 0 |
| `xs:element` declarations (all levels) | 241 | 242 | 233 |
| `xs:enumeration` values | 144 | 144 | 144 |
| `xs:documentation` annotations | 220 | 220 | 220 |

The differences in element counts come entirely from the global declarations in section 2. Documentation text, including existing typos such as "thr rock" and the "Allocthonous" spelling, is identical in all three files.

## 5. Formatting differences only

- RC1 and 1.0 put line breaks between `</xs:complexType><xs:complexType name="AllocthonousMaterialType">` and `…name="UnitHostRockType">`. DEV runs the first pair together on one line, and RC1 runs the second.
- RC1 has `<!--  -->` divider comments, and in one place a type definition directly follows a comment on the same line.
- The section-comment wording differs: "Types extending ABCD Identification/Result" (DEV, RC1) vs. "Elements extending ABCD Unit/Identifications/Identification/Result" (1.0). There is also "library of other reused types" vs. "library of reused types".
- Trailing whitespace differs on a few lines.

## 6. Which file to use

| Need | Recommended file | Reason |
|---|---|---|
| Match published EFG 1.0 instance data (TDWG namespace) | `EFG_1.0.xsd` | Official version and namespace, but it can't validate Unit-level content as root elements |
| Validate Unit/Identification fragments as root elements | `EFG_1.0_RC1.xsd` | Most complete set of global elements; closed vocabulary; qualified form |
| Allow depositional-environment terms outside the vocabulary | `EFG_1.0_DEV.xsd` | Union with `xs:string`. You'd also need to add `ABCD_2.06.xsd` locally and check whether unqualified element form is intended |

As `README.txt` notes, all three import **ABCD 2.06**, and none is compatible with ABCD 3.0.
