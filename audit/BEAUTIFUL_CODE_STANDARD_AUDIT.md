# DubboSDR — Beautiful Code Standard Audit

**Audit date:** 17 September 2026  
**Repository tier:** Active / hardware-integrated desktop app  
**Standard:** The Beautiful Code Standard

## Overall finding

DubboSDR has a clear .NET/WPF service/view structure, explicit architecture/testing docs, third-party notices and separate radio/streaming abstractions. That is a sensible shape for hardware-dependent software. The main missing evidence is visible automated CI and tests around the hardware boundary.

The committed `dotnet-install.ps1` is a large third-party bootstrap script; prefer a documented/pinned official install path or make its provenance/update policy explicit rather than maintaining vendor code casually.

## Priorities

1. Add CI for restore/build/tests on supported Windows/.NET versions.
2. Put SDR/hardware access behind testable interfaces and add fake-device tests for tuning, device loss, stream errors and reconnect behaviour.
3. Add a smoke/integration test for the non-hardware path (internet audio or fake source) so the full UI/audio pipeline can be exercised automatically.
4. Ensure remote streaming failure states are explicit and do not silently continue with stale device/status information.
5. Validate `stations.json` as canonical structured data.
6. Review whether vendoring `dotnet-install.ps1` is necessary; avoid maintaining copied installer logic without provenance.

## Bottom line

**The module boundaries are good. The next step is reproducible Windows CI and honest testing around the inherently unreliable hardware boundary.**
