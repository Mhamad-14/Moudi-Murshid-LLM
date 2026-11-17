# Murshid Mini | Project notes

## Purpose and implementation

Murshid Mini is an educational service-question prototype. The four-day core demonstrates the Python application logic surrounding a model-shaped interface. Its `FakeClient` is deterministic: it returns predefined answers for synthetic questions rather than generating text with a trained model.

## Synthetic dataset

The dataset is handwritten for teaching. It is not extracted from a government service or real users. The committed snapshot is [synthetic_data.json](../results/core/synthetic_data.json).

- `service_directory.ar` and `service_directory.en`: predefined Arabic and English FAQ answers.
- `records`: fictional application records indexed by a reference string such as `REF-1001`.
- `owner`: synthetic demo-user identifier used by the ownership check.
- `status`: fictional application status, such as `under_review` or `approved`.

The example record `REF-1001` belongs to `demo-user-1` and has status `under_review`. `REF-1002` belongs to `demo-user-2`. The demonstration's default synthetic session is `demo-user-1`, so a lookup of `REF-1002` is refused instead of revealing its private status.

## Four-day implementation

### Day 1: Baseline

The notebook creates the fictional service directory and a deterministic `FakeClient`. Baseline questions establish the expected bilingual FAQ behavior and save [baseline_results.json](../results/core/baseline_results.json).

### Day 2: Structured request and read-only tool

The routing flow extracts structured status-request fields (`service`, `city`, `request_id`, and `needs_clarification`). The read-only lookup validates the reference and checks ownership using the synthetic session. Missing references trigger clarification. Unsupported actions do not modify records. These checks are exercises in application-controlled decisions, not real authentication.

### Day 3: Guards and golden cases

The application checks input and output contracts, and distinguishes accepted responses from safe rejections. The ten selected test cases cover two public FAQs, authorized/absent/missing references, unsupported scope, access denial, an instruction override, blank input, and malformed schema output. Correct refusals count as passing cases when they match the expected outcome.

The saved Day 3 report records **10 passed out of 10**, in `mode=mock`. This is selected-case coverage, not an assertion of general safety or accuracy.

### Day 4: Cache and regression

The cache targets exact public FAQ questions. Its key includes relevant versions so changes to the prompt or directory can invalidate stale answers. Private application-status queries do not enter the public cache.

For three identical public FAQ requests:

| | No cache | Cache initially empty |
| --- | ---: | ---: |
| Requests | 3 | 3 |
| Mock-client calls | 3 | 1 |
| Cache hits | 0 | 2 |
| Cache-hit rate | 0% | 66.7% |

The cache-hit sequence is `false`, `true`, `true`. Day 4 also reruns the ten-case mock suite, returning **10/10**. The mock-client call counts are deterministic experiment data, not real API cost reductions. The core uses no external inference API.

## Homework assignments

Day 1 runs local `google/flan-t5-small` to demonstrate actual model generation. Day 2 checks seven simulated structured tool calls, including invalid calls and unauthorized access. Day 3 catches three intended Python validation exceptions and confirms a corrected question is accepted. Day 4 uses the same local model to generate answers for three synthetic FAQ paraphrases, recording token counts, measured inference time, and a reference-number keyword indicator.

The recorded Day 4 evaluation contains 3/3 keyword hits. Manual review found the three answers consistent with the single synthetic context sentence. The indicator checks two words, so it cannot measure broad semantic accuracy or Arabic-language competence.

## Reproduction and evidence

Open [the core notebook](../notebooks/Moudi_Murshid.ipynb) in Python 3.9+ or Google Colab CPU and run its cells in order. No additional Python libraries or keys are necessary for the core. The notebook writes JSON files to `murshid_outputs/`, and the committed snapshots are in [results/core](../results/core/).

The real-model homework notebooks need their own Colab CPU sessions with dependencies and downloaded weights. The Day 1 and Day 4 local inference reports are in [results/day1](../results/day1/) and [results/day4](../results/day4/).

## Limitations and possible improvement

- Only predefined questions and synthetic records are represented.
- `FakeClient` is not a language model and does not evaluate natural-language correctness.
- A demo user identifier does not provide authenticated identity or production authorization.
- Simple input guards do not provide comprehensive prompt-injection defense.
- Ten mock cases and three real-model homework cases are too small to support generalized quality claims.
- Timing measurements depend on the local runtime. The final report's cost example is hypothetical, not billed usage.

A future iteration would add a real authentication system, an independently reviewed dataset with more question types, and end-to-end evaluation of response correctness and safety. These additions would need testing before any real-world deployment.

## Attribution

This project was completed for **LLM Application Engineering (SDA-AIE-213)** with instructor **Meaad Al-Marri** in the [SDAIA Academy](https://github.com/SDAIAAcademy) training context. Reference materials are from the [instructor's course repository](https://github.com/almiyead-rgb/murshid-llm-application-engineering-sda-aie-213). Attribution does not imply endorsement of the implementation.
