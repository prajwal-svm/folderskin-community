# FolderSkin community

Community skin packs for [FolderSkin](https://github.com/prajwal-svm/folderskin), the free folder
icon changer for macOS, Windows and Linux. Every pack here appears on the app's **Community**
page, where anyone can add it to their library in one click, and new users are offered them on
first launch. No account, no server: the app reads this repository straight from GitHub.

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
  pack's id.
- `index.json`, `previews/<id>.png` and `v2/` are what the app downloads: the list of packs, a
  strip showing each pack's first four skins as folders, and the catalog it searches. The
  [Packs workflow](.github/workflows/packs.yml) rebuilds them on `main` whenever a pack changes,
  so never edit them by hand.

## Share a pack

The easy way is from the app: save your skins as a pack and choose **Share on GitHub**. FolderSkin
forks this repository and opens the pull request for you.

By hand: add a folder `packs/<your-pack-id>/` holding a `pack.json` and your pictures, then open
a pull request. A check runs on it, and once it's merged the pack is in everyone's Community
page within minutes. See [CONTRIBUTING.md](CONTRIBUTING.md) for the rules, and FolderSkin's
[pack guide](https://github.com/prajwal-svm/folderskin/blob/main/docs/PACKS.md) for every field
of `pack.json`.

Check a pack before you open the pull request, with FolderSkin's tools from a checkout of the app
beside this one:

```sh
cargo run --manifest-path ../folderskin/Cargo.toml -p folderskin-tools -- packs check --dir .
```

`packs make` turns a folder of pictures into a pack, and `render` shows how any picture looks as a
folder icon; the pack guide explains both.

## Licences

Each pack states its licence in its `pack.json`: `CC0-1.0`, `CC-BY-4.0` or `MIT`. Sharing a pack
means agreeing to FolderSkin's
[pack terms](https://github.com/prajwal-svm/folderskin/blob/main/docs/PACK-TERMS.md). Names,
logos and likenesses that appear in a skin belong to their owners; a pack's licence covers the
artwork, not those. To ask for a pack or a skin to come down, open an issue here.
