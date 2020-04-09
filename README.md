# buildpack-sentry-sourcemaps

This is a simple [Heroku buildpack][] used to uploads JavaScript sourcemaps
to [Sentry][], as described in [the Sentry docs][docs].

## Usage

Several environment variables are needed:

- `SOURCEMAP_DIR`: the folder (relative to the app root) where the sourcemaps can be found
- `SOURCEMAP_SENTRY_TOKEN`: an authentication token for the Sentry API. You can
  get it on the [API page][]. The token needs the `project:write` scope.
- `SOURCEMAP_SENTRY_PROJECT`: the organization and project slugs for you Sentry
  project. If your project is avaiable at `https://sentry.io/myorg/pyproject`,
  then this variable should be `myorg/myproect`.
- `SOURCEMAP_URL_PREFIX`: the prefix to prepend to each sourcemap. Can be a full
  URL (`https://example.com/dist/js/`) or a tilde-based prefix (`~/dist/js/`,
  see the [documentation][docs] for details). Make sure to include the final
  slash if it's needed.
- `SOURCEMAP_SENTRY_ORG`: the organization to search against for releases

Then add this buildpack to your app:

    heroku buildpacks:add https://github.com/Schnouki/buildpack-sentry-sourcemaps

And push a new relase.

The buildpack will use the current git commit number (environment variable
`$SOURCE_VERSION`) as the Sentry release. Make sure to add that in your app as
well!

## License

MIT.


[Heroku buildpack]: https://devcenter.heroku.com/articles/buildpacks
[Sentry]: https://sentry.io/
[docs]: https://docs.sentry.io/clients/javascript/sourcemaps/
[API page]: https://sentry.io/api/
