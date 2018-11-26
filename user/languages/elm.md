---
title: Building an Elm Project
layout: en

---

### What This Guide Covers

This guide covers build environment and configuration topics specific to
[Elm](https://elm-lang.org/) projects. Please make sure to read our
[Tutorial](/user/tutorial/) and
[general build configuration](/user/customizing-the-build/) guides first.

<aside markdown="block" class="ataglance">

| Elm                                         | Default                                   |
|:--------------------------------------------|:------------------------------------------|
| [Default `install`](#Dependency-Management) | `npm install`                             |
| [Default `script`](#Default-Build-Script)   | `elm-format --validate . && elm-test`     |
| [Matrix keys](#Build-Matrix)                | `elm`, `node_js`                          |
| Support                                     | [Community Support](https://travis-ci.community/c/languages/elm) |

Minimal example:

```yaml
  language: elm
  elm:
    - "0.19.0"
```

### Community-Supported Warning

Travis CI support for Elm is contributed by the community and may be removed
or altered at any time. If you run into any problems, please report them in the
[Travis CI Community Forum](https://travis-ci.community/c/languages/elm).

## Choosing Elm tool versions to test against

You can specify the Elm language version to test your project against with the
`elm` key:

```yaml
language: elm
elm:
  - elm0.19.0 # default, or equivalently, '0.19.0'
  - elm0.18.0
```
{: data-file=".travis.yml"}

This creates a separate Travis job for each Elm version.

### `elm-test` and `elm-format` versions

Elm jobs will also install `elm-test` and `elm-format`.
By default, these tools correspond to the `elm` version specified, with the
prefix `elm`.
For example, with `elm: 0.19.0`, the version of `elm-test` and `elm-format`
with the tag `elm0.19.0` will be installed.
You may also override them with `elm-test` and `elm-format` keys independently:

```yaml
language: elm
elm-test: 0.19.0-rev3
elm-format: 0.8.0
```
{: data-file=".travis.yml"}

### `elm`, `elm-test`, and `elm-format` versions

Notice that these values are passed to `npm`.
This means that they can be speicified as a version string (e.g., `0.19.0`)
or a tag (e.g., `elm0.19.0`).
`elm-test` and `elm-format` default to tags with `elm` prefix, derived from the
`elm` value.

### Choosing Node.js version to test against

Elm projects may also specify Node.js version, as done for
[Node.js](/user/languages/javascript-with-nodejs/) projects.

```yaml
language: elm
node_js: '10' # latest 10.x
```
{: data-file=".travis.yml"}

## Dependency Management

For dependency management, Elm projects use the same logic as Node.js projects.
See [Node.js documentation](/user/languages/javascript-with-nodejs/#dependency-management)
for details.

## Running Tests

The default command for testing Elm projects is:

```bash
elm-format --validate . && elm-test
```

You may override this with `script`:

```yaml
language: elm
script: elm-test
```
{: data-file=".travis.yml"}

## Environment Variables

* The version of Elm a job is using is available as `TRAVIS_ELM_VERSION`.
  This defualts to `elm0.19.0`.
* `TRAVIS_ELM_TEST_VERSION` points to the `elm-test` version in use.
  If you override `elm-test`, that value is used.
  If `elm-test` is not overridden but `elm` is, that value with the `elm`
  prefix is used. (For example, `elm: 0.18.0` chooses `elm-test@elm0.18.0`.)
  If neither `elm-test` nor `elm` is overridden, the default value, `elm0.19.0`
  is used.
* `TRAVIS_ELM_FORMAT_VERSION` points to the `elm-format` version in use.
  If you override `elm-format`, that value is used.
  If `elm-format` is not overridden but `elm` is, that value with the `elm`
  prefix is used. (For example, `elm: 0.18.0` chooses `elm-forma@elm0.18.0`.)
  If neither `elm-format` nor `elm` is overridden, the default value, `elm0.19.0`
  is used.
* `TRAVIS_NODE_VERSION` points to the `node_js` version in use.