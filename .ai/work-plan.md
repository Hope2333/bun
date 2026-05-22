# android-termux Work Plan

**Repository**: https://github.com/Hope2333/bun
**Branch**: `android-termux`
**Base**: upstream `main` (dcc04348)
**Last Update**: 2026-05-22

---

## Current Status

| Area | Status | Details |
|------|--------|---------|
| Fork | ✅ | Hope2333/bun created |
| android-termux branch | ✅ | Based on upstream main, not tag |
| CWD /data/ scan fix | ✅ | Committed (767462f) |
| `--target=bun-linux-android` | ⏳ | CompileTarget.zig already supports android libc |
| Build Android binary | ⛔ | Blocked: requires Buildkite CI (WebKit/JSC) |
| Test on Termux | ⏳ | Pending built binary |

---

## Task Queue

### Phase 1: Foundation (DONE)
- [x] Fork oven-sh/bun
- [x] Create android-termux branch from upstream main
- [x] Patch: CWD fallback on `/data/` permission denied
- [x] Push to remote

### Phase 2: Compile Target (NEXT)
- [ ] Verify `--target=bun-linux-arm64-android` works in CompileTarget.zig
- [ ] Test: `bun build --compile --target=bun-linux-arm64-android` on Linux
- [ ] If target missing → add the target string mapping
- [ ] Verify the output binary has compiled-app entry point

### Phase 3: Build Pipeline (BLOCKED)
- [ ] Set up GitHub Actions workflow for Linux → Android cross-compile
- [ ] Or: adapt upstream Buildkite pipeline for forks
- [ ] Or: build natively on Linux and use QEMU for Android linking
- [ ] Produce working `bun-linux-aarch64-android` binary with patches

### Phase 4: OpenCode Compilation
- [ ] Clone opencode source on CI
- [ ] Build with patched Bun: `bun build --compile --target=bun-linux-arm64-android`
- [ ] Test output on Termux
- [ ] Compare: does wrapped (bun-termux-loader) version work differently?

### Phase 5: Upstream
- [ ] Clean up patches for upstream PR
- [ ] Submit CWD fix to oven-sh/bun
- [ ] Submit Android compile target (if added)

---

## Blockers

| Blocker | Impact | Workaround |
|---------|--------|------------|
| Bun Android build requires Buildkite | Can't produce patched binary | Use bun-termux-loader + glibc as current production path |
| WebKit/JSC Android cross-compile | Complex toolchain setup | Wait for upstream to release next Android Bun |

## Dependencies

- Upstream Bun next release (for Android binary with potential fixes)
- Or: Android NDK + WebKit source for self-build

## Completion Criteria

android-termux branch is "done" when:
- [ ] `bun build --compile --target=bun-linux-arm64-android hello.ts` produces a working binary
- [ ] The binary runs on Termux without glibc
- [ ] OpenCode can be compiled with this target
