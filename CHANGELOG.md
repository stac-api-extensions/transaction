# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [v1.0.0-rc.2] - TBD

### Added

- Add the POST /collections/{collectionsId} operation to the possible transactions (PR #4)

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

[Unreleased]: <https://github.com/radiantearth/stac-api-spec/compare/master...dev>
[v1.0.0-beta.1]: <https://github.com/radiantearth/stac-api-spec/tree/v1.0.0-beta.1>
[v1.0.0-rc.1]: <https://github.com/radiantearth/stac-api-spec/tree/v1.0.0-rc.1>
