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

## Current state

The repository is initialized for OTA work. No update is published merely by adding this README. A production update feed should only be changed when the corresponding tested installer and exact SHA-256 digest are available.
