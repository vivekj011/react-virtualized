FlexTable
---------------

Table component with fixed headers and virtualized rows for improved performance with large data sets.
This component expects explicit width, height, and padding parameters.

### Prop Types
| Property | Type | Required? | Description |
|:---|:---|:---:|:---|
| children | [FlexColumn](FlexColumn.md) | ✓ | One or more FlexColumns describing the data displayed in this table |
| className | String |  | Optional custom CSS class name to attach to root `FlexTable` element. |
| disableHeader | Boolean |  | Do not render the table header (only the rows) |
| estimatedRowSize | Number |  | Used to estimate the total height of a `FlexTable` before all of its rows have actually been measured. The estimated total height is adjusted as rows are rendered. |
| headerClassName | String |  | CSS class to apply to all column headers |
| headerHeight | Number | ✓ | Fixed height of header row |
| headerStyle | Object |  | Optional custom inline style to attach to table header columns. |
| height | Number | ✓ | Fixed/available height for out DOM element |
| noRowsRenderer |  | Function | Callback used to render placeholder content when :rowCount is 0 |
| onHeaderClick |  | Function | Callback invoked when a user clicks on a table header. `(dataKey: string, columnData: any): void` |
| onRowClick |  | Function | Callback invoked when a user clicks on a table row. `({ index: number }): void` |
| onRowMouseOut |  | Function | Callback invoked when the mouse leaves a table row. `({ index: number }): void` |
| onRowMouseOver |  | Function | Callback invoked when a user moves the mouse over a table row. `({ index: number }): void` |
| onRowsRendered |  | Function | Callback invoked with information about the slice of rows that were just rendered: `({ overscanStartIndex: number, overscanStopIndex: number, startIndex: number, stopIndex: number }): void` |
| overscanRowCount |  | Number | Number of rows to render above/below the visible bounds of the list. This can help reduce flickering during scrolling on certain browers/devices. |
| onScroll | Function |  | Callback invoked whenever the scroll offset changes within the inner scrollable region: `({ clientHeight: number, scrollHeight: number: number, scrollTop: number }): void` |
| rowClassName | String or Function |  | CSS class to apply to all table rows (including the header row). This value may be either a static string or a function with the signature `({ index: number }): string`. Note that for the header row an index of `-1` is provided. |
| rowCount | Number | ✓ | Number of rows in table. |
| rowGetter | Function | ✓ | Callback responsible for returning a data row given an index. `({ index: int }): any` |
| rowHeight | Number or Function | ✓ | Either a fixed row height (number) or a function that returns the height of a row given its index: `({ index: number }): number` |
| rowStyle | Object |  | Optional custom inline style to attach to table rows. |
| scrollToAlignment | String |  | Controls the alignment scrolled-to-rows. The default ("_auto_") scrolls the least amount possible to ensure that the specified row is fully visible. Use "_start_" to always align rows to the top of the list and "_end_" to align them bottom. Use "_center_" to align them in the middle of container. |
| scrollToIndex | Number |  | Row index to ensure visible (by forcefully scrolling if necessary) |
| scrollTop | Number |  | Vertical offset |
| sort | Function |  | Sort function to be called if a sortable header is clicked. `({ sortBy: string, sortDirection: SortDirection }): void` |
| sortBy | String |  | Data is currently sorted by this `dataKey` (if it is sorted at all) |
| sortDirection | [SortDirection](SortDirection.md) |  | Data is currently sorted in this direction (if it is sorted at all) |
| style | Object |  | Optional custom inline style to attach to root `FlexTable` element. |
| width | Number | ✓ | Width of the table |

### Public Methods

##### measureAllRows
Pre-measure all rows in a `FlexTable`.

Typically rows are only measured as needed and estimated heights are used for cells that have not yet been measured.
This method ensures that the next call to getTotalSize() returns an exact size (as opposed to just an estimated one).

##### recomputeRowHeights
Recompute row heights and offsets.

VirtualScroll has no way of knowing when its underlying list data has changed since it only receives a `rowHeight` property. If the `rowHeight` is a number it can compare before and after values but if it is a function that comparison is error prone. In the event that a dynamic `rowHeight` function is in use and the row heights have changed this function should be manually called by the "smart" container parent.

### Class names

The FlexTable component supports the following static class names

| Property | Description |
|:---|:---|
| FlexTable | Main (outer) element |
| FlexTable__headerColumn | Header cell (similar to `thead > tr > th`) |
| FlexTable__headerRow | Header row (similar to `thead > tr`) |
| FlexTable__headerTruncatedText | Element within header cell responsible for truncating text |
| FlexTable__row | Table row (akin to `tbody > tr`) |
| FlexTable__rowColumn | Table column (akin to `tbody > tr > td`) |
| FlexTable__sortableHeaderColumn | Applied to header columns that are sortable |
| FlexTable__sortableHeaderIcon | SVG sort indicator |
| FlexTable__truncatedColumnText | Element within table column responsible for truncating text |

### Examples

Below is a very basic `FlexTable` example. This table has only 2 columns, each containing a simple string. Both have a fixed width and neither is sortable. [See here](../source/FlexTable/FlexTable.example.js) for a more full-featured example including custom cell renderers, sortable headers, and more.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { FlexTable, FlexColumn } from 'react-virtualized';
import 'react-virtualized/styles.css'; // only needs to be imported once

// Table data as a array of objects
const list = [
  { name: 'Brian Vaughn', description: 'Software engineer' }
  // And so on...
];

// Render your table
ReactDOM.render(
  <FlexTable
    width={300}
    height={300}
    headerHeight={20}
    rowHeight={30}
    rowCount={list.length}
    rowGetter={({index}) => list[index]}
  >
    <FlexColumn
      label='Name'
      dataKey='name'
      width={100}
    />
    <FlexColumn
      width={200}
      label='Description'
      dataKey='description'
    />
  </FlexTable>,
  document.getElementById('example')
);
```
