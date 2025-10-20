# Deneb Templates
## Line Chart Brush + Zoom
```json
{
  "usermeta": {
    "information": {
      "uuid": "c5f8ca48-0b47-4c26-bf63-6df13e6b4684",
      "generated": "2025-10-20T09:01:11.712Z",
      "previewImageBase64PNG": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVR42mNkYAAAAAYAAjCB0C8AAAAASUVORK5CYII=",
      "name": "Line Chart Brush + Zoom",
      "description": "Two stacked line charts. \nUse the brush on the bottom chart to zoom on the top chart.",
      "author": "Clement Villalard"
    },
    "deneb": {
      "build": "1.8.1.0",
      "metaVersion": 1,
      "provider": "vegaLite",
      "providerVersion": "6.1.0"
    },
    "interactivity": {
      "tooltip": true,
      "contextMenu": true,
      "selection": false,
      "selectionMode": "simple",
      "highlight": false,
      "dataPointLimit": 50
    },
    "config": "{\n  \"view\": {\n    \"stroke\": \"transparent\"\n  },\n  \"font\": \"Segoe UI\",\n  \"arc\": {},\n  \"area\": {\n    \"line\": true,\n    \"opacity\": 0.6\n  },\n  \"bar\": {},\n  \"line\": {\n    \"strokeWidth\": 0.5,\n    \"strokeCap\": \"round\",\n    \"strokeJoin\": \"round\",\n    \"grid\":true\n      },\n  \"point\": {\n    \"filled\": true,\n    \"size\": 75\n  },\n  \"rect\": {},\n  \"text\": {\n    \"font\": \"Segoe UI\",\n    \"fontSize\": 12,\n    \"fill\": \"#716E76\"\n  },\n  \"axis\": {\n    \"ticks\": false,\n    \"grid\": false,\n    \"domain\": false,\n    \"labelColor\": \"#716E76\",\n    \"labelFontSize\": 12,\n    \"titleFont\": \"din\",\n    \"titleColor\": \"#192229\",\n    \"titleFontSize\": 16,\n    \"titleFontWeight\": \"normal\"\n  },\n  \"axisQuantitative\": {\n    \"tickCount\": 3,\n    \"grid\": true,\n    \"gridColor\": \"#EDEDED\",\n    \"gridDash\": [\n      1,\n      5\n    ],\n    \"labelFlush\": false\n  },\n  \"axisX\": {\n    \"labelPadding\": 5\n  },\n  \"axisY\": {\n    \"labelPadding\": 10\n  },\n  \"header\": {\n    \"titleFont\": \"din\",\n    \"titleFontSize\": 16,\n    \"titleColor\": \"#192229\",\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 13.333333333333332,\n    \"labelColor\": \"#716E76\"\n  },\n  \"legend\": {\n    \"titleFont\": \"Segoe UI\",\n    \"titleFontWeight\": \"bold\",\n    \"titleColor\": \"#716E76\",\n    \"labelFont\": \"Segoe UI\",\n    \"labelFontSize\": 13.333333333333332,\n    \"labelColor\": \"#716E76\",\n    \"symbolType\": \"circle\",\n    \"symbolSize\": 75\n  }\n}",
    "dataset": [
      {
        "key": "__0__",
        "name": "Timestamp",
        "description": "Any Date or Date/Time field",
        "kind": "column",
        "type": "dateTime"
      },
      {
        "key": "__1__",
        "name": "Value",
        "description": "",
        "kind": "measure",
        "type": "numeric"
      }
    ]
  },
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "Line chart with brush + zoomed detail",
  "data": {
    "name": "dataset" // Use the dataset already loaded in Power BI
  },
  "vconcat": [ // Vertical concatenation: top chart + bottom chart
    {
      // --- Top Chart: zoomed view (filtered by brush) ---
      "mark": {
        "type": "line", // Line chart
        "interpolate": "monotone", // Smooth line
        "color": {
          "expr": "pbiColor(0)"
        },
        "tooltip": true,
        "strokeWidth": 1.5 // adjust as needed
      },
      "encoding": {
        "x": {
          "field": "__0__", // X-axis uses your timestamp field
          "type": "temporal", // Temporal axis (dates/times)
          "axis": {
            "title": null
          } // No title on top chart
        },
        "y": {
          "field": "__1__", // Y-axis uses Demand_kW
          "type": "quantitative", // Numeric scale
          "axis": {
            "tickCount": 10, // Number of ticks
            "grid": true, // Show gridlines
            "gridColor": "lightgrey", // Gridline color
            "gridDash": [],
            "gridOpacity": 0.3,
            "title": "__1__" // Y-axis title
          }
        }
      },
      "transform": [
        {
          "filter": {
            "param": "brush"
          }
          // Only show data in the interval selected by the brush
        }
      ],
      "width": 800, // Chart width
      "height": 350 // Chart height
    },
    {
      // --- Bottom Chart: brush/selector ---
      "mark": {
        "type": "line", // Line chart (overview)
        "interpolate": "monotone",
        "color": {
          "expr": "pbiColor(0)"
        }
      },
      "encoding": {
        "x": {
          "field": "__0__",
          "type": "temporal",
          "axis": {
            "title": "__0__"
          } // Show X-axis title
        },
        "y": {
          "field": "__1__",
          "type": "quantitative",
          "axis": {
            "title": null, // Hide Y-axis title in brush chart
            "labels": false, // Hide labels
            "ticks": false, // Hide ticks
            "grid": false // Hide gridlines
          }
        }
      },
      "params": [
        {
          "name": "brush", // Name of the selection parameter
          "select": {
            "type": "interval",
            "mark": {
              "fill": "grey",
              "fillOpacity": 0.1,
              "stroke": "grey",
              "strokeOpacity": 0.5
            }, // Interval selection (drag over X-axis)
            "encodings": [
              "x"
            ] // Only select along the X-axis
          }
        }
      ],
      "width": 800,
      "height": 80 // Small overview chart
    }
  ]
}
```
