# **Contributing**


## **Adding a new package**

To add a new package simply declare it in [.release-please-config.json](./release-please-config.json) as follows:

```json
{
    ...,
    "path/to/my-new-package": {
        "component": "new-pack",
        "release-type": "go",
        "initial-version": "0.1.0",
    }
}
```

There is no need to add anything to `.release-please-manifest.json` besides the initial empty config `{}` as new packages and versions will be merged in.

See the following for strategy and more config options:

- [please-release github](https://github.com/googleapis/release-please)
- [please-release-action](https://github.com/google-github-actions/release-please-action)
- [please-release manifest](https://github.com/googleapis/release-please/blob/main/docs/manifest-releaser.md)



## **Bumping versions**

The way release-please calculates release increments in a monorepo release is a function of files touched in path and [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) commit messages. \
This means that a commit message of, for instance, `fix`, `feat` or `feat!` only will lead to a new tag release if files in the package subdirectory has been altered. \
This entails that if you alter files in **/first-package** and **/second-package** a new release will be created for both packages with that conventional commit added to the changelog.

Beware that committing without files changed will cause releases for all packages in the directory:

```sh
git commit --allow-empty 'fix: this commit, with no files touched, will generate release tags for all packages'
```

## **Releasing 0.x.y as 1.0.0**

If your package is configured with `bump-minor-pre-major` and `bump-patch-for-minor-pre-major` == true, and your package is <1.0.0 then both "feat!" or "BREAKING" will only result in a minor upgrade. \
To bump your package to 1.0.0 you must alter one file within that package in the commit (git add ./mypackage/some-delta-file.txt) and commit it with two messages. The first one can be whatever; the second is important:

```sh
git commit -m "chore: release steady version of package" -m "release-as: 1.0.0"
```

Again, I stress how important it is to have one file altered inside the package so this commit doesn't affect all packages inside the monorepo.
