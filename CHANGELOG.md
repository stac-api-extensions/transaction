# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Support for [RFC 6902](https://tools.ietf.org/html/rfc6902) [#14](https://github.com/stac-api-extensions/transaction/pull/14)

### Changed

- Updated of [RFC 7386](https://tools.ietf.org/html/rfc7386) to [RFC 7396](https://tools.ietf.org/html/rfc7396) [#14](https://github.com/stac-api-extensions/transaction/pull/14)

## [v1.0.0-rc.3] - 2023-09-28

- Remove assertion that this will align with OAF Part 4.
- OAFeat Part 4 Conformance URI should no longer be advertised.

## [v1.0.0-rc.2] - 2022-11-01

- Minor wordsmithing updates.

## [v1.0.0-rc.1] - 2022-03-17

### Changed

- Clarified behavior of Transaction Extension endpoints:
  - PUT and PATCH of a body that changes the `collection` or `id` is disallowed.
  - POST, PUT, and PATCH do not need to include the `collection` attribute, as it should be derived from the URL.
  - POST and PUT can be used with a body that is at least a GeoJSON Feature, but does not have to be an Item, but for which 
    the server can derive a valid Item, e.g., by populating the id and collection fields or adding links
  - Likewise, POST can be used with a body of a FeatureCollection that contains features that meet the same constraints.

## [v1.0.0-beta.1] - 2020-12-10

### Changed

- Updated transaction extension so it aligns with OGC API - Features Part 4: Simple Transactions

## Older versions

See the [stac-spec CHANGELOG](https://github.com/radiantearth/stac-spec/blob/v0.9.0/CHANGELOG.md)
for STAC API releases prior to or equal to version 0.9.0.

[Unreleased]: <https://github.com/stac-api-extensions/transaction/compare/v1.0.0-rc.3...main>
[v1.0.0-rc.3]: <https://github.com/stac-api-extensions/transaction/tree/v1.0.0-rc.3>
[v1.0.0-rc.2]: <https://github.com/stac-api-extensions/transaction/tree/v1.0.0-rc.2>
[v1.0.0-rc.1]: <https://github.com/radiantearth/stac-api-spec/tree/v1.0.0-rc.1>
[v1.0.0-beta.1]: <https://github.com/radiantearth/stac-api-spec/tree/v1.0.0-beta.1>
