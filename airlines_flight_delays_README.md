# Which New York departures will leave 15+ minutes late?

Predicting departure delays for all 336,776 flights scheduled from JFK, LaGuardia and Newark in 2013, and measuring how much better the prediction gets once day-of-operations information is known.

**Business question.** Where should an airline put schedule buffers months ahead, and which flights should the operations team protect an hour before departure?

**Answer in one paragraph.** 22% of departed flights left 15+ minutes late. Using only what is known when the schedule is published, a model ranks flights with a ROC AUC of 0.67. Adding weather from an hour earlier and how late the airport already is lifts that to 0.74. Flagging the riskiest 10% of flights catches 29% of all delays at 57% precision (2.9× better than chance). A random train/test split would have claimed 0.77: the test here is on October to December, months the model never saw.

![Delay rate by hour](figures/fig1_delay_by_hour.png)

## What is in this repository

| Path | Contents |
|---|---|
| `src/analysis.py` | The whole analysis as one script with `# %%` cells (runs in Spyder, VS Code or plain Python) |
| `analysis.ipynb` | The same analysis as an executed notebook |
| `figures/` | Seven figures produced by the script |
| `results/metrics.json` | Every number quoted in the paper |
| `paper/paper.md` | Write-up in research-paper format with references |
| `animation.html` | Step-through explanation of the project (open in a browser) |

## Run it

```bash
pip install -r requirements.txt
python src/analysis.py
```

The data ship inside the `nycflights13` Python package, so nothing else needs downloading.

## Data and credit

US Bureau of Transportation Statistics on-time performance data, NOAA hourly weather and FAA aircraft registry, as packaged in `nycflights13` (Hadley Wickham; CC0). 

## Method in brief

1. **Clean**: missing departure times are cancellations (8,255), flagged rather than dropped; an impossible wind speed of 1,048 mph set to missing; an 80%-empty column removed; left joins asserted to keep the row count.
2. **Explore**: delay rate by hour, month, carrier, and by how late the airport already is.
3. **Split by time**: train January to September, test October to December.
4. **Model**: baseline, logistic regression, gradient boosting; each with schedule-time features and with day-of-operations features. All preprocessing inside scikit-learn pipelines.
5. **Evaluate**: ROC AUC, average precision, Brier score, calibration, permutation importance.
6. **Decide**: precision and recall when the top 5%, 10%, 20% of flights are flagged.

Limitations are listed in section 6 of the paper.
