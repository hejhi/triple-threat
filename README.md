# triple-threat

A simple agent skill that runs critical but practical reviews and fixes in rounds. Each round, the main orchestrating agent dispatches fresh subagents to review in parallel, each one focusing on a different slice of concerns:

- **Simplicity**: code and prose that can be smaller or plainer with the same behavior.
- **Correctness and design**: subtle bugs, performance, accessibility, test coverage, and design.
- **Security**: exploitable issues with a reachable attack path.

When the subagents finish, the orchestrating agent: 
- verifies each finding they return against the code, reproducing high- and medium-severity defects and vulnerabilities with a failing test or a run against scratch data where feasible
- reasons about them as part of the larger system
- accepts practical addressable issues only
- fixes the ones it accepts at their root cause
- re-reads the skill file and invokes a new round: after a high-severity fix, a full review; otherwise, a review of the fixes by only the slices they might affect

The review loop pauses for the user's decision when a finding needs one, and stops when a round produces no high- or medium-severity fixes, when its fixes affect no slice, or after four rounds.

Note: Any changes made stay uncommitted.

## Install

```sh
npx skills add hejhi/triple-threat
```

## Usage

```text
/triple-threat              # changes since the default branch, including uncommitted files
/triple-threat <path>       # the files under a path
/triple-threat <git-ref>    # changes since a ref, including uncommitted files
```

Plain-language instructions after the target apply to every round, for example:

```text
/triple-threat src also run each slice through codex exec in read-only mode
```

## Requirements

An agent that runs subagents in parallel, such as Claude Code or Codex.

## License

[MIT](LICENSE)
