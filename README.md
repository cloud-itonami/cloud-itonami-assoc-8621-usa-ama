# cloud-itonami-assoc-8621-usa-ama

Industry rule/policy-statement catalog for the **American Medical
Association** (AMA) — the FIRST entry aligned to **ISIC 8621** (general
medical practice activities), a new industry code for this family.
Alongside
[`cloud-itonami-assoc-6419-jpn-zenginkyo`](https://github.com/cloud-itonami/cloud-itonami-assoc-6419-jpn-zenginkyo),
[`-6512-jpn-sonpo`](https://github.com/cloud-itonami/cloud-itonami-assoc-6512-jpn-sonpo),
[`-6612-jpn-jsda`](https://github.com/cloud-itonami/cloud-itonami-assoc-6612-jpn-jsda),
[`-6419-deu-bankenverband`](https://github.com/cloud-itonami/cloud-itonami-assoc-6419-deu-bankenverband),
[`-6612-usa-finra`](https://github.com/cloud-itonami/cloud-itonami-assoc-6612-usa-finra),
[`-6512-usa-naic`](https://github.com/cloud-itonami/cloud-itonami-assoc-6512-usa-naic),
[`-6920-jpn-jicpa`](https://github.com/cloud-itonami/cloud-itonami-assoc-6920-jpn-jicpa),
[`-6920-usa-aicpa`](https://github.com/cloud-itonami/cloud-itonami-assoc-6920-usa-aicpa),
[`-6419-fra-fbf`](https://github.com/cloud-itonami/cloud-itonami-assoc-6419-fra-fbf),
[`-6511-jpn-seiho`](https://github.com/cloud-itonami/cloud-itonami-assoc-6511-jpn-seiho),
[`-6910-jpn-nichibenren`](https://github.com/cloud-itonami/cloud-itonami-assoc-6910-jpn-nichibenren),
[`-6810-jpn-recaj`](https://github.com/cloud-itonami/cloud-itonami-assoc-6810-jpn-recaj),
[`-6411-jpn-boj`](https://github.com/cloud-itonami/cloud-itonami-assoc-6411-jpn-boj),
[`-6120-usa-ctia`](https://github.com/cloud-itonami/cloud-itonami-assoc-6120-usa-ctia),
[`-5110-usa-a4a`](https://github.com/cloud-itonami/cloud-itonami-assoc-5110-usa-a4a),
[`-3510-usa-eei`](https://github.com/cloud-itonami/cloud-itonami-assoc-3510-usa-eei),
[`-2910-deu-vda`](https://github.com/cloud-itonami/cloud-itonami-assoc-2910-deu-vda),
[`-5510-usa-ahla`](https://github.com/cloud-itonami/cloud-itonami-assoc-5510-usa-ahla),
[`-2100-usa-phrma`](https://github.com/cloud-itonami/cloud-itonami-assoc-2100-usa-phrma),
[`-4719-usa-nrf`](https://github.com/cloud-itonami/cloud-itonami-assoc-4719-usa-nrf),
[`-4100-usa-agc`](https://github.com/cloud-itonami/cloud-itonami-assoc-4100-usa-agc),
[`-6020-usa-nab`](https://github.com/cloud-itonami/cloud-itonami-assoc-6020-usa-nab),
[`-3600-usa-awwa`](https://github.com/cloud-itonami/cloud-itonami-assoc-3600-usa-awwa),
[`-4923-usa-ata`](https://github.com/cloud-itonami/cloud-itonami-assoc-4923-usa-ata),
[`-5610-usa-nra`](https://github.com/cloud-itonami/cloud-itonami-assoc-5610-usa-nra),
and
[`-2011-usa-acc`](https://github.com/cloud-itonami/cloud-itonami-assoc-2011-usa-acc).
Part of the [`cloud-itonami`](https://github.com/cloud-itonami)
compliance-fact family (ADR-2607141700,
`cloud-itonami-compliance-fact-federation`, in `com-junkawasaki/root`).

## Scope

A **read-only reference/archive** catalog — not an Advisor⊣Governor
actuation actor. It proposes or executes nothing on AMA's behalf.

Coverage is reported honestly (see `association.facts/coverage`): an
association not in `catalog` has **no spec-basis**, full stop — never
fabricate one.

## Data

- `src/association/facts.kotoba` — the catalog, source of truth.
- `src/association_facts.kotoba` — the same catalog as Kotoba, which
  reaches the oracle, wasm and both native ISAs.
- `schema/association-rule.edn` — DataScript schema.
- `data/datascript-tx.edn` — derived DataScript tx-data (query this
  alongside other `cloud-itonami`/`etzhayyim` compliance-fact sources via
  `com-junkawasaki/root`'s `scripts/compliance-fact-query.cljs`).

**Six entries**, every one of them fetched and read before it was
written down, and every one citing a page on `ama-assn.org` or its
`code-medical-ethics` subdomain. All six were re-fetched on 2026-09-10
and returned HTTP 200.

The American Hospital Association (`aha.org`) was attempted first when
this repo was seeded but blocked WebFetch entirely across multiple
pages — abandoned without forcing it.

Dates are recorded at **the granularity the cited page states, and no
finer**:

| Entry | Date recorded | Because the page says |
|---|---|---|
| AMA History | `1847` | founding year, no month/day |
| Code of Medical Ethics | `1847` | "first adopted at the AMA's founding meeting in 1847" |
| Principles of Medical Ethics | `1957-06`, revised `2001-06` | "Adopted June 1957; revised June 1980; revised June 2001" |
| Declaration of Professional Responsibility | `2001-12-04` | "Adopted by the AMA House of Delegates on Dec. 4, 2001" |
| Council on Ethical & Judicial Affairs | *(absent)* | states no founding year |
| CPT® | *(absent)* | states no creation year |

An absent date is a fact about the citation, not a gap to fill from
memory — secondary sources have fuller dates for several of these, and
that is precisely why they are not recorded here.

## Tests

`test/` holds two suites: the catalog's own invariants, and a
field-by-field parity check between the Clojure catalog and the Kotoba
port (a catalog is exactly the shape where checking a sample only
checks the entries someone already looked at).

⚠ **Neither suite currently runs under `kbb -M:test`.** The
2026-09-10 workspace-wide rename moved every source to `.kotoba`, and
`cognitect.test-runner` discovers `.clj`/`.cljc` only — so the command
exits 0 having run **zero tests**, which looks exactly like passing.
Until this repo genuinely builds as Kotoba, the suites are run by
placing the sources on a classpath under their Clojure extensions.
Both were run that way against the six-entry catalog: 15 tests, 172
assertions, plus seven deliberate mutations confirmed to turn it red.

## License

AGPL-3.0-or-later (matches the `cloud-itonami-iso3166-*` /
`-municipality-*` / `-assoc-*` / `-lei-*` convention). Policy text
itself remains AMA's; this repo stores only citation metadata
(id/title/url/dates), not full text.
