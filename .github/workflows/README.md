# GitHub Actions workflows

<!-- workflow-operations-reference:start -->

<!-- TODO Reviewed ??-??-2026. -->

## Workflow operations reference

The workflow YAML files own execution behavior. Their inline comments explain the purpose and
the boundaries that must survive future refactoring. This reference records the current job map;
repository-level Actions enable/disable settings remain independent of these tracked definitions.

### Changes in this review

- main.yaml: Added branch-scoped concurrency with obsolete-run cancellation.
- rust-msrv.yml: Added branch-scoped concurrency with obsolete-run cancellation.
- rust-msrv.yml: Bound msrv to 120 minutes.

### [Rust GitHub Action test workflow](main.yaml)

Events: `push, workflow_dispatch`. Branch/path filters and manual defaults are defined in the linked file.

| Job      | Runs on / reuse | Dependencies | Guard                             | Main checks or side effects                                                                              |
| -------- | --------------- | ------------ | --------------------------------- | -------------------------------------------------------------------------------------------------------- |
| test_job | "ubuntu-latest" | []           | Successful dependencies (default) | Check out the test application; Build the application image archive; Validate and run the exported image |

### [Rust minimum version](rust-msrv.yml)

Events: `pull_request, push, workflow_dispatch`. Branch/path filters and manual defaults are defined in the linked file.

| Job  | Runs on / reuse | Dependencies | Guard                             | Main checks or side effects                                                                                           |
| ---- | --------------- | ------------ | --------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| msrv | "ubuntu-latest" | []           | Successful dependencies (default) | actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1; rustup toolchain install 1.98.1 --profile minimal; Check . |

### Caches, permissions and failures

- Keep package downloads and compiler outputs separate. Match cache keys to compiler, OS, dependency locks, build profiles and features; a cache is an optimization, not a prerequisite for correctness.
- Matrix jobs start on separate machines. Build/test commands in one job reuse local outputs; moving them to separate jobs requires an explicit compatible artifact handoff.
- Read-only validation and live publication have different lifecycles. Preserve existing credentials, event/ref conditions, environments and non-cancelling deployment groups.
- Timeouts bound hung or unexpectedly expensive runs. Diagnose a timeout before increasing it; never convert a failed check into an unconditional success.
- A queued/disabled/billing-blocked run is not a passed check. Record hosted results separately from local workflow parsing/format validation.

### Local validation

```sh
actionlint
git diff --check
```

Use the repository formatter for edited YAML/Markdown. Run the commands named by the affected
jobs when their executable behavior changes; platform/container/credential-dependent checks
must be reported at the scope actually executed. Do not run publishing commands merely to test
a comment or validation-only change.

<!-- workflow-operations-reference:end -->
