# spog-updates

Public version manifest for [SPOG](https://github.com/ccromer-secops/SPOG).

SPOG checks `version.json` on launch and prompts the user to download when a
newer release exists. This repo is public only because the app reads it with no
credentials — it holds a version string and a link, nothing else. The download
link points at the private SPOG repo, so releases stay restricted to the team.

## Publishing a new version

After a SPOG release, bump `version` here to match:

```bash
gh api repos/ccromer-secops/spog-updates/contents/version.json \
  --method PUT -f message="v0.1.2" \
  -f content="$(printf '%s' '{"version":"0.1.2","url":"https://github.com/ccromer-secops/SPOG/releases/latest","notes":"..."}' | base64 -w0)" \
  -f sha="$(gh api repos/ccromer-secops/spog-updates/contents/version.json --jq .sha)"
```
