# assets/gate4 — the labelled delivery-photo set

Twenty delivery photos for the Gate 4 delivery gate, every one
of them generated and labelled `generated` in the manifest.

- `manifest.json` — the label and expectation for each photo:
  12 `true_*` photos of the mandated matte red gooseneck
  kettle, 5 `wrong_*` photos (black and silver kettles, an
  electric jug, a stovetop kettle, a toaster), and 3 edge
  cases (`blurry_true_kettle`, `box_only_empty`,
  `packaging_only`).
- `measurements.json` — measurement v1: phrase-box
  co-location. This is the version that passed a black kettle
  by reading a label box's overlap as colour: **12 of 20**
  verdicts in the right direction.
- `measurements_v2.json` — measurement v2: the SAM 3.1 mask
  decoded to pixels — colour is the photo's pixels under the
  mask, form is the mask's fill. **18 of 20.**

The two v2 divergences are named, not hidden: the tight spout
close-up (`true_05_spout_closeup.jpg`) is refused as
item-absent in both versions — whether a close-up counts as a
delivery photo is a scope question left open — and the
deliberately blurred true kettle passes, because the
segmentation is robust to blur and the ambiguity verdict does
not yet price degradation. The colour band in v2 was
calibrated on these same twenty photos; that is the stated
limit of the claim.

Full matrices: `docs/gate4-confusion-matrix.md` (v1) and
`docs/gate4-confusion-matrix-v2.md` (v2).
