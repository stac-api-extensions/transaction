<img src="https://github.com/radiantearth/stac-site/raw/master/images/logo/stac-030-long.png" alt="stac-logo" width="700"/>

# STAC API

## About

The SpatioTemporal Asset Catalog (STAC) specification aims to standardize the way geospatial assets are exposed online and queried. 
A 'spatiotemporal asset' is any file that represents information about the earth captured in a certain space and 
time. The core STAC specification lives at [gitub.com/radiantearth/stac-spec](https://github.com/radiantearth/stac-spec).

A STAC API is the dynamic version of a SpatioTemporal Asset Catalog. It returns a STAC [Catalog](stac-spec/catalog-spec/catalog-spec.md), 
[Collection](stac-spec/collection-spec/collection-spec.md), [Item](stac-spec/item-spec/item-spec.md), 
or ItemCollection, depending on the endpoint.
Catalogs and Collections are JSON, while Items and ItemCollections are GeoJSON-compliant entities with foreign members.  
Typically, a Feature is used when returning a single Item, and FeatureCollection when multiple Items (rather than a JSON array of Item entities).

The API can be implemented in compliance with the *[OGC API - Features](http://docs.opengeospatial.org/is/17-069r3/17-069r3.html)* standard 
(formerly known as *OGC Web Feature Service 3*). In this case it can be thought of as a specialized Features API 
to search STAC Catalogs, where the features returned are STAC [Items](stac-spec/item-spec/item-spec.md), 
that have common properties, links to their assets and geometries that represent the footprints of the geospatial assets.

The specification for STAC API is provided as an [OpenAPI](http://openapis.org/) 3.0 specification in addition to human-readable documentation.

## Stability Note

This specification has evolved over the past couple years, and is used in production in a variety of deployments. It is 
currently in a 'beta' state, with no major changes anticipated. For 1.0-beta we remain fully aligned with  [OGC API - 
Features](http://docs.opengeospatial.org/is/17-069r3/17-069r3.html) Version 1.0. We have further aligned STAC extensions
with OGC API - Features extensions, particularly [CQL](https://github.com/opengeospatial/ogcapi-features/tree/master/extensions/cql/)
and [Transactions](https://github.com/opengeospatial/ogcapi-features/tree/master/extensions/transactions). These are not
yet entirely stable, so if they change then STAC will update to remain in line.

## Communication

For any questions feel free to jump on our [gitter channel](https://gitter.im/SpatioTemporal-Asset-Catalog/Lobby) or email 
our [google group](https://groups.google.com/forum/#!forum/stac-spec). The majority of communication about the evolution of 
the specification takes place in the [issue tracker](https://github.com/radiantearth/stac-api-spec/issues) and in 
[pull requests](https://github.com/radiantearth/stac-api-spec/pulls).

## In this repository

The **[Overview](OVERVIEW.md)** document describes all the various parts of the STAC API and how they fit together.

**STAC API - Core Specification:**
The main description of the core STAC API specification is in the *[core](core/)* folder and
allows browsing catalogs and retrieving the API capabilities.
An implementation will most always add extensions for broader functionality than just browsing catalogs.

**Extensions:**
In the [extensions/](extensions/) folder there are additional endpoints defined that can be added to enrich the functionality of STAC API - Core.
OpenAPI YAML documents are provided for each extension with additional documentation and examples provided in a README.

**Fragments:**
The [fragments/](fragments/) folder contains re-usable building blocks to be used in STAC API - Core and STAC API extensions.
This includes the OpenAPI schemas for items, catalogs and collections, but also common schemas and parameters for behavior like sorting and querying. Most all of them are compatible with OGC API - Features, and the plan is to fully align most of the functionality and have it be useful
for all OAFeat implementations.

**STAC Specification:** This repository includes a '[sub-module](https://git-scm.com/book/en/v2/Git-Tools-Submodules)', which
is a copy of the [STAC specification](stac-spec/) tagged at the latest stable version.
Sub-modules aren't checked out by default, so to get the directory populated
either use `git submodule update --init --recursive` if you've already cloned it,
or clone from the start with `git clone --recursive git@github.com:radiantearth/stac-api-spec.git`. 

## Contributing

Anyone building software that catalogs imagery or other geospatial assets is welcome to collaborate.
Beforehand, please review our [guidelines for contributions and development process](CONTRIBUTING.md).
