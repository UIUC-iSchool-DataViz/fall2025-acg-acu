---
title: vega-lite example 4
description: Selecting for bar graphs with IMDB
layout: vegalite_example
---


{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {"url": "data/movies.json"},
  "hconcat": [
    {
      "params": [{"name": "my_selection", "select": "interval"}],
      "mark": "circle",
      "encoding": {
        "x": {"field": "US Gross", "type": "quantitative"},
        "y": {"field": "Worldwide Gross", "type": "quantitative"},
        "tooltip": {"field": "Title"},
        "color": {
          "value": "gray",
          "condition": {"param": "my_selection", "field": "MPAA Rating"}
        }
      }
    },
    {
      "mark": "bar",
      "transform": [
        {"filter": {"param": "my_selection"}}
      ],
      "encoding": {
        "x": {"field": "IMDB Rating", "type": "quantitative", "bin": true},
        "y": {"field": "Worldwide Gross", "type": "quantitative", "aggregate": "sum"}
      }
    }
  ]
}
