# Toronto Firearm Incident Analysis

I pulled Toronto Police Service open data on shootings and firearm discharges and asked a pretty simple question: do the neighbourhoods with the most incidents also tend to have the most harm, or does “high risk” shift depending on whether you count events vs. injuries and deaths? The notebook cleans the data, ranks neighbourhoods a few different ways, checks how closely incident counts track harm, and looks at year-over-year trends and event types.

**Role:** Built this solo as a personal project — data cleaning, analysis, charts, and write-up were all me.

## Tools

- Python
- pandas
- matplotlib
- Jupyter Notebook

## What’s in the data (from the notebook run)

After dropping unclear neighbourhood labels (`NSA`), the cleaned set had **6,759** incidents, **3,114** injuries, and **788** deaths (harm = injuries + deaths → **3,902**).

A few numbers that stuck out:

- Correlation between neighbourhood incident counts and total harm: **0.968**
- **6** neighbourhoods showed up in both the top 10 by incidents and the top 10 by harm (Black Creek, Glenfield-Jane Heights, West Humber-Clairville, Mount Olive-Silverstone-Jamestown, Yorkdale-Glen Park, York University Heights)
- By raw incident volume, Glenfield-Jane Heights led at **347** incidents; ranking by harm *per* incident looked totally different (e.g. Playter Estates-Danforth at **1.83** harm per incident on only **12** incidents)
- Split by event type: **3,600** firearm discharges (0 recorded injuries/deaths in this file) vs **3,159** shootings (all of the injuries and deaths above)

So frequency and total harm move together at the neighbourhood level, but the “worst” places on a per-incident basis are not the same list.

## How to run it

1. Clone this repo (or download the folder).
2. Make sure `shooting_firearm_discharges.csv` sits next to `Toronto_Firearm_Analysis_Code.ipynb` (it already does in this folder).
3. Install what you need:

```bash
pip install pandas matplotlib jupyter
```

4. Open the notebook and run all cells:

```bash
jupyter notebook Toronto_Firearm_Analysis_Code.ipynb
```

Running it will also write `neighbourhood_summary.csv`, `yearly_summary.csv`, and `event_summary.csv` — those are regenerable, so they’re gitignored.

Source data: [Toronto Police Service — Shooting and Firearm Discharges](https://data.torontopolice.on.ca/) open data portal (rename the download to `shooting_firearm_discharges.csv` if you grab a fresh copy).

## What I learned

- Cleaning matters more than I expected. Rows labeled `NSA` would have skewed any neighbourhood ranking if I’d left them in.
- One metric isn’t enough. Counting incidents and summing harm tell a similar story here (that 0.968 correlation), but harm-per-incident flips who looks “high risk,” which is useful when you’re thinking about how public safety stats get framed.
- Charts beat tables when you’re comparing top-10 lists. The overlap check (6 shared neighbourhoods) was the clearest way to answer the research question without overclaiming.
