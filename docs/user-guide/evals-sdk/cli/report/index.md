`strands-evals report` renders an `EvaluationReport` JSON that a previous [`run`](/docs/user-guide/evals-sdk/cli/run/index.md) produced, and `strands-evals validate` schema-checks an `Experiment` JSON before you spend money running it.

## `report`: Render an existing report

```bash
# Static Rich rendering on stdout (Rich on a TTY, JSON when piped; pass --rich to force)
strands-evals report reports/regression.json --rich

# Interactive Rich table (expand/collapse rows)
strands-evals report reports/regression.json --interactive

# Include diagnosis recommendations
strands-evals report reports/regression.json --recommendations

# Re-emit as JSON
strands-evals report reports/regression.json --json
```

`report` accepts `-` to read from stdin, so it composes with `run`:

```bash
strands-evals run experiments/regression.json --agent my_pkg.agents:build_agent \
  | strands-evals report - --recommendations
```

`-o PATH` always writes JSON regardless of `--interactive`/`--rich`, so you can pipe through `report` to persist a stable on-disk format.

## `validate`: Schema-check an experiment

```bash
strands-evals validate experiments/customer_service.json
# valid: 12 case(s), 3 evaluator(s) [OutputEvaluator, TrajectoryEvaluator, HelpfulnessEvaluator]
```

`validate` loads the file via `Experiment.from_file` and reports case + evaluator counts. It exits non-zero on schema or I/O errors, making it a fast CI gate before `run`. Use `--custom-evaluator MODULE:CLASS` (repeatable) when the experiment references custom evaluators.

## Next steps

-   [`run`](/docs/user-guide/evals-sdk/cli/run/index.md): produce the report JSON these commands consume.
-   [Serialization](/docs/user-guide/evals-sdk/how-to/serialization/index.md): the on-disk shapes consumed by `validate` and `report`.
-   [CI integration](/docs/user-guide/evals-sdk/cli/index.md#ci-integration): wire `validate` and `run` into a workflow.