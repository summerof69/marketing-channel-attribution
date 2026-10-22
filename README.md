# Marketing Channel Attribution

Companion notebooks and data for the **Marketing Channel Attribution** series on [harendrasahu.com](https://www.harendrasahu.com). They reproduce every chart and table in the articles, using two fictional companies:

- **Kesari Threads**: a D2C ethnic-wear brand with short journeys (2,000 orders)
- **TaskHarbor**: a B2B SaaS tool with long journeys (600 deals)

All companies and numbers are fictional. The data is simulated with fixed random seeds, so every run gives the same numbers as the blog.

## Notebooks

| Part | Article | Notebook | Open |
| --- | --- | --- | --- |
| 1 | [What Is Marketing Attribution? A Practical Introduction](https://www.harendrasahu.com/blog/attribution-1-what-is-marketing-attribution) | [attribution_1_what_is_marketing_attribution_notebook.ipynb](notebooks/attribution_1_what_is_marketing_attribution_notebook.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/summerof69/marketing-channel-attribution/blob/main/notebooks/attribution_1_what_is_marketing_attribution_notebook.ipynb) |
| 2 | [First Touch, Last Touch, Linear and More: Attribution Models Explained](https://www.harendrasahu.com/blog/attribution-2-attribution-models-explained) | [attribution_2_attribution_models_explained_notebook.ipynb](notebooks/attribution_2_attribution_models_explained_notebook.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/summerof69/marketing-channel-attribution/blob/main/notebooks/attribution_2_attribution_models_explained_notebook.ipynb) |
| 3 | [The Last-Click Trap: Why LNDC Starves Your Top of Funnel](https://www.harendrasahu.com/blog/attribution-3-lndc-problem-why-multi-touch) | [attribution_3_lndc_problem_why_multi_touch_notebook.ipynb](notebooks/attribution_3_lndc_problem_why_multi_touch_notebook.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/summerof69/marketing-channel-attribution/blob/main/notebooks/attribution_3_lndc_problem_why_multi_touch_notebook.ipynb) |

What each notebook covers:

- **Part 1**: journey length for both companies, one order credited four ways, and two example journeys split into TOF and BOF.
- **Part 2**: six rule-based models (first touch, last click (LC), last non-direct click (LNDC), linear, position-based and time decay) on one example order and on all 2,000 Kesari Threads orders, plus custom position-based splits and half-life sensitivity for time decay.
- **Part 3**: LC vs LNDC, how much credit top-of-funnel and bottom-of-funnel channels get under each model, TaskHarbor's attributed ROAS, and how many touchpoints single-touch models ignore.

## Dataset

[`dataset/attribution-multi-touch-data.csv`](dataset/attribution-multi-touch-data.csv) has one row per touchpoint in a journey that ended in a conversion (10,262 rows). Every notebook regenerates this same file from scratch, so you don't need to download it to run them.

| Column | Description |
| --- | --- |
| `journey_id` | ID of one customer's path to a single conversion. `D2C-xxxxx` = Kesari Threads order, `B2B-xxxxx` = TaskHarbor deal. |
| `step` | Order of the touchpoint in its journey. `1` = first touch. |
| `channel` | The source the touchpoint came from, e.g. Instagram Ads, Email, Brand Search, Direct. |
| `stage` | `TOF` = up to add to cart (Kesari) or the demo request (TaskHarbor); `BOF` = after it. |
| `days_before_conversion` | Days before the conversion. The last touch is always `0`. |
| `revenue` | Conversion value in INR. Repeats on every row of a journey, so take one value per `journey_id` before summing. |
| `company` | `Kesari Threads` or `TaskHarbor`. |

TaskHarbor revenue is simulated in USD and converted at a fixed ₹80 per USD.

## Run it

**In Colab (no setup):** click a badge above, then **Runtime → Run all**.

**Locally:**

```bash
pip install numpy pandas matplotlib seaborn jupyter
jupyter notebook notebooks/
```

Each notebook saves its charts as PNG files next to itself.

## Use your own data

Replace the generated `d2c` or `b2b` DataFrame with your own export, using the same columns (at minimum `journey_id`, `step`, `channel`, `days_before_conversion` and `revenue`). Every model and chart then runs unchanged.

## Licence

MIT. See [LICENSE](LICENSE).
