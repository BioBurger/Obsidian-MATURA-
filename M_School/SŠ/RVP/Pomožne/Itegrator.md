
```vega-lite
{
	"width":600,
	"height":220,
	"data":{
		"values":[
			{"time": 0, "Uvh": 1},
			{"time": 1, "Uvh": 0},
			{"time": 2, "Uvh": 1},
			{"time": 3, "Uvh": 0}
		]
	},
	"layer":[
		{
			"mark":{
				"type":"line",
				"interpolate": "step-after",
				"point": false,
				"color": "#c622c9"
			},
			"encoding": { 
			"x": {"field": "time", "type": "quantitative", "title": "ms"},
			"y": {"field": "Uvh", "type": "quantitative", "title": "Uvh"}
			}
		}

	]
}
```


```vega-lite
	{
		"width":600,
		"hight":300,
		"data":{
			"values":[
				{"time":0,"Uiz":0},
				{"time":1,"Uiz":-1},
				{"time":2,"Uiz":0},
				{"time":3,"Uiz":-1}
			]
		},
		"layer":[
			{
				"mark":{
					"type":"line",
					"color": "red",
					"interpolate":"linear",
					"point":false
				},
				"encoding":{
					"x":{"field":"time","type":"quantitative","title":"ms"},
					"y":{"field":"Uiz","type":"quantitative","title":"Uiz"}
				}
			}
		]
	}
```


```chart
type: line
labels: [0.0, 1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0]
series:
  - title: "Sawtooth U (constant)"
    data: [0.0, 1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0]
  - title: "Ramp U (linear input)"
    data: [0.0, 0.5, 2.0, 4.5, 8.0, 12.5, 18.0, 24.5, 32.0]
  - title: "Curve U (quadratic input)"
    data: [0.0, 0.33, 2.67, 9.0, 21.33, 41.67, 72.0, 114.33, 170.67]
width: 100%

```
```chart
type: line
labels: [0.0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 1.0]
series:
  - title: "Constant input (U = t)"
    data: [0.0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 1.0]
  - title: "Linear input (U = t²)"
    data: [0.0, 0.01, 0.04, 0.09, 0.16, 0.25, 0.36, 0.49, 0.64, 0.81, 1.0]
  - title: "Quadratic input (U = t³)"
    data: [0.0, 0.001, 0.008, 0.027, 0.064, 0.125, 0.216, 0.343, 0.512, 0.729, 1.0]
width: 100%

```
