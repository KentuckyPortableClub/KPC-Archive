# KPC-Archive as the store (Nov 9 2026)

Brandon (Nov 9, 4:33-4:59 PM CST): saved outlines and saved 2-fer answers are kept here. Brandon t923u (4:59 PM CST): **outline
geometry is never committed to git** (no history growth); it lives only as compressed **release assets** on this repo, and a refresh
REPLACES the asset. Git here keeps only small index files.

| Where | What | Written by | Size today |
|---|---|---|---|
| release `saved-outlines`: `US-XX.json.gz`, `CA-ALL.json.gz` | the US / Canada keys' saved park outlines (every record id they read) | KPC-Links `kpc-us-key.yml`, `kpc-boundary-check.yml` (two states a night = each state about once a month), `kpc-ca-key.yml` (monthly live read) | US 70.8 MB (largest US-AK 7.7 MB) + CA 6.2 MB = 77 MB |
| release `fers-saved-live`: `saved-live-<area>.json.gz` | outlines the 2-fer bot had to read live (no key copy); re-read about once a month, a quarter per run | KPC-Data `kpc-fers.yml` | new, small |
| git `index/saved-outlines.json` | per file: bytes, sha256, date, run | the same workflows | a few KB |
| git `index/fers-saved-live.json` | per file as above + per park: record ids, outline fingerprint, date | KPC-Data `kpc-fers.yml` | under 1 MB at full size (about 1,300 parks) |

The saved 2-fer answers (per pair: fingerprint + the spots found) stay in KPC-Data `data/fers/reuse-p*-<area>.json` as before
(git; a file over 20 MB is gzipped by the Save step). Git size of this repo is untouched by outlines; the 500 MB cap of
`kpc_archive_move.py` counts git only.

Not moved: the world outlines (305.6 MB; W-DE 105.4 MB) stay on the KPC-Links `boundary-cache` release. The KPC-Links
`boundary-cache` release also keeps getting the US/CA files for now (about 15 workflows still read it); move those readers to
`kpc_archive.sh get` and then stop the mirror.

**Access from GitHub Actions:** secret `KPC_ARCHIVE_TOKEN` in KPC-Links and KPC-Data (added by Brandon Nov 9, 4:59 PM CST):
a fine-grained token, owner KentuckyPortableClub, repository access KPC-Archive only, permission **Contents: Read and write**
(release upload/replace + the index commit; Metadata: Read comes with it). If it is missing or cannot write, every workflow prints
a warning and uses the KPC-Links release copy; nothing fails.
