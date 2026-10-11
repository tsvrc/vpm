# TsVRC VPM listing

The VPM listing for every TsVRC package, published at `https://vpm.tsvrc.com/index.json`. Add it to
the [VRChat Creator Companion](https://vcc.docs.vrchat.com/) once and every TsVRC package installs
from there, as described in [Install a TsVRC package](https://tsvrc.com/docs/install-a-package).

## How it works

[`build-listing.yml`](.github/workflows/build-listing.yml) builds `index.json` and the landing page
from the releases of every repository in [`source.json`](source.json), with the VRChat
[package-list-action](https://github.com/vrchat-community/package-list-action), and deploys both to
GitHub Pages. It runs when `source.json` changes, when started by hand, and when the release
workflow of a package sends a `package-released` dispatch. `Website/` holds the landing page
template. Old versions stay listed, so projects that depend on them keep working.

## Adding a package

1. Add `"tsvrc/<repository>"` to `githubRepos` in `source.json`. The repository must be public:
   the build fails when it can't read one.
2. Give the package repository a `VPM_LISTING_TOKEN` secret: a fine-grained token for `tsvrc/vpm`
   with read and write access to Contents.
3. Copy the "Update the VPM listing" step from the
   [Udon Test Kit release workflow](https://github.com/tsvrc/udon-test-kit/blob/main/.github/workflows/release.yml)
   into the release workflow of the package.

## License

Apache-2.0, see [LICENSE](LICENSE).
