# Environment variables

## Environment variables used by the Whack Red SDK

- `WHACKRED_HOME` - Path to the Whack Red SDK.

## Environment variables Whack Red sets for packages

These environment variables are available for use with `env::VAR_NAME` expressions within Whack Red packages, their build scripts and unit-testing classes.

```
env::WHACKRED_MANIFEST_DIR
```

- `TARGET` - Path to the artifact target directory based on platform and build profile.
- `WHACKRED_MANIFEST_DIR` - Path to the directory containing the manifest of your package.
- `WHACKRED_MANIFEST_PATH` - Path to the manifest file of your package.
- `WHACKRED_PKG_NAME` - Package name.
- `WHACKRED_PKG_VERSION` - Package SemVer version number.
- `WHACKRED_PKG_VERSION_MAJOR` - Package major version number.
- `WHACKRED_PKG_VERSION_MINOR` - Package minor version number.
- `WHACKRED_PKG_VERSION_PATCH` - Package patch version number.

## Using static DotEnv variables

For setting static DotEnv variables for ShockScript to use, create an `.env` file in your package's directory, with contents like:

```
FOO=bar
```

You can then refer to that in ShockScript with expressions like:

```
env::FOO
```