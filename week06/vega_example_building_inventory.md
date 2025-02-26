---
title: vega-lite example 4
description: Building inventory in Vega Lite
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
  "params": [{"name": "panzoom", "bind": "scales", "select": "interval"}],
  "encoding": {
    "x": {
      "field": "Year Acquired",
      "type": "temporal",
      "bin": true,
      "timeUnit": {"unit": "year", "step": 10}
    },
    "y": {"field": "Square Footage", "type": "quantitative", "aggregate": "sum"}
  }
}
