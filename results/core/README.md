# Core project results

All files in this directory were produced by the cumulative four-day **mock** Murshid notebook.

| File | Contents |
| --- | --- |
| `baseline_results.json` | Day 1 Arabic/English FAQ and clarification baseline |
| `day2_results.json` | Day 2 structured request and synthetic status outcomes |
| `day3_results.json` | Ten golden test results, including intended refusals |
| `day4_results.json` | Controlled public-FAQ caching comparison |
| `metrics.json` | Per-request mock call counts, cache flags, and Python timing in milliseconds |
| `synthetic_data.json` | Fictional directory text and demo application records |
| `final_report.json` | Combined selected-case test summary, cache experiment, limitations, and hypothetical-cost illustration |

The Day 3 and Day 4 suites each recorded **10/10 passing selected mock cases**. In the repeated-question experiment, the mock-client call count fell from **3 to 1**, producing two cache hits across three requests (66.7%). The core made **zero external model API calls**. These values do not establish real-model quality, production security, or actual cost savings.
