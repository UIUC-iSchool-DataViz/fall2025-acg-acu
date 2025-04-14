---
title: vega-lite example 4
description: Binding to a radius parameter
layout: vegalite_example
---


{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {
    "values": [
      {"animal": "Dog", "count": 4},
      {"animal": "Cat", "count": 8},
      {"animal": "Capybara", "count": 2},
      {"animal": "Snake", "count": 4},
      {"animal": "Cassowary", "count": 2}
    ]
  },
  "params": [
    {
      "name": "radius_param",
      "value": 50,
      "bind": {"input": "range", "min": 0, "max": 95}
    }
  ],
  "mark": "arc",
  "encoding": {
    "color": {"field": "animal"},
    "theta": {"field": "count", "type": "quantitative"},
    "radius": {"value": 100},
    "radius2": {"datum": {"expr": "radius_param"}}
  }
}
