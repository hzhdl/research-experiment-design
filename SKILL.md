---
name: research-experiment-design
description: Design academically rigorous experiment plans for research projects that have method claims, datasets, code, benchmarks, or manual test flows. Use when asked to structure experiments into dataset construction and research-question sections, align research questions with the paper motivation, choose baselines, metrics, and statistical tests, map repository code to feasible evaluation, or derive reproducible manual test commands from local scripts and CLIs.
---

# Research Experiment Design

## Workflow

1. Ground the plan in the actual repository, paper draft, or research notes before proposing any experiment.
2. Extract the method's motivation, claimed contribution, and intended evidence target.
3. Split the plan into `dataset construction` and `research question response` unless the user explicitly asks for another structure.
4. Build a small set of falsifiable research questions that directly test the method's claimed value.
5. Reuse metrics, outputs, and evaluation paths that the project can already generate when possible.
6. State leakage controls, validity checks, artifact requirements, and statistical tests explicitly.
7. Distinguish supported experiments from implementation gaps instead of silently inventing missing infrastructure.
8. When asked for manual testing, derive commands from the current codebase, not from an abstract workflow.

## Read First

Read these references before drafting a plan:

- [references/experiment-framework.md](references/experiment-framework.md)
- [references/repo-grounding.md](references/repo-grounding.md)

Use them to choose the structure, decide which local files to inspect, and convert repository reality into an academically defensible experiment design.

## Planning Rules

- Tie every research question to a motivation, threat, or claimed contribution in the research materials.
- Phrase every research question as a concrete question that can be falsified by an experiment.
- Separate `main-paper evidence` from `appendix or case-study evidence`.
- Prefer paired comparisons when the same items can be evaluated under multiple modes or conditions.
- Prefer fresh evaluation artifacts and isolated data splits over historical notes or ad hoc examples.
- Prefer repository-native metrics over newly invented terminology when the project already exposes meaningful evaluation outputs.
- Flag unsupported baselines, missing datasets, or absent artifact paths as constraints.

## Output Requirements

When writing an experiment plan, include:

- the research objective in one sentence;
- the dataset construction policy;
- the research questions and corresponding experiment designs;
- the baselines, metrics, and statistical tests;
- the artifact, leakage-control, and validity requirements;
- the main risks, assumptions, and scope limits.

When writing manual testing commands, include:

- a command to inspect or discover the target under test;
- a command for the main method flow;
- a control command or comparison command;
- any artifact-check or audit command only if it materially improves confidence.
