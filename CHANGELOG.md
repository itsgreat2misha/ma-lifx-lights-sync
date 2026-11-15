# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Releases are versioned by git tag and GitHub release; the provider
manifest deliberately carries no `version` field. The provider
itself remains `stage: alpha` in the manifest.

## [Unreleased]

### Changed

- The provider now calls Music Assistant's `get_setup_value`
  directly instead of guarding for servers without setup-flow
  support. No behaviour change on supported servers (2.10+):
  `get_setup_value` itself falls back to the stored config values
  for keys absent from `setup_data`.
- The manifest now declares the `aiohttp` requirement used by the
  direct Home Assistant discovery path.
- Internal tidy-up: the unicast sweep block moved out of the main
  discovery orchestration into its own method, and a dead
  `discover_targets()` helper was removed.

## [1.0.0] - 2026-11-13

First public release.

### Added

- LIFX Lights Sync plugin for Music Assistant: a Sendspin
  visualizer client that renders per-light colors and brightness
  from Music Assistant's streamed spectrum, peak and beat data and
  writes them to LIFX lights over the local LAN protocol.
- Each sync target appears as a virtual LIGHT player that can be
  joined to a Sendspin player or group: one target per Home
  Assistant area with LIFX lights, one per matrix/ceiling light
  (per-zone frames; ceiling uplight zone excluded), plus
  "Ungrouped" and LAN-only targets.
- Home Assistant-first discovery — names, areas and serials from
  the HA registries via Music Assistant's own hass provider (no
  credentials entered in this plugin) or an optional direct HA
  connection collected by a setup flow into encrypted storage —
  with LAN discovery (lifx-async) as fallback and address
  gap-filler, including a unicast subnet sweep for serials still
  missing an address.
- Five color modes: Smooth, Ambient, Flashing, Energetic (the
  Hue-analyzer presets, adapted) and a dedicated Bass mode whose
  shared brightness envelope follows only the 20–369 Hz spectrum
  bins.
- Album-artwork palette support, brightness cap and brightness
  floor settings, latency compensation, send-rate limiting (bulbs
  are capped at 20 Hz; matrix devices honour the configured rate
  up to 30 Hz), an optional debug frame log, and snapshot/restore
  of each target light's state when a stream starts and stops.
- Public-release hygiene: CI (pytest, ruff, mypy), SECURITY.md,
  CONTRIBUTING.md, issue and pull-request templates, Dependabot
  and OpenSSF Scorecard workflows.

## [0.1.0] - 2026-11-02

### Added

- Initial LIFX Lights Sync plugin for Music Assistant: a Sendspin
  visualizer client that renders per-light colors and brightness
  from Music Assistant's streamed spectrum, peak, and beat data
  and writes them to LIFX lights over the local LAN protocol.
- Each sync target appears in Music Assistant as a virtual LIGHT
  player that can be joined to a Sendspin player or group: one
  target per Home Assistant area with LIFX lights, one per
  matrix/ceiling light, plus "Ungrouped" and LAN-only targets.
- Home Assistant-first discovery (names, areas, and serials from
  the HA registries, via Music Assistant's hass provider or a
  direct HA connection), with LAN discovery via lifx-async as a
  fallback and IP gap-filler.
- Four color modes (Smooth, Ambient, Flashing, and Energetic; the
  Bass mode was added later, under `[Unreleased]` above),
  album-artwork palette support, per-light rate limiting, and
  snapshot/restore of each target light's state when a stream
  starts and stops.
