# FolderSkin community

Community skin packs for [FolderSkin](https://github.com/prajwal-svm/folderskin), the free folder
icon changer for macOS, Windows and Linux. Every pack here appears on the app's **Community**
page, where anyone can add it to their library in one click, and new users are offered them on
first launch. The gallery on [folderskin.app](https://folderskin.app/community/) has an
**Install** button on every pack that does the same. Adding a pack needs no account: the app
reads this repository from GitHub, or the same files from its copy at `packs.folderskin.app`.

## The packs

| Pack | Skins | Licence |
|---|---:|---|
| [Everyday Folders](packs/everyday-folders) | 40 | CC0-1.0 |
| [Subjects](packs/subjects) | 20 | CC0-1.0 |
| [AI Providers](packs/ai-providers) | 20 | CC0-1.0 |
| [Hollywood](packs/hollywood) | 10 | CC0-1.0 |
| [Sound & Music](packs/sound-and-music) | 10 | CC0-1.0 |
| [Cinema & Photography](packs/cinema-and-photography) | 10 | CC0-1.0 |
| [Retro Travel Posters](packs/retro-travel-posters) | 10 | CC0-1.0 |
| [Science & Space](packs/science-and-space) | 10 | CC0-1.0 |
| [Money & Work](packs/money-and-work) | 8 | CC0-1.0 |
| [Scientists - Pop Art](packs/scientists-pop-art) | 42 | CC0-1.0 |
| [Classic Art](packs/classic-art) | 16 | CC0-1.0 |
| [Greek Art](packs/greek-art) | 15 | CC0-1.0 |
| [Soft Rainbow](packs/soft-rainbow) | 10 | CC0-1.0 |
| [Colours](packs/colours) | 8 | CC0-1.0 |

## What's in this repository

- `packs/<id>/` is one pack: a `pack.json` and the pictures it lists. The folder's name is the
  pack's id, made from its name and six random characters, such as `classic-art-k7q2mx`. Names
  can repeat, so many packs can be called Classic Art, but every id is different, and an id never
  changes.
- `moved.json` records the ids packs had before they were given generated ones, each old id with
  the id that pack has now, so links and the packs people added under an old id still find it.
- `index.json`, `previews/<id>.png` and `v2/` are what the app downloads: the list of packs, a
  strip showing each pack's first four skins as folders, and the catalog it searches. The
  [Packs workflow](.github/workflows/packs.yml) rebuilds them on `main` whenever a pack changes,
  and copies `v2/` to `packs.folderskin.app`, so never edit them by hand.

## Share a pack

Share from the app: **Community → Share your skins**, or ⋯ → **Share with community** on one
skin. The pack goes to FolderSkin's community service, and the maintainer reviews every pack
before anyone else can see it. Approving it publishes it here: the Packs workflow pulls it,
checks it and commits it, within about 15 minutes. Nobody needs a GitHub account for any of
it.

Packs also come in by hand: add a folder under `packs/` holding a `pack.json` and your pictures,
then open a pull request. Make the folder with `packs make`, which gives the pack its id; don't
pick one yourself. A check runs on the pull request, and once it's merged the pack is in
everyone's Community page within minutes. See [CONTRIBUTING.md](CONTRIBUTING.md) for the rules,
and FolderSkin's [pack guide](https://github.com/prajwal-svm/folderskin/blob/main/docs/PACKS.md)
for every field of `pack.json`.

Check a pack before you open the pull request, with FolderSkin's tools from a checkout of the app
beside this one:

```sh
cargo run --manifest-path ../folderskin/Cargo.toml -p folderskin-tools -- packs check --dir .
```

`packs make` turns a folder of pictures into a pack, and `render` shows how any picture looks as a
folder icon; the pack guide explains both.

## How approval publishes

The [Packs workflow](.github/workflows/packs.yml) does it, in one run:

1. It starts when the community service sends a `pack-approved` dispatch, which it does when it
   has a GitHub token for that. Without one, the workflow asks the service every 15 minutes
   whether any approved pack is waiting, which takes seconds, and goes on only when one is. It
   also runs every day and every week, and whenever it's started by hand.
2. `folderskin-tools community pull` writes each approved pack into `packs/`, and checks every
   file's size and SHA-256 against what the service recorded. The service gives each pack its
   generated id, and a folder that is there already is never written over.
3. `packs check` checks every pack, as it does for a pull request.
4. Each pack is committed as "Add the <name> pack" by github-actions[bot] and pushed to `main`.
5. Only then does `community done` tell the service the pack is published. A check or a push
   that fails leaves it waiting at the service for the next run, and GitHub emails the
   maintainer that the run failed.
6. The index, the previews and `v2/` are rebuilt, `v2/` is copied to the mirror, and they're
   committed.

The mirror is the Cloudflare R2 bucket behind `https://packs.folderskin.app`. The community
service writes to it, so this repository holds no Cloudflare token: `community mirror` uploads
every file the mirror doesn't have yet through the service, and `head.json` last, once every other
file is there.

The maintainer sets these once, in the repository's Actions settings:

| | what it does |
|---|---|
| secret `FOLDERSKIN_ADMIN_KEY` | the maintainer's signing key, the whole file `community keygen` wrote. Pulling packs and copying the mirror need it; without it, both are skipped with a notice |
| variable `COMMUNITY_MIRROR_URL` | `https://packs.folderskin.app`. It turns the mirror on, and `head.json` lists it |
| variable `REQUIRE_GENERATED_IDS` | `true` makes every check turn down a pack without a generated id |

## Licences

Each pack states its licence in its `pack.json`: `CC0-1.0`, `CC-BY-4.0` or `MIT`. Sharing a pack
means agreeing to FolderSkin's
[pack terms](https://github.com/prajwal-svm/folderskin/blob/main/docs/PACK-TERMS.md). Names,
logos and likenesses that appear in a skin belong to their owners; a pack's licence covers the
artwork only, not those. To ask for a pack or a skin to come down, open an issue here.
