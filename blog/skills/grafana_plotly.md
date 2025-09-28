# Customized Grafana visualizations with Plotly Panel

Date Created: December 5, 2023 10:11 PM
Status: Doing

![image.png](image.png)

- Grafana does not directly support many visualizations out of the box (like scatter plots, box plots, sunburst chart etc.
- We will use the Plotly panel Grafana plugin to create highly customizable visualizations

## How Plotly Panel works

- Plotly panel uses Plotly JS JavaScript library to create the visualization in Grafana Panel
- Plotly JS is a famous and opensource charting library that has a provision to easily create various types of visualizations (like scatter plots, box plots, bar charts, 3d charts, sunburst chart etc.)
- The JavaScript code required to create the desired visualization is to be written in the “Script” input of a Plotly panel in Grafana dashboard.

## Plotly Panel Grafana plugin installation

- Plotly panel plugin can be found at [https://grafana.com/grafana/plugins/ae3e-plotly-panel/](https://grafana.com/grafana/plugins/ae3e-plotly-panel/)
- It can be installed directly by searching it in the Plugins page

![image.png](image%201.png)

- For offline installation, the plugin zip file can be downloaded from its GitHub releases page at [https://github.com/ae3e/ae3e-plotly-panel/releases](https://github.com/ae3e/ae3e-plotly-panel/releases) and unpack it in the Grafana plugins folder (`C:\Program Files\GrafanaLabs\grafana\data\plugins`)

![image.png](image%202.png)

## Using Plotly panel in Grafana dashboard

- Create a panel in the dashboard. In the panel editing screen, select the visualization as “Plotly panel” as shown below

![image.png](image%203.png)

## Plotly panel Script

![image.png](image%204.png)

- The Plotly panel script should return a JavaScript object with attributes `data`, `layout` and `config` (`layout` and `config` are optional)
    - `data` is a list of `traces`. Each trace contains a data series like timeseries, bar chart etc. (refer examples of various trace types [here](https://plotly.com/javascript/)).
    - `layout` is the non-data related visual attributes like title, margins, backgrounds, axis configuration etc. (refer various layout options [here](https://plotly.com/javascript/reference/layout/))
    - config is the high-level options for the chart like scroll zoom behavior, mode bar visibility etc. (refer various config options [here](https://plotly.com/javascript/configuration-options/))
- The script will have 2 JavaScript variables data and variables populated
    - The `data` variable contains the data fetched by the Grafana queries. So, the data from Grafana data sources can be used by Plotly Script using the data variable. For example, `data.series[0].fields[1].values` is the values of the 1st query and `data.series[0].fields[1].values` is the timestamps of the 2nd query
    - The `variables` variable contains the Grafana variables of the current dashboard (like user variables, global variables like `__from`, `__to`, `__interval` and `__interval_ms`)

## Examples

The following are the example scripts that can be used in a Grafana Plotly panel

### Scatter plot example

```jsx
// Correlation of stock prices between 2 companies
xData = data.series[0].fields[1].values;
yData = data.series[1].fields[1].values;

var trace1 = {
    x: xData,
    y: yData,
    mode: 'markers',
    type: 'scatter',
    marker: { size: 3 }
};

var tracesData = [trace1];

var layout = {
    title: {
        text: "Stock price correlation between Acme and Whimsey",
        font: {
            family: 'Helvetica, Arial, sans-serif',
            color: "rgb(200, 200, 200)"
        }
    },
    yaxis: {
        autorange: true,
        showgrid: true,
        gridcolor: "rgb(150, 150, 150)",
        gridwidth: 1,
        type: "linear",
    },
    xaxis: {
        type: "linear"
    },
    margin: {
        l: 40, r: 30, b: 80, t: 100
    },
    paper_bgcolor: "rgb(50, 50, 50)",
    plot_bgcolor: "rgb(50, 50, 50)",
    showlegend: false
};

return {
    data: tracesData,
    layout: layout
}
```

### Box plot example

```jsx
// Stock Price variations of companies over time
var xData = [];
var yData = [];
// console.log(data.series);
for (var i = 0; i < data.series.length; i++) {
    xData.push(data.series[i].refId);
    yData.push(data.series[i].fields[1].values);
}

var colors = ['rgba(93, 164, 214, 0.5)', 'rgba(255, 144, 14, 0.5)', 'rgba(44, 160, 101, 0.5)', 'rgba(255, 65, 54, 0.5)', 'rgba(207, 114, 255, 0.5)', 'rgba(127, 96, 0, 0.5)', 'rgba(255, 140, 184, 0.5)', 'rgba(79, 90, 117, 0.5)', 'rgba(222, 223, 0, 0.5)'];

var tracesdata = [];

for (var i = 0; i < xData.length; i++) {
    var result = {
        type: 'box',
        y: yData[i],
        name: xData[i],
        boxpoints: 'outlier',
        jitter: 0.5,
        whiskerwidth: 0.2,
        fillcolor: 'cls',
        marker: {
            size: 2
        },
        line: {
            width: 1
        }
    };
    tracesdata.push(result);
};
var layout = {
    title: {
        text: "Stock Price variations of companies",
        font: {
            family: 'Helvetica, Arial, sans-serif',
            color: "rgb(200, 200, 200)"
        }
    },
    yaxis: {
        autorange: true,
        showgrid: true,
        zeroline: true,
        gridcolor: "rgb(100, 100, 100)",
        gridwidth: 1,
        zerolinewidth: 2,
        type: "linear",
    },
    xaxis: {
        type: "category"
    },
    margin: {
        l: 40, r: 30, b: 80, t: 100
    },
    paper_bgcolor: "rgb(50, 50, 50)",
    plot_bgcolor: "rgb(50, 50, 50)",
    showlegend: false
}
// console.log(data);
return {
    data: tracesdata,
    layout: layout
}
```

### Day wise box plot example

```jsx
// Daywise stock price of a company
// console.log(data.series);

function formatTimestampToYYYYMMDD(timestamp) {
    const date = new Date(timestamp);

    const year = date.getFullYear();
    const month = (date.getMonth() + 1).toString().padStart(2, '0'); // Month is 0-indexed, so add 1
    const day = date.getDate().toString().padStart(2, '0');

    return `${year}-${month}-${day}`;
}

var dateDict = {};
for (var k = 0; k < data.series[0].fields[0].values.length; k++) {
    var dateKey = formatTimestampToYYYYMMDD(new Date(data.series[0].fields[0].values[k]));
    var val = data.series[0].fields[1].values[k];
    if (dateKey in dateDict) {
        dateDict[dateKey].push(val);
    }
    else {
        dateDict[dateKey] = [val];
    }
}

var xData = Object.keys(dateDict).sort();
var yData = xData.map(function (k) { return dateDict[k]; });

var colors = ['rgba(93, 164, 214, 0.5)', 'rgba(255, 144, 14, 0.5)', 'rgba(44, 160, 101, 0.5)', 'rgba(255, 65, 54, 0.5)', 'rgba(207, 114, 255, 0.5)', 'rgba(127, 96, 0, 0.5)', 'rgba(255, 140, 184, 0.5)', 'rgba(79, 90, 117, 0.5)', 'rgba(222, 223, 0, 0.5)'];

var tracesData = [];

for (var i = 0; i < xData.length; i++) {
    var result = {
        type: 'box',
        y: yData[i],
        name: xData[i],
        boxpoints: 'outlier',
        jitter: 0.5,
        whiskerwidth: 0.2,
        fillcolor: 'cls',
        marker: {
            size: 2
        },
        line: {
            width: 1
        }
    };
    tracesData.push(result);
};
var layout = {
    title: {
        text: "Daywise stock price of " + data.series[0].refId,
        font: {
            family: 'Helvetica, Arial, sans-serif',
            color: "rgb(200, 200, 200)"
        }
    },
    yaxis: {
        autorange: true,
        showgrid: true,
        zeroline: true,
        gridcolor: "rgb(100, 100, 100)",
        gridwidth: 1,
        zerolinewidth: 2,
        type: "linear",
    },
    xaxis: {
        "type": "date"
    },
    margin: {
        l: 40, r: 30, b: 80, t: 100
    },
    paper_bgcolor: "rgb(50, 50, 50)",
    plot_bgcolor: "rgb(50, 50, 50)",
    showlegend: false
}
// console.log(data);
return {
    data: tracesData,
    layout: layout
}
```

## References

- Grafana Plotly Panel - [https://grafana.com/grafana/plugins/ae3e-plotly-panel/](https://grafana.com/grafana/plugins/ae3e-plotly-panel/)
- Plotly JS code examples - [https://plotly.com/javascript/basic-charts/](https://plotly.com/javascript/basic-charts/)
- Plot JS data, layout and config explained - [https://plotly.com/javascript/plotlyjs-function-reference/](https://plotly.com/javascript/plotlyjs-function-reference/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NDMyMjQyNzJdfQ==
-->