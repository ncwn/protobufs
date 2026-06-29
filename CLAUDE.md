# protobufs (SELFCIUS fork)

> This is a fork of `meshtastic/protobufs` on the `selfcius/main` branch.
> When merging upstream releases, consult the V4 Modifications section
> to understand which conflicts are expected vs accidental.

## Upstream Base

- **Tag:** v2.7.21-6-ge30092e
- **Commit:** e30092e6168b13341c2b7ec4be19c789ad5cd77f
- **Upstream repo:** meshtastic/protobufs
- **Fork repo:** ncwn/protobufs

## Build / Regeneration

This submodule owns protobuf source schemas. Firmware-generated nanopb C++ outputs live in the parent firmware repo under `src/mesh/generated/`.

From `meshtastic-firmware/`, regenerate firmware protobuf outputs with:

```bash
./bin/regen-protos.sh
```

The firmware regen script expects `nanopb-0.4.9/generator-bin/protoc` in the firmware root.

## Rules

- Always merge upstream, **never rebase selfcius/main**.
- Keep `origin` as `ncwn/protobufs` and `upstream` as `meshtastic/protobufs`.
- Update the V4 Modifications section below when changing protobuf schemas or generation options.
- After changing `.proto` or `.options`, regenerate the parent firmware outputs and commit the generated files with the schema change.
- Do not reuse existing Meshtastic admin fields for SELFCIUS behavior; add explicit schema when a concrete SELFCIUS requirement needs it.
- Treat protobuf changes as cross-client compatibility changes. Coordinate firmware, scripts, and future mobile/backend consumers before enabling runtime behavior.

## V4 Modifications

<!-- When you modify a file, add an entry here:

### meshtastic/file.proto
- **What:** Brief description of the change
- **Why:** Reason this modification is needed for the v4 project
- **Conflict risk:** Low / Medium / High when merging upstream
-->

### meshtastic/admin.proto
- **What:** Added `SelfciusEpoch` admin payload variant tag 68 with read/set action, origin epoch, sequence floor, and success fields.
- **Why:** SELFCIUS officer epoch provisioning needs an explicit admin schema instead of overloading unrelated Meshtastic fields.
- **Conflict risk:** Medium - shared admin schema; regenerate firmware outputs and coordinate clients before relying on runtime behavior.

### CLAUDE.md
- **What:** Added SELFCIUS fork workflow, protobuf regeneration guidance, and a V4 Modifications log for this nested submodule.
- **Why:** Future agents editing protobuf schemas need the same fork/upstream tracking and change-log discipline as the other SELFCIUS Meshtastic submodules.
- **Conflict risk:** Low - documentation-only fork guidance.
- **What:** Renamed the tracked integration branch from `v4` to `selfcius/main` for handoff clarity.
- **Why:** Future intERLab-AIT maintainers need project-specific branch names rather than the old wrapper-era `v4` label.
- **Conflict risk:** Low - branch guidance only; the old `v4` branch remains as a temporary fallback.

### New Files

<!-- Files added that don't exist in upstream -->

- `CLAUDE.md` — local agent guidance for the `ncwn/protobufs` v4 fork.
- `AGENTS.md` — symlink to `CLAUDE.md`.

### Deleted Files

<!-- Upstream files removed intentionally -->

_None yet._
