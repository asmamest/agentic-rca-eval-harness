# Rebuilding the Agentic RCA Harness

Use this roadmap to rebuild the repository in a separate learning repository. Implement and understand each stage yourself before moving forward.

## 1. Prepare the Workspace

- Install Python, Git, Docker, and Ollama.
- Create a virtual environment.
- Add `.gitignore`, `requirements.txt`, and a basic README.
- Commit: `chore: initialize Python project configuration`

## 2. Model the RCA Domain

Create Pydantic models for:

- `Observation`
- `Hypothesis`
- `TriageState`
- Incident metadata
- Ground-truth labels

Build a synthetic incident generator and save a labeled incident dataset as JSON.

Commits:

- `feat: add typed RCA schemas`
- `feat: add synthetic incident generator`
- `feat: add labeled incident dataset`

## 3. Implement the Evidence Agents

Build each agent independently:

1. **Log Reader**: parse log anomalies.
2. **Metrics Analyst**: detect thresholds and metric spikes.
3. **Trace Inspector**: identify latency or error propagation.
4. **Hypothesis Generator**: rank possible root causes.

Test every agent with a single incident before integrating it.

Commits:

- `feat: add log reader sub-agent`
- `feat: add metrics analyst sub-agent`
- `feat: add trace inspector sub-agent`
- `feat: add hypothesis generator sub-agent`

## 4. Build the Orchestrator

- Connect the agents using LangGraph.
- Pass typed state between nodes.
- Aggregate observations.
- Generate a confidence-scored ranked hypothesis.
- Add defensive handling for malformed or truncated model responses.

Commits:

- `feat: add LangGraph RCA workflow`
- `fix: handle truncated agent JSON responses`

## 5. Add Component-Level Evaluations

Test each sub-agent independently.

Cover:

- Log extraction accuracy
- Metric threshold detection
- Trace span selection
- Observation uniqueness and validity
- Observation ID references

Commits:

- `test: add sub-agent evaluation cases`
- `feat: add component-level scorers`

## 6. Add End-to-End Evaluations

Evaluate the complete pipeline against the labeled incident dataset.

Measure:

- Root-cause correctness
- Hypothesis groundedness
- Confidence calibration
- Judge quality
- Error rate
- Execution time

Start with deterministic keyword scoring, then add LLM-as-judge scoring.

Commits:

- `feat: add end-to-end evaluation runner`
- `feat: add groundedness and correctness scorers`
- `feat: add LLM-as-judge scoring`

## 7. Add Prompt Regression Testing

Configure Promptfoo to:

- Test multiple prompts.
- Use case-insensitive assertions.
- Compare llama3.1 and llama3.2.
- Preserve evaluation reports.

Commits:

- `feat: add Promptfoo prompt regression suite`
- `test: add prompt vocabulary assertions`

## 8. Add Observability

Instrument:

- Orchestrator spans
- Sub-agent spans
- Prompt inputs
- Structured outputs
- Ground-truth labels
- Confidence values
- Incident IDs
- Errors and latency

Run the system with local Arize Phoenix in Docker.

Commits:

- `feat: add OpenTelemetry tracing`
- `feat: instrument orchestrator and sub-agents`
- `feat: add Phoenix Docker setup`

## 9. Harden the System

Improve:

- Input and schema validation
- Prompt instructions
- Retry behavior
- Timeout handling
- Logging
- Secrets management
- Reproducible incident generation
- Unit and integration tests
- Continuous integration

Commit each improvement independently.

## 10. Add an Original Improvement

Choose two or three extensions:

- Stream sub-agent progress
- Support multiple LLM providers
- Compare routing strategies
- Add cost and latency dashboards
- Visualize evaluation trends over commits
- Add a web interface
- Add retrieval only if a measured baseline shows that it helps

For each extension:

1. Define a measurable hypothesis.
2. Record the baseline.
3. Implement the smallest useful change.
4. Add tests or evaluations.
5. Commit and push it separately.
6. Explain the result in the README.

## Suggested 14-Day Schedule

| Day | Goal |
|---|---|
| 1 | Environment and project structure |
| 2 | Pydantic schemas |
| 3 | Synthetic incidents |
| 4 | Log Reader |
| 5 | Metrics Analyst |
| 6 | Trace Inspector |
| 7 | Hypothesis Generator |
| 8 | LangGraph orchestration |
| 9 | Component evaluations |
| 10 | End-to-end evaluation |
| 11 | Promptfoo |
| 12 | Observability |
| 13 | Test and improve weak areas |
| 14 | Documentation and portfolio polish |

Study the existing repository when blocked, but implement each file by reasoning through it yourself rather than copying it directly.
