# Pump-manager-releases

Public releases repo for Pump Manager. Holds built installers only - the
app's actual source stays in a separate private repo.

## blocked-licences.json

Whenever the app has internet, it checks this file. If a licence's key (the
`k` field printed by `tools/issue-licence.js`, e.g. `PM-XXXX-XXXX-XXXX`) is
listed under `blocked`, that install is soft-restricted: existing data stays
fully readable and exportable, but new entries are refused until the key is
removed from this list (or a fresh licence is issued).

To block a client, add their key to the array and commit:

```json
{
  "blocked": ["PM-XXXX-XXXX-XXXX"]
}
```

An install with no internet access never sees this file - it falls back to
comparing its licence's own support-until date against its own clock, which
is a much weaker check (see `docs/LICENSING_PLAN.md` in the main repo for
why that can't be made airtight offline). This file is the one that can
actually restrict someone who is deliberately staying offline to avoid it -
the moment they connect for any reason (an update check, anything), this
gets checked.
