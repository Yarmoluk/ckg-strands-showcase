# Reported results & scope

[← Project overview](README.md)

These aggregate figures describe Daniel Yarmoluk's September 22, 2026 experiment. The implementation, complete graph, and raw reports are private. This page is a reported summary, not a publicly reproducible benchmark or an independent audit.

## Combined live demonstration

| Measure | Direct lookup | Generated explanation |
|---|---:|---:|
| Model calls | 0 | 1 |
| Request time | 0.109 ms | 7.064 s |
| Local context preparation | 0.108 ms | 0.074 ms |
| Input model tokens | Not applicable | 712 |
| Output model tokens | Not applicable | 175 |
| Total model tokens | Not applicable | 887 |

Graph loading: 0.670 ms, separately. Context preparation is included in request time. Request time excludes interpreter startup and terminal printing. One request per route; different tasks, not a speed comparison. Model: `claude-sonnet-4-6`. Fixture: 48 concepts.

The demonstrated result is that the application can complete the supported lookup without a model, and can provide the retrieved context to Strands for one explanation call. The generated response added claims beyond the supplied evidence and was not graded for full semantic accuracy.

## Earlier extension comparison

Five questions, two trials per arm. Correctness was measured against manually specified expectations for the graph snapshot.

| Arm | Correct JSON content | Tokens / 10 answers | Mean time / answer | Model calls / 10 answers |
|---|---:|---:|---:|---:|
| Full CSV | 10/10 | 42,470 | 4.97 s | 10 |
| Full CSV + CKG extension | 10/10 | 111,365 | 11.33 s | 21 |
| Selective CKG extension | 10/10 | 27,414 | 10.87 s | 20 |

All arms scored 0/10 on strict JSON-only formatting. JSON content was re-scored using saved responses after the same parser correction was applied to each arm. Surrounding prose was not graded. No model requests were repeated to recover those scores.

The additive configuration did not improve this measured task. Selective context reduced token usage but increased latency. Fallback tool use added model round trips; output verbosity also differed. This comparison does not isolate network or traversal latency.

The combined router has not yet been evaluated against these arms on equivalent tasks.

## Validation

The private implementation passed 55 Python tests covering traversal, routing, parsing, context injection, and provider cleanup. SDK/provider tests used simulated HTTP responses. These checks validate behavior, not live model quality.

The public workflow checks only the showcase's allowed file inventory. It does not run or expose the private implementation.

## Limits and next steps

- Small experimental fixture; not a production deployment or a RAG comparison.
- Declared relationships were not independently reverified against current source pages for this release.
- Successful generation is not proof that every generated claim is supported.
- Next work: reviewed domain relationships, broader question coverage, and equivalent-task comparisons of error rates, latency distributions, and token usage.
