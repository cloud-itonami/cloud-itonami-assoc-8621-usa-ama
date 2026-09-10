(ns association.facts
  "Industry rule/policy-statement catalog for the American Medical
  Association (AMA, Wikidata Q465697) -- a 27th industry-association-
  level source (see cloud-itonami-assoc-6419-jpn-zenginkyo, -6512-jpn-sonpo,
  -6612-jpn-jsda, -6419-deu-bankenverband, -6612-usa-finra, -6512-usa-naic,
  -6920-jpn-jicpa, -6920-usa-aicpa, -6419-fra-fbf, -6511-jpn-seiho,
  -6910-jpn-nichibenren, -6810-jpn-recaj, -6411-jpn-boj, -6120-usa-ctia,
  -5110-usa-a4a, -3510-usa-eei, -2910-deu-vda, -5510-usa-ahla,
  -2100-usa-phrma, -4719-usa-nrf, -4100-usa-agc, -6020-usa-nab,
  -3600-usa-awwa, -4923-usa-ata, -5610-usa-nra, -2011-usa-acc for the
  first twenty-six) per ADR-2607141700 (cloud-itonami-compliance-fact-federation).
  The FIRST entry aligned to ISIC 8621 (general medical practice
  activities) -- a new industry code for this family. A rule not in
  this table has NO spec-basis, full stop; extend `catalog`, do not
  invent an id/url/date.

  aha.org (American Hospital Association) was attempted first this
  tick but blocked WebFetch entirely (HTTP 403 across multiple pages,
  including /about/history, /125, and /about) -- abandoned without
  forcing it, pivoted to AMA instead.

  Both entries were directly WebFetch-verified against
  ama-assn.org's own pages. Neither states a specific month/day for
  its 1847 founding -- 'AMA History' confirms the 1847 establishment
  year but no month/day; 'Why does the medical profession need a code
  of ethics?' confirms the Code of Medical Ethics 'was first adopted at
  the AMA's founding meeting in 1847', likewise year-only. Both
  :established-date values are therefore deliberately year-only rather
  than invented full dates (secondary sources place the founding at
  May 7, 1847 in Philadelphia, but that specific date was not directly
  confirmed on ama-assn.org itself).")

(def catalog
  "assoc-slug -> vector of self-regulatory rule entries."
  {"ama"
   [{:association-rule/id "ama.ama-history"
     :association-rule/title "AMA History"
     :association-rule/association "ama"
     :association-rule/isic "8621"
     :association-rule/country "USA"
     :association-rule/kind :governance-program
     :association-rule/url "https://www.ama-assn.org/about/ama-history/ama-history"
     :association-rule/url-provenance :official-association-site
     :association-rule/established-date "1847"
     :association-rule/retrieved-at "2026-07-16"
     :association-rule/topic #{:governance}}
    {:association-rule/id "ama.code-of-medical-ethics"
     :association-rule/title "Code of Medical Ethics"
     :association-rule/association "ama"
     :association-rule/isic "8621"
     :association-rule/country "USA"
     :association-rule/kind :self-regulatory-code
     :association-rule/url "https://www.ama-assn.org/about/ethics/why-does-medical-profession-need-code-ethics"
     :association-rule/url-provenance :official-association-site
     :association-rule/established-date "1847"
     :association-rule/retrieved-at "2026-07-16"
     :association-rule/topic #{:ethics :medical-ethics}}]})

(defn spec-basis [assoc-slug] (get catalog assoc-slug))

(defn coverage
  ([] (coverage (keys catalog)))
  ([slugs]
   (let [have (filter catalog slugs)
         missing (remove catalog slugs)]
     {:requested (count slugs)
      :covered (count have)
      :covered-associations (vec (sort have))
      :missing-associations (vec (sort missing))
      :note (str "cloud-itonami-assoc-8621-usa-ama Wave 0 (ADR-2607141700): "
                 (count (get catalog "ama")) " ama entries seeded with an "
                 "official ama-assn.org citation. Extend "
                 "`association.facts/catalog`, never fabricate a rule id/url.")})))

(defn by-topic [assoc-slug topic]
  (filterv #(contains? (:association-rule/topic %) topic) (spec-basis assoc-slug)))
