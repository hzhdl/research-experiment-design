# Experiment Framework

## Use This Reference For

- turning a vague experiment request into an academic design;
- structuring the answer as `dataset construction` plus `research question response`;
- ensuring the plan validates method effectiveness rather than merely listing runnable scripts.

## Core Principle

Design experiments to validate the method's claimed contribution, not to exhaustively exercise the codebase.

Before drafting any plan, identify:

- the method's motivation;
- the claimed improvement or capability;
- the unit of evaluation;
- the strongest evidence that would support or refute the claim.

## Part 1: Dataset Construction

Use `dataset construction` to define the data foundation required by the research questions.

Include these decisions explicitly:

1. **Source pool**
   - Define where the raw items come from.
   - Distinguish raw candidates from evaluation-ready items.

2. **Unit of evaluation**
   - Define what one example means: document, sample, contract, image, case, query, user session, benchmark task, or another atomic item.

3. **Inclusion and exclusion**
   - Define which items remain in scope.
   - Record why items are excluded instead of silently dropping them.

4. **Labels or targets**
   - Define what counts as a label, gold answer, candidate signal, or downstream verification target.
   - Distinguish noisy upstream labels from the final evaluation target when they are different.

5. **Preprocessing**
   - Define normalization, deduplication, filtering, compilation checks, schema checks, or environment checks.

6. **Split policy**
   - Define train, validation, test, or paired subsets only if they are needed by the method claim.
   - Add leakage controls such as family-disjoint, time-disjoint, entity-disjoint, or source-disjoint splits when transfer or generalization matters.

7. **Artifact outputs**
   - Define which manifests, sample lists, audit files, or derived datasets must be written to make the experiment reproducible.

Write dataset construction so that another researcher can rebuild the evaluation set without guessing hidden filtering logic.

## Part 2: Research Question Response

Use `research question response` to define a small number of high-value research questions. Do not turn every subsystem into a separate RQ.

Each research question should include:

- the question itself;
- why it matters to the method claim;
- the comparison or intervention;
- the exact experiment protocol;
- the primary metrics;
- the statistical test or decision rule;
- the interpretation criterion.

## Default Research Question Families

Use only the families that match the method's claim.

### RQ1: Overall Effectiveness

Ask whether the method improves the primary task outcome compared with the most relevant baselines or controls.

Typical evidence:

- success rate;
- confirmed rate;
- accuracy, F1, recall, AUROC;
- human preference;
- task completion rate.

### RQ2: Efficiency or Cost

Ask whether the method reduces effort, search cost, latency, token use, memory use, number of attempts, or another operational burden.

Typical evidence:

- runtime;
- number of actions, plans, or steps;
- resource consumption;
- intervention count.

### RQ3: Mechanism, Ablation, or Causal Contribution

Ask whether the proposed component is actually responsible for the gain.

Typical evidence:

- with-component vs without-component comparison;
- ablations;
- causal trace or reuse analysis;
- component-specific hit rates.

### RQ4: Generalization, Transfer, or Robustness

Ask whether the method still works across new domains, tasks, families, environments, or perturbations.

Typical evidence:

- cross-domain transfer;
- cross-family evaluation;
- robustness under changed settings;
- failure-category breakdown.

### RQ5: Continual Learning or Online Adaptation

Use only when the method claims online improvement, feedback-driven updating, or memory accumulation.

Typical evidence:

- cumulative gain curves;
- later-sample improvements;
- sequential evaluation under multiple orderings.

## Statistical Defaults

Prefer simple, defensible tests that match the design:

- McNemar exact test for paired binary outcomes;
- Wilcoxon signed-rank for paired non-normal cost metrics;
- bootstrap confidence intervals for rate deltas;
- descriptive statistics only when the sample is too small for stronger claims.

If the data volume is small or the setup is exploratory, say so explicitly and weaken the claim.

## Main-Paper vs Appendix Boundary

Put an experiment in the main paper only if it directly supports the central method claim.

Move these to appendix or case-study scope when needed:

- sparse classes or domains;
- unsupported baselines;
- anecdotal debugging runs;
- highly manual case analyses;
- speculative future experiments.

## Common Failure Modes

- defining research questions around implementation modules rather than scientific claims;
- skipping dataset construction and jumping straight to metrics;
- using upstream labels as final truth without qualification;
- omitting leakage controls in transfer claims;
- proposing baselines that the project cannot actually run;
- listing metrics without saying how success will be judged;
- treating manual smoke tests as sufficient evidence of effectiveness.
