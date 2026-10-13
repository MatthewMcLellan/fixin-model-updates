# fixin-model-updates

Over-the-air diagnosis model updates for the fixin iOS app. The app reads this
repo; people don't need to.

| Path | What it is |
|---|---|
| `models/fixin/catalog.json` | The engines on offer and every file each one needs, with their SHA-256s |
| `models/fixin/catalog.json.sig` | Ed25519 signature over the exact bytes of `catalog.json` |
| `models/fixin/blobs/sha256/<digest>` | Model files, each named by its SHA-256 |

The app fetches these from GitHub, then jsDelivr (a CDN copy of this repo),
then the fixin server, whichever answers first. It installs nothing unless the
catalog's signature verifies against a key built into the app, the catalog is
no older than the last one it accepted, and every file matches its SHA-256. So
it doesn't matter which host serves them.

This repo is public on purpose and holds only what the app downloads. Signing
keys and source models live elsewhere.

**Don't edit it by hand.** A hand-edited catalog fails its signature, and every
device ignores it. Publish with `Tools/publish_model_mirror.py` in the app repo.
