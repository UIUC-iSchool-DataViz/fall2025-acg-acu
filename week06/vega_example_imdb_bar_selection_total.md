---
title: vega-lite example 4
description: More complex bar selection in vega-lite
layout: vegalite_example
---


{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "data": {"url": "data/movies.json"},
  "vconcat": [
    {
      "mark": {"type": "text", "fontSize": 16},
      "title": "Total Gross",
      "transform": [{"filter": {"param": "my_selection"}}],
      "encoding": {"text": {"aggregate": "sum", "field": "Worldwide Gross", "format": "0.3e"}}
    },
    {
      "hconcat": [
        {
          "width": 400,
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
          "layer": [
            {
              "mark": "bar",
              "width": 200,
              "encoding": {
                "x": {
                  "field": "IMDB Rating",
                  "type": "quantitative",
                  "bin": true
                },
                "y": {
                  "field": "Worldwide Gross",
                  "type": "quantitative",
                  "aggregate": "sum"
                },
                "color": {"value": "grey"}
              }
            },
            {
              "mark": "bar",
              "width": 200,
              "transform": [{"filter": {"param": "my_selection"}}],
              "encoding": {
                "x": {
                  "field": "IMDB Rating",
                  "type": "quantitative",
                  "bin": true
                },
                "y": {
                  "field": "Worldwide Gross",
                  "type": "quantitative",
                  "aggregate": "sum"
                }
              }
            }
          ]
        }
      ]
    }
  ]
}
