# STAC API - Transaction Extension Specification <!-- omit in toc -->

- [Overview](#overview)
- [Methods](#methods)
  - [POST](#post)
  - [PUT](#put)
  - [PATCH](#patch)
  - [DELETE](#delete)

## Overview

- **Title:** Transaction
- **OpenAPI specification:** [openapi.yaml](openapi.yaml)
- **Conformance URIs:**
  - <https://api.stacspec.org/v1.0.0/ogcapi-features/extensions/transaction>
- **Scope:** STAC API - Features
- **[Extension Maturity Classification](https://github.com/radiantearth/stac-api-spec/tree/main/README.md#maturity-classification):** Candidate
- **Dependencies**:
  - [STAC API - Features](https://github.com/radiantearth/stac-api-spec/tree/v1.0.0/ogcapi-features/README.md)
- **Owner**: none

The STAC API Transaction Extension adds support for the creation, modification, and deletion
of items through POST, PUT, PATCH, and DELETE method requests.
The behavior described here is based on the [OGC API - Features](https://ogcapi.ogc.org/features/) transactions as
specified in [OGC API - Features - Part 4: Create, Replace, Update and Delete](http://docs.opengeospatial.org/DRAFTS/20-002.html). The core
OGC standard lays out the end points for transactions, without specifying any content types. For STAC we
use STAC Item objects in our transactions, and those transaction must be done at the OGC API - Features endpoints,
under `/collections/{collectionId}/items`.

Additionaly, the STAC API Transaction Extension supports optimistic locking through use of the ETag header.

## Methods

| Path                                                   | Content-Type Header | Body                                   | Success Status | Description                                                       |
| ------------------------------------------------------ | ------------------- | -------------------------------------- | -------------- | ----------------------------------------------------------------- |
| `POST /collections/{collectionId}/items`               | `application/json`  | partial Item or partial ItemCollection | 201, 202       | Adds a new item to a collection.                                  |
| `POST /collections/{collectionId}/bulk_items`          | `application/json`  | partial ItemCollection                 | 201, 202       | Adds multiple items to a collection in a single request.          |
| `PUT /collections/{collectionId}/items/{featureId}`    | `application/json`  | partial Item                           | 200, 202, 204  | Updates an existing item by ID using a complete item description. |
| `PATCH /collections/{collectionId}/items/{featureId}`  | `application/json`  | partial Item                           | 200, 202, 204  | Updates an existing item by ID using a partial item description.  |
| `DELETE /collections/{collectionId}/items/{featureId}` | n/a                 | n/a                                    | 200, 202, 204  | Deletes an existing item by ID.                                   |

### POST

#### POST /collections/{collectionId}/items

When the body is a partial Item:

- Must only create a new resource.
- Must have an id field.
- Must return 409 if an Item exists for the same collection and id field values.
- Must populate the `collection` field in the Item from the URI.
- Must return 201 and a Location header with the URI of the newly added resource for a successful operation.
- May return the content of the newly added resource for a successful operation.

When the body is a partial ItemCollection:

- Must only create a new resource.
- Each Item in the ItemCollection must have an id field.
- Must return 409 if an Item exists for any of the same collection and id values.
- Must populate the `collection` field in each Item from the URI.
- Must return 201 without a Location header.
- May create only some of the Items in the ItemCollection. Implementations are not
  required to implement all-or-none sematics for this operation. For example, if an
  ItemCollection contains two Items and one is successfully created and the other
  fails to be created, the server is not required to then delete the successfully
  created one. When only some of the Items in the ItemCollection are created, the
  server should communicate this failure back to the client with an error status code.

All cases:

- Must return 202 if the operation is queued for asynchronous execution.

#### POST /collections/{collectionId}/bulk_items

This is an alternate version of the `POST /collections/{collectionId}/items` where the body is a partial ItemCollection. 

- Must only create new resources.
- Must accept a partial ItemCollection containing multiple Items.
- Each Item in the ItemCollection must have an id field.
- Must return 409 if an Item exists for any of the same collection and id values.
- Must populate the `collection` field in each Item from the URI.
- Must return 201 with a response body containing the status and number of items created.
- Must return 202 if the operation is queued for asynchronous execution.
- May create only some of the Items in the ItemCollection. Implementations are not required to implement all-or-none semantics.

### PUT

- Must populate the `id` and `collection` fields in the Item from the URI.
- Must return 200 or 204 for a successful operation.
- If 200 status code is returned, the server shall return the content of the updated resource for a successful operation.
- Must return 202 if the operation is queued for asynchronous execution.
- Must return 404 if no Item exists for this resource URI.
- If the `id` or `collection` fields are different from those in the URI, status code 400 shall be returned.

### PATCH

- Must populate the `id` and `collection` fields in the Item from the URI.
- Must return 200 or 204 for a successful operation.
- If status code 200 is returned, the server shall return the content of the updated resource for a successful operation.
- May return the content of the updated resource for a successful operation.
- Must return 202 if the operation is queued for asynchronous execution.
- Must return 404 if no Item exists for this resource URI.
- If the `id` or `collection` fields are different from those in the URI, status code 400 shall be returned.

PATCH is compliant with [RFC 7386](https://tools.ietf.org/html/rfc7386).

### DELETE

- Must return 200 or 204 for a successful operation.
- Must return a 202 if the operation is queued for asynchronous execution.
- May return a 404 if no Item existed prior to the delete operation. Returning a 200 or 204 is also valid in this situation.
