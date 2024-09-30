---
title: vega-lite example 4
description: A couple movie charts with linked selection
layout: vegalite_example
---


{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {"url": "data/movies.json"},
  "hconcat": [
    {
      "mark": "point",
      "params": [{"name": "selected", "select": "interval"}],
      "encoding": {
        "x": {"field": "Production Budget", "type": "quantitative"},
        "y": {"field": "US Gross", "type": "quantitative"},
        "color": {"value": "grey", "condition": {"param": "selected"}}
      }
    },
    {
      "mark": "bar",
      "transform": [{"filter": {"param": "selected"}}],
      "params": [{"name": "stanley", "select": "interval", "bind": "scales"}],
      "encoding": {
        "x": {"field": "IMDB Rating", "bin": true, "type": "quantitative"},
        "y": {
          "aggregate": "sum",
          "field": "Worldwide Gross",
          "type": "quantitative"
        }
      }
    },
    {
      "mark": "bar",
      "encoding": {
        "x": {
          "field": "MPAA Rating",
          "scale": {"domain": ["G", "PG", "PG-13"]}
        },
        "y": {
          "field": "Worldwide Gross",
          "aggregate": "sum",
          "type": "quantitative"
        }
      }
    }
  ]
}
