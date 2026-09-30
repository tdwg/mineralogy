# Interoperability

This directory holds the work needed to use the Mineralogy Extension (MinExt) terms alongside existing collection-data standards and in the applications that already consume them. It has two parts:

- **Mappings** between MinExt and related standards: Darwin Core (DwC), ABCD-EFG, and the GeoCASe aggregator.
- **Schemas** for publishing MinExt data, generated to match the structure of existing schemas used for the same purpose.

## Contents

```
interop/
├── mappings/
│   ├── minext_term_crosswalk.csv          # MinExt terms vs. DwC issues, repo term list, and KOS
│   ├── minext_dwc_issue_terms.csv         # MinExt term proposals filed as DwC issues
│   ├── minext_dwc_issue_terms.xlsx        # Spreadsheet version of the above
│   ├── efg/                               # ABCD Extension for Geosciences (EFG) schemas and mapping
│   └── geocase_v1/                        # GeoCASe 2.0 full-index harvest (2026-08-31)
└── schemas/
    ├── reference/                         # Existing schemas the generated schemas must follow
    └── generated/                         # Schemas generated for MinExt
```

## Mappings

### `minext_term_crosswalk.csv`

One row per concept. It reconciles each MinExt term across three sources that drifted apart during the DwC public review:

| Column group | Source | Key columns |
|---|---|---|
| `dwc_issue_*`, `issue_*`, `review_outcome`, `final_status` | The term as proposed in the tdwg/dwc GitHub issues | term name, issue numbers and URLs, type, class, definition, usage notes, examples, review outcome |
| `repo_*` | The term list in this repository | term, label, class, namespace, material scope, definition, `repo_match`, `repo_vs_issue_definition` |
| `kos_*` | The published vocabulary at kos.geospecimens.org | notation, preferred label, IRI, status, definition, `kos_vs_issue_definition` |
| `notes` | | Actions needed to bring the sources into line |

Use it to find where the repo term list is out of date. For example, several terms were renamed to plural list forms during review (`geologicalMaterialName` → `geologicalMaterialNames`, `classificationCode` → `classificationCodes`), and the `GeologicalMaterial` class was created during review and isn't yet in the repo list.

### `minext_dwc_issue_terms.csv` / `.xlsx`

One row per tdwg/dwc issue filed for MinExt, with issue state, dates, labels, the proposed term (name, label, type, class, definition, usage notes, examples, datatype) and its review outcome. The class proposals (`Hazard`, `Chemistry`, `GeoName`) were withdrawn in favor of a flatter model, and their properties were re-homed to `dwc:MaterialEntity` or `dwc:GeologicalMaterial`. The `outcome_notes` column records the status of each issue after the 2026 public review.

### `efg/`

ABCD Extension for Geosciences (ABCD-EFG), the geoscience extension of ABCD and the basis for the GeoCASe schema.

| File | Description |
|---|---|
| `EFG_1.0.xsd` | Published EFG 1.0 (`http://rs.tdwg.org/abcd/efg/1.0`) |
| `EFG_1.0_RC1.xsd` | Release candidate 1 (`http://www.synthesys.info/ABCDEFG/1.0`) |
| `EFG_1.0_DEV.xsd` | Development copy (`http://rs.tdwg.org/abcd/efg/DEV`) |
| `ABCD_2.1.xsd` | ABCD schema |
| `EFG_1.0_RC1_Data_Dictionary.csv` | One row per element path in RC1: type, cardinality, enumerations, and definition |
| `EFG_1.0_XSD_Comparison.md` | Detailed comparison of the three EFG files |
| `minext_to_EFG_1.0_RC1_Mapping.xlsx` | MinExt terms mapped to EFG RC1 elements |

The three EFG files share the same 22 complex types but differ in namespace, element form, ABCD import location, global elements, and whether the depositional-environment vocabulary is open or closed. The mapping targets **RC1** because it's the only version in which every EFG unit type can be validated as a root element. All three import ABCD 2.06 and aren't compatible with ABCD 3.0. See `EFG_1.0_XSD_Comparison.md` for details.

### `geocase_v1/`

A full harvest of the GeoCASe 2.0 index taken on 2026-08-31: 1,827,648 specimen records with 147 columns, from 11 providers. It shows which EFG-derived fields data providers actually populate, which helps test and prioritize the mappings.

- `merged/`: the records as JSON (1.9 GB, source shape) and CSV (1.1 GB, flattened), plus `geocase_README.md`, which documents provenance, flattening rules, summary statistics, and caveats.
- `zip/`: compressed copies of the merged files.

These records belong to the providing institutions. This directory asserts no licence over them. Check each provider's terms before redistributing, and cite the holding institution.

## Schemas

### `reference/`

Darwin Core Occurrence, Event, and Taxon definitions in the GBIF extension format (`http://rs.gbif.org/extension/`), the format the GBIF Integrated Publishing Toolkit (IPT) uses to define core and extension data types. These files are the guide for the generated schemas, which must follow the same structure:

- A root `<extension>` element with `dc:title`, `name`, `namespace`, `rowType`, `dc:issued`, `dc:subject`, `dc:relation`, and `dc:description`.
- One `<property>` element per term with `name`, `namespace`, `qualName`, `dc:relation`, `dc:description`, `examples`, and `required`, plus `group`, `type`, and `thesaurus` where they apply.
- Validation against `http://rs.gbif.org/schema/extension.xsd`.

### `generated/`

MinExt schemas generated from the crosswalk. This directory is currently empty.

Crosswalk columns map to extension attributes as follows:

| Extension attribute | Crosswalk source |
|---|---|
| `name` | `dwc_issue_term` |
| `namespace` | term namespace (`http://rs.tdwg.org/dwc/terms/` for approved DwC terms) |
| `qualName` | `namespace` + `name` |
| `group` | `issue_organized_in_class` |
| `dc:description` | `issue_definition` (plus `issue_usage_notes`) |
| `examples` | `issue_examples` |
| `dc:relation` | `dwc_issue_urls`, until term pages are published |
| `type` | `datatype`, from `minext_dwc_issue_terms.csv` |

Only terms with a `final_status` of approved should be included. Terms that are unresolved or withdrawn are left out until their issues close.
