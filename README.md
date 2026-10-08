# triple-threat

A simple agent skill that runs critical but practical reviews and fixes in rounds. Each round, the main orchestrating agent dispatches fresh subagents to review in parallel, each one focusing on a different slice of concerns:

- **Simplicity**: code and prose that can be smaller or plainer with the same behavior.
- **Correctness and design**: subtle bugs, performance, accessibility, test coverage, and design.
- **Security**: exploitable issues with a reachable attack path.

When the subagents finish, the orchestrating agent: 
- verifies each finding they return against the code
- reasons about them as part of the larger system
- accepts practical addressable issues only
- fixes the ones it accepts at their root cause
- re-reads the skill file and invokes a new round with only the slices those fixes might affect

The review loop stops when a round produces no high- or medium-severity fixes, when its fixes affect no slice, when a finding needs a decision from the user, or after four rounds.

Note: Any changes made stay uncommitted.

## Install

```sh
npx skills add hejhi/triple-threat
```

## Usage

```text
/triple-threat              # the current branch's changes since the default branch
/triple-threat <path>       # the files under a path
/triple-threat <git-ref>    # the current branch's changes since a ref
```

Plain-language instructions after the target apply to every round, for example:

```text
/triple-threat src also run each slice through codex exec in read-only mode
```

## Requirements

An agent that runs subagents in parallel, such as Claude Code or Codex.

## License

[MIT](LICENSE)
