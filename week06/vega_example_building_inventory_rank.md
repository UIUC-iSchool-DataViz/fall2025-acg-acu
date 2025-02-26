---
title: Building ranking operation
description: Top-5 agencies for building inventory
layout: vegalite_example
---

{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "url": "https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/building_inventory.csv"
  },
  "width": 600,
  "height": 400,
  "mark": "bar",
  "params": [
    {
      "bind": {"input": "range", "min": 0, "max": 10, "step": 1, "name": "Rank Wanted"},
      "value": 5,
      "name": "rank_wanted"
    }
  ],
  "transform": [
    {
      "aggregate": [
        {"field": "Square Footage", "as": "total_by_agency", "op": "sum"}
      ],
      "groupby": ["Agency Name"]
    },
    {
      "window": [
        {"field": "total_by_agency", "op": "rank", "as": "agency_rank"}
      ]
    },
    {"filter": "datum.agency_rank <= rank_wanted"}
  ],
  "encoding": {
    "x": {"field": "Agency Name"},
    "y": {"field": "total_by_agency", "type": "quantitative"}
  }
}
