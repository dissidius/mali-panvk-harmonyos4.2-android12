# JimVulkan H42 Kirin 990 — v1.0.0

**Status:** Stable source release for a successfully tested Huawei P40 Pro
(Kirin 990 / Mali-G76 / HarmonyOS 4.2 / Android 12).

## Changes

- Preserved the H42 Atom72 and `KBASE_IOCTL_MEM_IMPORT_32` compatibility paths.
- Kept the proven Huawei/Kirin 990 gralloc workaround: add CPU-read usage
  when requesting Android swapchain buffers on the Kirin 990 kbase driver.
- Preserved guarded AFBC16x16 sparse handle detection.
- Removed experimental `H42DIAG`, `H42TEST`, and `H42LINEAR` logging.
- Other Mali kbase devices retain their previous no-AFBC/compositor usage
  behavior; the extra CPU-read flag is limited to Kirin 990.

## Binaries

Get the `JimVulkan-H42-Kirin990-v1.0.0-stable` artifact from the
[stable build workflow](https://github.com/dissidius/mali-panvk-harmonyos4.2-android12/actions/workflows/h42-kirin990-stable.yml)
and extract the workflow artifact to access:

- `JimVulkan-H42-Kirin990-v1.0.0-generic.zip` — standard PanVK package
  with `libvulkan_panfrost.so`.
- `JimVulkan-H42-Kirin990-v1.0.0-ARMSX2.zip` — ARMSX2 package that
  renames the same ARM64 ELF to `libvulkan_freedreno.so`.
- `SHA256SUMS.json` — package and ELF checksums, including the source commit.

Both driver ZIPs contain the **identical** PanVK ELF; only the filename and
package metadata differ. The renamed ARMSX2 ELF does not become an Adreno driver.

## Installation and validation

Import the appropriate ZIP into the emulator's custom Vulkan driver
manager; activate it; then fully close and reopen the emulator before
launching a game. Test rendering, display rotation, and performance.

The Kirin 990 workaround has been confirmed in gameplay and rotation in
ARMSX2 using the earlier experimental package. The clean stable source
should be separately validated after its build. Compatibility with other
emulators (and other phones) is not yet verified.

## Rollback

Known working experimental branch:
[`harmony42-huawei-linear-usage-ab`](https://github.com/dissidius/mali-panvk-harmonyos4.2-android12/tree/harmony42-huawei-linear-usage-ab)
at commit `15e050e3fca46ec6f17fc7bf50cf4dacf60c5f20`.

The source code and binary packages are provided as an experimental Mesa
driver port, not a Huawei-supplied GPU driver.
