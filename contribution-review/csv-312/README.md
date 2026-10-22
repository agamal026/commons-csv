# CSV-312: archived validation evidence

This packet documents the one-file test contribution for [CSV-312](https://issues.apache.org/jira/browse/CSV-312). It preserves existing local execution records; preparing this packet did not rerun tests.

## Source identity and chronology

- Baseline: [`b217f58fac4bdf26507cde121ffb9cd50fd335e7`](https://github.com/apache/commons-csv/commit/b217f58fac4bdf26507cde121ffb9cd50fd335e7).
- Published equivalent source: [`f609cb0eab7614c7eac7214aa608381dd4e8c120`](https://github.com/agamal026/commons-csv/commit/f609cb0eab7614c7eac7214aa608381dd4e8c120), parent `b217f58fac4bdf26507cde121ffb9cd50fd335e7`, tree `8ab8ccf767cd4495c1a7f2a98eb5a84440468ae8`.
- Added file: [JiraCsv312Test.java](https://github.com/agamal026/commons-csv/blob/f609cb0eab7614c7eac7214aa608381dd4e8c120/src/test/java/org/apache/commons/csv/issues/JiraCsv312Test.java), 71 lines / 3,218 bytes; SHA-256 `3886666340f8965035535ff7fe2067d7d1e82c747b7474951baf7087213e7e05`.

The successful default build finished **2026-10-22 at 05:14:16 UTC** on the baseline plus the uncommitted reviewed test. The equivalent source commit was created later, at **06:26:18 UTC**, with the same baseline and file bytes. The archived build did not check out that later commit. The published source diff contains only the added test file.

## Scope and results

Four cases combine LF or CRLF inside quoted header names with bare RFC4180 parsing or automatic header extraction. Record boundaries stay CRLF. Bare parsing checks all three complete records; automatic extraction checks exact header names, two data records, and all four named values. This characterizes supported behavior; the reported exception was not reproduced.

| Archived check | Result |
| --- | --- |
| Focused `JiraCsv312Test` | 4 tests; 0 failures, 0 errors, 0 skips |
| Full default build | 39 suites; 989 reported tests: 978 passed, 0 failures, 0 errors, 11 existing skips |
| New class in full build | All 4 cases passed |
| Default gates | BUILD SUCCESS; coverage checks met; RAT, japicmp, SpotBugs, PMD/CPD, Javadoc and Checkstyle completed; Checkstyle reported 0 violations |

The 11 skips are in existing `CSVParserTest` and `CSVPrinterTest`; individual reasons are retained in `final-summary.json`. `test-totals.json` derives suite counts and focused case outcomes from the original XML and records their SHA-256 hashes. System properties and classpaths are excluded.

## Reviewer commands and environment

From a checkout of the published source, with Maven and a full JDK available:

```sh
mvn -B -ntp -Dtest=JiraCsv312Test test
mvn -B -ntp
```

These are ordinary reviewer commands, not a claim of new execution. The focused receipt records `JiraCsv312Test` as its selector. The saved default-goal sequence is:

```text
clean verify apache-rat:check japicmp:cmp spotbugs:check pmd:check pmd:cpd-check javadoc:javadoc checkstyle:check
```

The archived run used Linux, OpenJDK 17.0.20 and Maven 3.9.11. It additionally supplied `-s`, `-Dmaven.repo.local` and `-DjavadocExecutable` for its environment. Maven used the environment's existing network proxy. A native `javadoc` executable was absent, so the launcher invoked the installed JDK's real Javadoc module. This was not an unmodified plain-Maven run. No required default check was disabled; routine resource/report skips remain visible in the log.

## Earlier failures and final-log qualifications

The initial focused attempt failed during parent-POM resolution and executed no tests. The first full attempt completed tests but failed because Javadoc's native launcher was unavailable. The next full attempt reached Checkstyle and failed on two operator-wrapping violations. After moving the two `+` operators to the preceding lines, the final default sequence passed. `prior-failures.txt` preserves the relevant fatal and terminal excerpts; `redactions.json` records original full-log hashes and selected ranges. The complete earlier logs are not included in this compact packet.

The final log is retained in full, including nonfatal SPDX network-error stack traces with cached-license fallback, CycloneDX warnings, PMD warnings, and disabled tests. It is not a warning-free run. These records establish local results in the stated environment, not hosted CI, maintainer approval, or upstream acceptance.

## Redaction and integrity

Only these literal prefixes were substituted in the full final log; no lines were removed or reordered:

| Placeholder | Redacted prefix category | Final-log replacements |
| --- | --- | ---: |
| `<CHECKOUT>` | Temporary source checkout directory | 27 |
| `<MAVEN_REPOSITORY>` | Temporary Maven dependency-cache directory | 2 |
| `<JAVA_HOME>` | Installed JDK directory | 1 |

Original final-log SHA-256: `3b731c0af9fe57f2a264945b3d16e593a76744c82397a82a2640a1ba65a96eb2`. Sanitized final-log SHA-256: `35e75ca5d8bacb0b4fd693f235247b474d18e221880d80a2fbdba02b6b82335c`. Both contain 481 lines. `redactions.json` records every substitution by rule, original line and count; omitted literal prefixes are identified by hashes without revealing their values. `SHA256SUMS` covers all other files in this packet. Private settings, identities and credentials are not included.

Implementation, review and evidence preparation were AI-assisted. Agent review is not human maintainer review.
