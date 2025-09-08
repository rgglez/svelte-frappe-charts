# svelte-frappe-charts

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
![GitHub all releases](https://img.shields.io/github/downloads/rgglez/svelte-frappe-charts/total) 
![GitHub issues](https://img.shields.io/github/issues/rgglez/svelte-frappe-charts) 
![GitHub commit activity](https://img.shields.io/github/commit-activity/y/rgglez/svelte-frappe-charts)
![Downloads](https://img.shields.io/npm/dm/@rgglez/svelte-frappe-charts.svg)
![MadeWithSvelte](https://madewithsvelte.com/storage/repo-shields/2274-shield.svg)
![GitHub stars](https://img.shields.io/github/stars/rgglez/svelte-frappe-charts?style=social)
![GitHub forks](https://img.shields.io/github/forks/rgglez/svelte-frappe-charts?style=social)

Makes it easy to use [frappe-charts](https://frappe.io/charts) in your [Svelte](https://svelte.dev/) project.

## About this fork

This fork patches a security vulnerability and updates the Svelte dependency to **version 5+**. Take this into account.

## Installation

```bash
yarn add svelte @rgglez/svelte-frappe-charts

npm i -S svelte @rgglez/svelte-frappe-charts
```

## Dependencies

- **svelte** >= 5.0.0

## Usage

Use the chart in your Svelte project with ease:

```javascript
<script>
  import Chart from '@rgglez/svelte-frappe-charts';

  let data = {
    labels: ['Sun', 'Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
    datasets: [
      {
        values: [10, 12, 3, 9, 8, 15, 9]
      }
    ]
  };
</script>

<Chart data={data} type="line" />
```

The component API directly matches the [the configuration of `frappe-charts`](https://frappe.io/charts/docs/reference/configuration).

## Updating data

There are two ways to update data in a chart: either in adding and removing individual points, or updating the existing data with an entirely new set of data points.

## Updating individual data points

### addDataPoint

Add a data point to the chart, increasing the length of the dataset.

```javascript
<script>
  import Chart from '@rgglez/svelte-frappe-charts';

  let data = {
    labels: ['Sun', 'Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
    datasets: [
      {
        values: [10, 12, 3, 9, 8, 15, 9]
      }
    ]
  };

  let chartRef;

  function addDataPoint() {
    chartRef.addDataPoint('Wed', [30], 1);
  }
</script>

<Chart data={data} type="line" bind:this={chartRef} />

<button on:click={addDataPoint}>Add data point</button>
```

[More info on `addDataPoint`](https://frappe.io/charts/docs/reference/api#adddatapoint).

### removeDataPoint

Remove a data point from the chart, reducing the length of the dataset.

```javascript
<script>
  import Chart from '@rgglez/svelte-frappe-charts';

  let data = {
    labels: ['Sun', 'Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
    datasets: [
      {
        values: [10, 12, 3, 9, 8, 15, 9]
      }
    ]
  };

  let chartRef;

  function removeDataPoint() {
    chartRef.removeDataPoint(3); // Index of the item to remove
  }
</script>

<Chart data={data} type="line" bind:this={chartRef} />

<button on:click={removeDataPoint}>Remove data point</button>
```

[More info on `removeDataPoint`](https://frappe.io/charts/docs/reference/api#removedatapoint).

### Updating full data

Update the entire data, including annotations, by passing the entire new data object to update.

```javascript
<script>
  import Chart from '@rgglez/svelte-frappe-charts';

  let data = {
    labels: ['Sun', 'Mon', 'Tues', 'Wed', 'Thurs', 'Fri', 'Sat'],
    datasets: [
      {
        values: [10, 12, 3, 9, 8, 15, 9]
      }
    ]
  };

  let chartRef;

  function updateData() {
    data = {
      labels: ['Friday', 'Saturday', 'Sunday'],
      datasets: [
        {
          values: [300, 380, 275]
        }
      ]
    };
  }
</script>

<Chart data={data} type="line" bind:this={chartRef} />

<button on:click={updateData}>Update Chart</button>
```

### Chart navigation

[Chart navigation](https://frappe.io/charts/docs/update_state/navigation) can be used when the `isNavigable` prop is set on the `Chart` component.
Once it is set, the `data-select` event is propagated and can be handled in Svelte's standard ways (see the Events section of the tutorial and examples, and [the API docs](https://svelte.dev/docs#on_component_event)).

```javascript
<script>
  import Chart from "@rgglez/svelte-frappe-charts";

  let data = {
    labels: [ "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun", "Mon" ],
    datasets: [
      { values: [ 300, 250, 720, 560, 370, 610, 690, 410, 370, 480, 620, 260, 170, 510, 630, 710 ] },
    ],
  };

  const onDataSelect = (event) => {
    console.log("Data select event fired!", event);
    selected = event;
  };
  let selected;
</script>

<h1>Svelte Frappe charts navigation demo</h1>
<Chart {data} on:data-select={onDataSelect} isNavigable type="bar" />
```

### Exporting charts

You can easily export a chart ([see Exporting](https://frappe.io/charts/docs/exporting/images)) as an SVG by storing a reference to the `<Chart />` component, and then calling `exportChart` on it:

```javascript
<script>
  // ...

  let chartRef;
  const onExport = () => chartRef.exportChart();
</script>

<Chart data={data} type="line" bind:this={chartRef} />
<button on:click={onExport}>
  Export
</button>
```

## Contributing

[Issues](https://github.com/rgglez/svelte-frappe-charts/issues/new) and pull requests are greatly welcome!

## License

Original work by [Dave](http://himynameisdave.com). 

This fork: 

Copyright 2025 Rodolfo González González.

Licenced under [MIT](https://mit-license.org/). Read the [LICENSE](LICENSE) file.
