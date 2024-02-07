# vue-expandable-table

`vue-expandable-table` is a highly customizable Vue.js component designed for displaying tabular data with the added functionality of expandable rows. It supports customizable styling for borders, cell padding, header and data cell backgrounds, and expandable row backgrounds. This component is perfect for applications requiring detailed data presentation with the capability to expand rows for additional information.

## Installation

Install the component using npm:

```bash
npm install vue-expandable-table
```

## Usage

To use the component in your project, import it and then include it in your component using the script setup syntax. Define your table data and columns as shown in the example below:

```vue
<script setup>
import { ExpandableTable } from 'vue-expandable-table';
import "vue-expandable-table/style.css"

const data = [
  { name: 'Luke', homeWorld: 'Tatooine', age: 19, birthDate: '1996-01-01' },
  { name: 'Leia', homeWorld: 'Alderaan', age: 19, birthDate: '1994-01-02' }
];

const columns = [
  { label: 'Name', field: 'name' },
  { label: 'Age', field: 'age' },
  { label: 'Homeworld', field: 'homeWorld' }
];
</script>

<template>
  <expandable-table :data="data" :columns="columns"></expandable-table>
</template>
```

Note that data values not included in columns will be stored on an expandable row.

## Props Configuration

| Prop                        | Type    | Default       | Description                                           |
|-----------------------------|---------|---------------|-------------------------------------------------------|
| `customBorderColor`         | String  | `'#1D3557'`   | Sets the border color of the table.                   |
| `thBackgroundColor`         | String  | `'#A8DADC'`   | Background color for table headers.                   |
| `tdBackgroundColor`         | String  | `'#F1FAEE'`   | Background color for table cells.                     |
| `expandableBackgroundColor` | String  | `'#fefae0'`   | Background color for expandable row sections.         |
| `borderWidth`               | String  | `'1px'`       | Border width of the table cells.                      |
| `tdPaddingY`                | String  | `'12px'`      | Vertical padding for table cells.                     |
| `tdPaddingX`                | String  | `'12px'`      | Horizontal padding for table cells.                   |
| `thPaddingY`                | String  | `'12px'`      | Vertical padding for table headers.                   |
| `thPaddingX`                | String  | `'12px'`      | Horizontal padding for table headers.                 |
| `expansiblePaddingX`        | String  | `'12px'`      | Horizontal padding for the expandable section.        |
| `expansiblePaddingY`        | String  | `'12px'`      | Vertical padding for the expandable section.          |
| `fullWidth`                 | Boolean | `'false'`     | Sets the width to 100%.                               |
| `data`                      | Array   | `'null'`      | The data to display in the table.                     |
| `columns`                   | Array   | `'null'`      | Configuration for the table columns.                  |

