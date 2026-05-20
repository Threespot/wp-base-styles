# @threespot/wp-base-styles

Common Sass partials used across Threespot WordPress projects.

## Install

Loaded directly from GitHub by tag — no npm registry involved.

```json
{
  "dependencies": {
    "@threespot/wp-base-styles": "github:Threespot/wp-base-styles#v0.1.0"
  }
}
```

Pin to a tag (immutable) or a semver range:

```json
"@threespot/wp-base-styles": "github:Threespot/wp-base-styles#semver:^0.1.0"
```

## Use

From a consumer's Sass entry point:

```scss
// Forward everything
@use '@threespot/wp-base-styles';

// Or pick what you need
@use '@threespot/wp-base-styles/base/fonts';

// Sass variables (Gutenberg breakpoints, admin sidebar dimensions)
@use '@threespot/wp-base-styles/vars' as *;

// Sass mixins (no-wrap, etc.)
@use '@threespot/wp-base-styles/mixins' as *;
```

## Structure

```
base/            Element defaults (fonts, etc.)
helpers/         Utility classes (no-js, etc.)
vars/            Sass variables (Gutenberg breakpoints, admin sidebar)
mixins/          Sass mixins
```

Each folder has an `_index.scss` that forwards its partials. The top-level `_index.scss` forwards `vars`, `base`, and `helpers` — `mixins/` is opt-in via explicit `@use` since mixins emit no CSS until included.

## Develop

```bash
npm install        # installs deps and sets up the pre-commit hook
npm run lint:css   # lint all .scss files
npm run lint:css:fix
```

Stylelint runs automatically on staged `.scss` files via husky + lint-staged before each commit.

## Release

Tag the commit you want consumers to be able to pin to:

```bash
git tag v0.1.0
git push --tags
```

Consumers update by bumping the tag in their `package.json` and running `npm install`.
