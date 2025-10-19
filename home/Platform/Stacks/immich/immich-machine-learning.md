<!--
title: immich-machine-learning
description:
published: true
date: 2025-10-19T08:57:42Z
tags:
editor: markdown
-->

# immich-machine-learning

## Overview
Handles ML inference for facial recognition, image classification, and other enrichment tasks. It pulls the same Immich version tag as the main server and caches downloaded models under the `model-cache` volume.【F:immich_base/compose.yml†L33-L56】

## Runtime Profile
- **Image:** `ghcr.io/immich-app/immich-machine-learning:${IMMICH_VERSION:-release}`
- **Networks:** `backend_net`
- **Volumes:** `model-cache:/cache`
- **Devices:** `/dev/dri` for hardware acceleration
- **Restart policy:** `always`
- **Healthcheck:** Enabled but uses default Immich behavior

## Integrations & Operations
- Ensure GPU drivers on the host support the chosen ML backend; configure `hwaccel.ml.yml` if you need CUDA, ROCm, or other acceleration profiles.
- Shares Redis and Postgres connectivity indirectly through the server; keep version parity to avoid gRPC schema mismatches.
- Back up the `model-cache` to avoid re-downloading large ML assets after rebuilds.
