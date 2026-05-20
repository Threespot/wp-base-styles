# @threespot/wp-base-styles

Common Sass partials and stylesheets used across Threespot WordPress projects.

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

The package ships four standalone entry points, each meant to be compiled into a stylesheet enqueued in a different WP context:

| Entry point          | Where it's enqueued                                |
| -------------------- | -------------------------------------------------- |
| `main.scss`          | Front-end (vars + base + helpers)                  |
| `gutenberg.scss`     | Block editor                                       |
| `admin-all.scss`     | All admin pages                                    |
| `admin-fields.scss`  | Admin pages with editable fields (ACF, TinyMCE)    |

From a consumer's Sass entry point:

```scss
// Front-end bundle
@use '@threespot/wp-base-styles/main';

// Or compile any of the context-specific entry points directly
@use '@threespot/wp-base-styles/gutenberg';
@use '@threespot/wp-base-styles/admin-all';
@use '@threespot/wp-base-styles/admin-fields';

// Pick individual partials
@use '@threespot/wp-base-styles/base/fonts';

// Sass variables (Gutenberg breakpoints, admin sidebar dimensions)
@use '@threespot/wp-base-styles/vars' as *;

// Sass mixins (no-wrap, etc.)
@use '@threespot/wp-base-styles/mixins' as *;
```

## Structure

```
main.scss            Front-end entry point (forwards vars, base, helpers)
gutenberg.scss       Block editor entry point
admin-all.scss       Admin-wide entry point
admin-fields.scss    Editable-fields admin entry point

base/                Element defaults (admin-bar, fonts)
helpers/             Utility classes (javascript-helpers, what-input)
vars/                Sass variables (Gutenberg breakpoints, admin sidebar)
mixins/              Sass mixins
```

Each folder has an `_index.scss` that forwards its partials. `main.scss` forwards `vars`, `base`, and `helpers` — `mixins/` is opt-in via explicit `@use` since mixins emit no CSS until included.

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
