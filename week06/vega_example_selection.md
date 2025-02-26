---
title: vega-lite example 4
description: Selecting IMDB grosses
layout: vegalite_example
---


{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {"url": "data/movies.json"},
  "width": 600,
  "height": 500,
  "params": [{"name": "my_selection", "select": "interval"}],
  "mark": "circle",
  "encoding": {
    "x": {"field": "US Gross", "type": "quantitative"},
    "y": {"field": "Worldwide Gross", "type": "quantitative"},
    "tooltip": {"field": "Title"},
    "color": {"value": "gray", "condition": {"param": "my_selection", "field": "MPAA Rating"}}
  }
}
