# Quotation Manager Releases

Public distribution repository for Quotation Manager installers and OTA update metadata.

## Purpose

This repository is intentionally separate from the private application source repository. It may contain:

- Production installer releases
- Human-readable release notes
- Machine-readable OTA metadata
- SHA-256 hashes for release verification

It must not contain application source code, runtime databases, customer data, backups, credentials, or private configuration.

## OTA model

Quotation Manager uses installer-based updates rather than self-patching. The application checks public metadata, downloads the normal Windows installer over HTTPS, verifies the expected SHA-256 digest, performs a protected pre-update recovery step, then launches the installer for an in-place upgrade.

A release is not considered healthy until the upgraded application starts successfully and validates its database and supported schema. Automatic rollback is limited to this pre-validation window so that later user-created business data is never silently discarded.

## Stable feed

The stable OTA feed is `latest.json` on the `main` branch.

Current OTA baseline: **v1.0.12** (database schema **8**).

v1.0.9 is the first build containing the OTA client, so earlier builds must be upgraded to v1.0.9 using the normal installer. For every later OTA release, `latest.json` must include a verified rollback installer for each supported source version before the update is considered installable.

The production update feed must only be changed after the corresponding tested installer is uploaded as a versioned GitHub Release asset and its exact size and SHA-256 digest are verified.
