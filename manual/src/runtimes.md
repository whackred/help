# Runtimes

## Dependency compatibility

Dependencies of incompatible runtime are forbidden.

- The runtime `http://www.w3.org/1994/generic` is compatible with:
  - `http://www.w3.org/1994/web`
  - `http://www.nodejs.org/2009`

A package of the generic runtime can still use all APIs, like mixing `org.w3.web.*` and `org.node`, although it's necessary to use ShockScript conditional compilation with constants such as `__whack__::web` and `__whack__::node` where these APIs are used so that unnecessary and invalid bindings are not generated.