# android-termux Roadmap

## Phase 1: Foundation ✅
- Fork Bun, create branch, apply CWD fix

## Phase 2: Compile Target
- Verify `--target=bun-linux-arm64-android` works
- Test output for compiled-app entry point
- Fix any remaining issues

## Phase 3: Build Pipeline
- Set up CI or use upstream Buildkite
- Produce Android binary with patches

## Phase 4: OpenCode Integration
- Compile OpenCode with patched Bun
- Test on Termux

## Phase 5: Upstream
- Submit CWD fix PR to oven-sh/bun
- Submit compile target improvements
