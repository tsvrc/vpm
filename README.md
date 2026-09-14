# TsVRC VPM listing

The VRChat Package Manager (VPM) listing for every package under the `tsvrc` org.
Add it to the [VRChat Creator Companion](https://vcc.docs.vrchat.com/) once, and every
current and future TsVRC package becomes installable from it.

## Add this listing to VCC

- **With VCC installed**: [Add TsVRC's listing to Creator
  Companion](vcc://vpm/addRepo?url=https%3A%2F%2Fvpm.tsvrc.com%2Findex.json)
- **Or paste manually**: in VCC, go to **Settings > Packages > Add Repository** and
  paste `https://vpm.tsvrc.com/index.json`.

## What's in this repo

- `source.json`: lists which package repos feed this listing (`githubRepos`) and the
  listing's own metadata (name, author, banner).
- `Website/`: the landing page template. Rendered at build time with each package's
  metadata, not something to edit by hand except for swapping the banner image.
- `.github/workflows/build-listing.yml`: builds `index.json` and the landing page from
  the latest GitHub Release of every repo in `source.json`, deploys both to this repo's
  GitHub Pages. Runs on a push to `source.json`, a manual trigger, or a
  `repository_dispatch` sent by a package repo's own release workflow right after it
  publishes a new release.

## Adding a new TsVRC package to this listing

1. Add `"tsvrc/<repo-name>"` to `source.json`'s `githubRepos` array, open a PR.
2. In the new package's own repo, add a fine-grained GitHub PAT scoped only to this
   repo (`tsvrc/vpm`) with **Contents: Read and write** permission, stored as a repo
   secret (e.g. `VPM_LISTING_TOKEN`).
3. Add a step to that repo's release workflow, after it creates the GitHub Release:

   ```yaml
   - name: Notify VPM listing
     run: |
       curl -sf -X POST \
         -H "Authorization: Bearer ${{ secrets.VPM_LISTING_TOKEN }}" \
         -H "Accept: application/vnd.github+json" \
         https://api.github.com/repos/tsvrc/vpm/dispatches \
         -d '{"event_type":"package-released"}'
   ```

That's it, no changes needed here beyond the `source.json` line. This repo never
removes old package versions once published (per VPM's own convention), since projects
still depending on an older version would break otherwise.

## License

Apache-2.0, see [LICENSE](LICENSE). This is a config/tooling repo, not TsVRC's own
package code (that's in [tsvrc/tsvrc-core](https://github.com/tsvrc/tsvrc-core)) or its
documentation (that's in [tsvrc/docs](https://github.com/tsvrc/docs)).
