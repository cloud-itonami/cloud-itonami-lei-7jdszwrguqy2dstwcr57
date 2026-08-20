# cloud-itonami-lei-7jdszwrguqy2dstwcr57

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by BANK LEUMI LE-ISRAEL LTD..**

This repository archives the publicly published Privacy Policy of **BANK LEUMI LE-ISRAEL LTD.** (IL), with source-url and retrieval-date provenance, per
ADR-2607110300 (`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`).
Read-only reference/archive repository — not a governed Advisor/Governor actor.

- LEI: `7JDSZWRGUQY2DSTWCR57` (GLEIF entity status ACTIVE, registration ISSUED)
- Source: https://www.leumi.co.il/privacy-policy
- Retrieved: 2026-07-25T06:37:00Z
- SHA-256 of archived text: `9376fc30298f571a7a1f13d5da5dda1fe8c01d601dd2fa2f834c509c09c20f2f`

Acquired by `scripts/lei-acquire.cljs` as part of the worldwide-broadening
continuation that followed the 2026-07-25 coverage audit, which found the
catalog's real reach was 27 countries with the United States at 55%.

## Verified public-register citations

`facts/catalog.edn` records 56 citations for this legal entity, drawn from **three
independent authorities**: GLEIF, Companies House (United Kingdom), and the
issuer's own website. Every row was retrieved before it was written down; nothing
in that file is asserted from memory.

Check them against the live web:

```sh
nbb tools/verify_citations.cljs facts/catalog.edn --min 50
```

Exit codes are three, not two — "nothing was checked" must not look like
"nothing was wrong":

| exit | meaning |
|---|---|
| 0 | every citation fetched, every substring present, floor met |
| 1 | answered, and at least one citation is wrong (`DRIFT <id> <why>`) |
| 2 | **could not answer** — catalog missing/unparseable, zero rows, or fewer rows than `--min` |

### Read `:cite/row-kind` before you read the claims

Not every row identifies this company, and the file says so per row:

- **`:identity`** (22) — names the entity, its identifiers, or a specific related
  legal entity. Repoint the URL at another company and the row fails.
- **`:attribute`** (34) — true of this entity but **not only** of it (country `IL`,
  status `ACTIVE`, governing law `Israeli Law`, SIC `64191`). Such a row can
  survive a swap to a similar company. Recorded because it is checked and true,
  not because it identifies.

Treating all 56 as identifying would overstate what the catalog proves: 28 of them
come from a *single* GLEIF document — one authority speaking once. Three rows were
reclassified from `:identity` to `:attribute` because the swap test below
**measured** them surviving; the taxonomy is checked, not asserted.

### The home register is not cited — but its number is still corroborated

GLEIF names `RA000406` — the Israeli Corporations Authority (Department of
Justice) — as both the register of record and the validation authority, and gives
the company number as `520018078`. That register could not be cited: the open-data
copy on data.gov.il answers HTTP 500 to every query form, its bulk CSV is 254 MB,
and the Tagidim portal is a POST-only search form. All routes tried are named in
`:catalog/unreachable`; none was worked around.

Unlike others in this repository family, however, **the home registration number
does not rest on GLEIF alone.** Companies House, asked about the UK subsidiary
`00640370`, publishes its person with significant control and prints in the UK
register's own words: place registered *Israeli Companies Register*, registration
number **`52-001807`** — `520018078` without its trailing check digit. Two states
that did not consult each other carry the same number.

The catalog also records three points where the two authorities **disagree** —
the UK register still carries the pre-2022 legal name, a 2016 address GLEIF has
since superseded, and a `Liquidation` status for the subsidiary that GLEIF returns
as `ACTIVE`. Those are recorded, not reconciled.

### How this gate was shown to discriminate

Measured, not assumed:

| break | result |
|---|---|
| unmodified | exit 0, `CHECKED 56 OK 56 FAIL 0` |
| one substring falsified (`520018078`→`520018079`) | exit 1 naming **only** `gleif-registered-as` |
| GLEIF URL repointed at BANK HAPOALIM, a real Israeli near-twin | exit 1: **all 9** `:identity` rows on that URL fail, 11 of 19 `:attribute` rows survive — exactly what the two kinds claim |
| Companies House URL repointed at TESCO PLC | exit 1, 16 of 17 UK rows fail; the one survivor is `:attribute` (`Public limited Company`) |
| host made unresolvable | exit 1 `fetch-error`, not a silent pass |
| catalog missing / empty / unparseable | exit 2 |
| `--min 100` against 56 rows / `--min 56` against the same rows | exit 2 `FLOOR`, then exit 0 |

### Known gap in this repository, not fixed by this change

The privacy-policy URL recorded above (`https://www.leumi.co.il/privacy-policy`)
now answers **HTTP 404**; the live document has moved to
`https://www.leumi.co.il/he/privacy_policy`, which is what the two `:issuer` rows
cite. The archived text in `80-data/public/tos.journal.edn` and its recorded
SHA-256 were **not** re-verified here and nothing in `facts/catalog.edn` claims
they are current.
