# Contributing a pack

Thanks for sharing your skins. A pack is a folder under `packs/` with a `pack.json` and the
pictures it lists; the pull request that adds it is checked with the same rules the app uses
before it saves a pack.

## The rules

- **Your own pictures.** Only pictures you made, or are allowed to share, under `CC0-1.0`,
  `CC-BY-4.0` or `MIT`. No art taken from another product, stock photos, wallpapers or anything
  whose terms you haven't checked.
- **1 to 50 skins** a pack. Split a bigger set into themed packs.
- **Pictures** are PNG, JPEG or WebP, 256 to 1024 px on each side and at most 2 MB each. Keep
  them near 400 KB: everyone who adds the pack downloads all of it. `packs make` does this for
  you.
- **The id** is the folder's name: lower-case words joined by dashes, at most 40 characters,
  such as `night-prints`. **The name** is 1 to 40 characters; **tags** are 1 to 5, lower case,
  and the first one names the pack in everyone's filters.
- **Skin names** are 1 to 60 characters. Name people from what the picture says (a caption,
  lettering), never from their face.
- Never edit `index.json`, `previews/` or `v2/`. The workflow rebuilds them after the merge.

The full contract is FolderSkin's
[pack guide](https://github.com/prajwal-svm/folderskin/blob/main/docs/PACKS.md), and sharing a
pack means agreeing to the
[pack terms](https://github.com/prajwal-svm/folderskin/blob/main/docs/PACK-TERMS.md).

## Making and checking a pack

With [FolderSkin](https://github.com/prajwal-svm/folderskin) checked out beside this repository:

```sh
# Turn a folder of pictures into packs/<id>/ (finished folders on magenta or transparency are cut out)
cargo run --manifest-path ../folderskin/Cargo.toml -p folderskin-tools -- \
  packs make ~/Pictures/my-skins --dir . --id my-skins --name "My Skins" --tags art \
  --author <your-github-name> --preview /tmp/my-skins.png

# Check every pack the way the app and this repository's workflow do
cargo run --manifest-path ../folderskin/Cargo.toml -p folderskin-tools -- packs check --dir .
```

Open the `--preview` sheet before you send the pull request: it draws every skin as the folder
the app makes of it.
