# Repository Grounding

## Use This Reference For

- converting a local repository into a feasible experiment plan;
- deciding which files to inspect first;
- deriving manual test commands from current code paths;
- avoiding plans that depend on missing infrastructure.

## First Inspection Pass

Before drafting the plan, inspect the local project for:

1. research-plan files such as `*plan*.md`, `*research*.md`, `*experiment*.md`, `docs/`, or manuscript drafts;
2. configuration files that define the default runtime path;
3. dataset loaders, schema definitions, or manifest builders;
4. benchmark, evaluation, or split-generation scripts;
5. CLI entrypoints, wrappers, and task runners;
6. tests that reveal supported modes, expected outputs, and edge cases.

If the project already has benchmark or report generators, treat them as the source of truth for what can be measured today.

## Questions To Answer From Code

Answer these questions from the repository before finalizing the plan:

- What is the real evaluation entrypoint?
- Which baselines or modes are actually implemented?
- What data items are loader-visible after filtering?
- Which metrics are already emitted by the code?
- Which results are persisted to disk, and where?
- Which manual test paths already exist?
- Which claims in the docs are not backed by current artifacts?

## Command-Derivation Pattern

When the user asks for manual testing commands, derive them from the current CLI and wrappers.

Try to provide:

1. an inspection or candidate-discovery command;
2. a main experiment or verification command;
3. a control command that disables the studied component or uses a baseline mode;
4. an artifact inspection command if the tool writes results to disk.

Keep commands minimal and explicit. Add flags that remove ambiguity, especially when defaults could read the wrong dataset, model, or memory store.

## Grounding Rules

- Prefer explicit flags over implicit defaults in all reproducibility-sensitive commands.
- Prefer isolated outputs, fresh caches, or fresh memory stores when the method depends on historical state.
- Prefer repository-native artifact files over narrative notes when reporting completed experiments.
- Treat missing output directories as absent evidence, even if a document claims they once existed.

## Planning Rules Derived From Code

When the codebase exposes a measurement directly, reuse that measurement in the experiment plan.

When the codebase does not expose a requested measurement:

- either propose it as future implementation work;
- or replace it with the closest supported measurement;
- never pretend it already exists.

When a component has different operational modes, design experiments that isolate them cleanly:

- main method vs no-component control;
- readonly history vs online writeback;
- paired benchmark vs unpaired batch evaluation;
- automatic discovery vs explicit target mode.

## Common Failure Modes

- reading a design note and assuming the current repo still matches it;
- ignoring default-state hazards such as stale caches, shared memories, or default libraries;
- forgetting to run the control condition;
- proposing commands that mix training and test writes into the same stateful store;
- deriving evaluation claims from logs that are not part of a reproducible artifact path.
