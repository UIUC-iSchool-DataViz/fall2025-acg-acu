---
title: Building Inventory Ranking by Year
description: 
layout: vegalite_example
---
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "url": "https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/building_inventory.csv"
  },
  "vconcat": [
    {
      "mark": "line",
      "params": [
        {
          "select": {"type": "interval", "encodings": ["x"]},
          "name": "years_selected"
        }
      ],
      "transform": [
        {
          "aggregate": [
            {
              "op": "sum",
              "field": "Square Footage",
              "as": "total_square_footage"
            }
          ],
          "groupby": ["Year Acquired"]
        },
        {
          "window": [
            {"field": "total_square_footage", "op": "sum", "as": "agg_accum"}
          ],
          "sort": [{"field": "Year Acquired", "order": "ascending"}]
        }
      ],
      "encoding": {
        "x": {"field": "Year Acquired", "type": "temporal"},
        "y": {"field": "agg_accum", "type": "quantitative"}
      }
    },
    {
      "transform": [
        {"filter": {"param": "years_selected"}},
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
        {"filter": "datum.agency_rank <= 10"}
      ],
      "mark": "bar",
      "encoding": {
        "x": {"field": "Agency Name"},
        "y": {"field": "total_by_agency", "type": "quantitative"}
      }
    }
  ]
}
