# schemas — the protocol's message shapes

- `claim.schema.json` — a claim: what the tenant asserts and
  what the instrument measured are different fields, by
  construction. A claim cannot carry its own measurement.
- `receipt.schema.json` — a receipt: the verdict, its named
  reason, the measurement it rests on, and the hash links
  that chain it to the receipts before it.

These are the shapes the code in `src/runway/` emits and the
replay checks. If the code and a schema disagree, the schema
is the protocol and the code is the bug.
