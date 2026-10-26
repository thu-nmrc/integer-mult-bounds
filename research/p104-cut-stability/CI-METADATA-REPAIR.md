# Preserve a legacy standalone capsule without opting it into generic CI

The first hosted PR5557 run, 40207759843, stopped in two unchanged shared
onboarding tests before selecting this package's mathematical replay. Both
failed with `use an exact Git-tracked input path from HEAD: MANIFEST.json`.

An authenticated scan of all 3317 canonical declarations at base
`13be6ac685845c1ff671f5d26e7166165abd998e` found exactly one such input:
`research/wordram-ntt-kernel/VERIFY.json`, blob
`4ae0f65622d1159e1c8a051155c2ac9e2579238f`. Its bytes are identical in the
base and initial PR5557 head. This is an archive-only standalone source-export
declaration; its generic TASK/SOURCES/VERIFY schema is absent. It is unrelated
to the new P104 package's empty external input list.

Changing only its input spelling would still wrongly select it for generic
replay, and would break its own integrity manifest. The repair instead:

1. Renames that descriptor byte-identically to `STANDALONE-VERIFY.json`.
2. Updates its inventory key in its own `MANIFEST.json`, retaining the exact
   descriptor hash.
3. Corrects the one README reference to the descriptor name and updates that
   README's inventory hash.

Every mathematical source, data, result, license and attribution byte stays
unchanged. No shared planner, schema validation or scientific acceptance gate
is weakened. The original three metadata files are retained in
`validation/legacy-canonical/`, with exact canonical Git/blob and SHA256 pins
in SOURCES.json. The old standalone command remains `python3 -B verify.py`
inside its own package; it is deliberately not converted to a registered
generic replay.

The independent authenticated planner reproduction confirms 3316 base names
after removal of this unintended registration, 3317 including the new P104
package, and only the new P104 package selected for this PR. No other existing
manifest input consumes a path under the legacy package prefix. The scan and
rename receipts are retained in `validation/`; the actual committed planner
and hosted tests are checked separately.

The final isolated standalone variant passes its own complete normal replay
in 7.617 wall seconds, including 8 NTT tests, 65537 RAM multiply slices, 5096
butterfly cases, 277 whole-program cases and 20 recovery pairs at each of two
precisions. All 32 inventory hashes still match afterward. Its final manifest
SHA256 is `5b4eba8e8b915be9af8f2415de33e36e77e4c485238d91929b06b68a29ba54f0`.
The author intentionally rejects `-O`; the independent rename control checks
that rejection. No optimized-mode PASS, Lean execution, universal machine
theorem, generic registration or scientific adoption is inferred from this
metadata repair. The P104 package itself supports both normal and optimized
replay as documented separately.
