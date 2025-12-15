# 2018-05-31-crime-and-heat-analysis

## Reproduction in Roundup

These steps outline just one of many possible ways to wrangle the source tables into the final form. It takes the path with the shortest number of steps.

1. Load the following source tables: `lambert_1.csv` (45 x 3,653), `lambert_2.csv` (21 x 120), and `violent_crimes.csv` (4 x 64,739)
2. Create a _stack_ operation, Stack-1, from `lambert_2.csv` and `lambert_2.csv`.
3. Trim extra `lambert_1.csv` columns, indices 22-45, to align tables.
4. Trim _stack_ child columns at indices 1-2 (`STATION` and `NAME`).
5. Trim _stack_ child columns at indices 2-3 (`PRCP` and `PRCP_ATTR`).
6. Trim _stack_ child columns at indices 3-17, leaving only `DATE` and `TMAX`.
7. Materialize Stack-1 and inspect results
8. Create a _pack_ operation, Pack-1, from Stack-1, and `violent_crimes.csv`.
9. Set _pack_ parameters in Pack-1: _left join key_ = `DATE`, _right join key_ = `Date`, _join predicate_ = `CONTAINS`.
10. Swap table positions in Pack-1, `violent_crimes.csv` becomes _left table_ and Stack-1 becomes _right table_.
11. Materialize Pack-1 and inspect results
12. Export Pack-1

## Original `README.md`

This is a basic analysis of crime and temperature for the story [Warm weather worries in St. Louis: When temperatures rise, crime often follows
](http://news.stlpublicradio.org/post/warm-weather-worries-st-louis-when-temperatures-rise-crime-often-follows).

See the [python notebook](crimes-and-heat.ipynb) for the analysis.
