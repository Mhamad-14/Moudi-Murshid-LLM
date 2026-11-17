# Homework | Murshid Mini

These are four independent exercises from **LLM Application Engineering (SDA-AIE-213)**. They are separate from the cumulative core project in [notebooks/murshid.ipynb](../notebooks/murshid.ipynb).

| Day | Focus | Notebook | Results |
| --- | --- | --- | --- |
| 1 | Generate an answer with local `google/flan-t5-small` | [day1_real_model.ipynb](day1_real_model.ipynb) | [live_demo_result.json](../results/day1/live_demo_result.json) |
| 2 | Validate structured calls, tool allowlisting, and record ownership | [day2_tools.ipynb](day2_tools.ipynb) | Seven test outcomes saved in the notebook |
| 3 | Catch expected `ValueError` cases and accept corrected input | [day3_errors.ipynb](day3_errors.ipynb) | Three caught rejections and a corrected input, saved in the notebook |
| 4 | Evaluate three application-status FAQ paraphrases with local FLAN-T5 | [day4_evaluation.ipynb](day4_evaluation.ipynb) | [evaluation_result.json](../results/day4/evaluation_result.json) |

Day 1 and Day 4 involve downloaded model weights and packages, but no hosted inference API or paid API key. Day 2 and Day 3 use the Python standard library.

The Day 4 output contains three keyword matches for `reference` and `number`. This limited indicator does not establish overall answer quality or general model accuracy. The notebooks retain their test outputs and explanations.
