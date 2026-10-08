# triple-threat

An agent skill that reviews and fixes a change in rounds. Each round, fresh subagents review the change in parallel, one per slice:

- **Simplicity**: code and prose that can be smaller or plainer with the same behavior.
- **Correctness and design**: subtle bugs, performance, accessibility, test coverage, and design.
- **Security**: exploitable issues with a reachable attack path.

The orchestrating agent verifies each finding against the code, fixes the accepted ones at their root cause, and starts a new round with the slices those fixes could affect. The loop stops when a round produces no high- or medium-severity fix, when its fixes affect no slice, when a finding needs a decision from the user, or after four rounds. Changes stay uncommitted.

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

## Requirements

An agent that runs subagents in parallel, such as Claude Code.

## License

[MIT](LICENSE)
