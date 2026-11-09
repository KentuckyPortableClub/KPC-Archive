# KPC-Archive as the store (Nov 9 2026)

Brandon (Nov 9, 4:33-4:52 PM CST): saved outlines, saved 2-fer answers and source files live here, not only on release assets.

| Folder | What | Written by | Size today |
|---|---|---|---|
| `outlines/US-XX.json.gz` | the US key's saved park outlines, one file per state (every record id it read: PAD-US, state layers, FWS) | KPC-Links `kpc-us-key.yml`, `kpc-boundary-check.yml` (nightly re-read, two states a night = each state about once a month) | 70.8 MB, largest US-AK 7.7 MB |
| `outlines/CA-ALL.json.gz` | the Canada key's saved outlines | KPC-Links `kpc-ca-key.yml` (re-read live on the monthly run) | 6.2 MB |
| `fers/saved-live-<area>.json.gz` | outlines the 2-fer bot had to read live (no saved copy above), re-read about once a month, a quarter per run | KPC-Data `kpc-fers.yml` | new (small) |

Every change is a git commit, so the old copy is always in the history (no `prev-` files needed here).

**Too big for git** (GitHub refuses a file over 100 MB; `kpc_archive.sh` stops at 95 MB): stays a release asset on KPC-Links
`boundary-cache`. Today that is the world key's `W-DE.json.gz` (105.4 MB). World outlines (305.6 MB, W-FR 61.8 MB) are not moved yet.

**Mirror:** the KPC-Links `boundary-cache` release keeps getting the same US/CA files for now, because about 15 workflows in KPC-Links
and KPC-Data still read it. Move the readers to `kpc_archive.sh get` and then stop the mirror (a later, separate change).

**Access from GitHub Actions:** secret `KPC_ARCHIVE_TOKEN` in KPC-Links and KPC-Data (or one organization secret for both):
a fine-grained token, owner KentuckyPortableClub, repository access only KPC-Archive, permission Contents: Read and write
(Metadata: Read comes with it). Without it every workflow prints a warning and uses the release copy; nothing fails.
