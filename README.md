# University of Bern Skin

## Set-Up

1. This repository needs to be cloned into a Monoceros ILIAS 10 to `Customizing/skin/`.
2. In ILIAS, go to `Administration > Layout and Navigation > Layout` and make the `Uni Bern / Uni Bern` skin the default. In the Delos row on this page, you can use the Action dropdown to switch all users currently using the Delos skin to `Uni Bern / Uni Bern`.

## Compiling

> [!CAUTION]
> Compiling this skin simply with `sass unibern.scss unibern.css` will fail. You need to use the load-path parameters as described below.

To compile, you need to pass two paths to the sass compiler in the following order:
* this skin's root
* the templates/default location.

This means if a `.scss` file is loaded through `@use` or `@follow` with a bare specifier (e.g. `010-settings/settings_color-palette` instead of `./010-settings/settings_color-palette`) anywhere in any files, it will be either
* taken from the skin directory if it exists
* or taken from `templates/default` if it doesn't (but with all previously replaced files being used for dependencies instead of the `templates/default` version).

SCSS only loads any file once. If it was once loaded from the skin, this version is the one being used everywhere, even in Delos files.

Let's enter the path of the skin coming from the root level and then compile from within the style folder.

```bash
cd public/Customizing/skin/munibernos/unibern/
npx sass --load-path=. --load-path=../../../../../templates/default unibern.scss unibern.css
```

## Developing

### Path Auto-Complete in JetBrain IDEs like PHPStorm

The bare specifiers that we use for paths break the path verification and auto-complete.

To make the IDE understand the paths
* go to `Settings > Directories`
* in the tree, find `templates/default`
* right click on the default folder and choose `Resource Root`
* do the same for `public/Customizing/skin/{skinname}/unibern`
* Click `Apply`

Now all paths in @use and @forward should be resolved correctly once again. When you right-click them, you can choose to go to the skin or Delos version. If there is a skin version, this is the one being used on compile.
