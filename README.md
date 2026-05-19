# @threespot/wp-base-styles

Sass partials for default WordPress blocks and common styles used across Threespot WP projects.

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
@use '@threespot/wp-base-styles/default-blocks';
@use '@threespot/wp-base-styles/helpers/no-wrap';

// Sass variables (Gutenberg breakpoints, admin sidebar dimensions)
@use '@threespot/wp-base-styles/vars' as *;
```

## Structure

```
base/            Element defaults (fonts, etc.)
default-blocks/  Default WP core block styles
helpers/         Reusable helper classes
vars/            Sass variables (Gutenberg breakpoints, admin sidebar)
```

Each folder has an `_index.scss` that forwards its partials. The top-level `_index.scss` forwards `base`, `default-blocks`, and `helpers` — `vars/` is opt-in via explicit `@use` since it outputs no CSS.

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
