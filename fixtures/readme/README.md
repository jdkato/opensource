# chartcli

[![CI](https://github.com/example/chartcli/actions/workflows/ci.yml/badge.svg)](https://github.com/example/chartcli/actions)

chartcli is a command-line tool that reads CSV files from disk or standard input and simply draws them as bar, line, or scatter charts.

## Usage

Obviously, you need a CSV file first. Pass it to the tool:

```sh
chartcli data.csv
```

| Flag | Meaning |
| ---- | ------- |
| `--width` | Chart width, in columns. |
| `--height` | Chart height, in rows. |
| `--color` | Bar color. |
| `--title` | Chart title. |
| `--legend` | Show a legend. |
| `--log` | Use a log scale. |
| `-q` | Print nothing but the chart. |

### Choosing a chart

The tool picks a chart type from the shape of the data. A file with one
text column and one number column becomes a bar chart, with a bar for each
row. A file whose first column holds dates or times becomes a line chart,
with one line for each number column after it. A file with two number
columns and nothing else becomes a scatter chart, with one point for each
row. When the shape fits more than one type, the tool picks the bar chart,
since it reads well at any width. To choose the type yourself, pass the
type as the first argument, before the file name. The tool then reads the
columns the way that type expects, and stops with a message when the file
does not fit.

### Reading the input

The first row of the file is read as a header, and its cells name the
columns. When the first row holds numbers, the tool treats it as data and
names the columns by position instead. Cells are split on commas unless
the file name ends in a tab extension, in which case they are split on
tabs. Quoted cells may hold commas and line breaks. Empty cells are read
as missing values, and a missing value leaves a gap in a line chart and
drops the point from a scatter chart. Numbers may use a period or a comma
as the decimal mark, and the tool guesses which from the first numeric
cell it sees. Text in a number column stops the run with the row and
column it came from.

### Sizing the chart

By default the chart fills the width of the terminal and is a third as
tall as it is wide. When the output is not a terminal, such as a pipe or a
file, the tool falls back to eighty columns and twenty rows. Labels on the
left axis take as much room as the longest label needs, up to a quarter
of the width, and longer labels are cut with an ellipsis. Bars are drawn
with block characters, so a bar can end partway through a cell. Lines are
drawn with braille characters, which give each cell eight dots and make a
line look smooth at small sizes. The scale on each axis starts at zero
for a bar chart and at the smallest value for the other types.

### Colors

Colors follow the terminal theme. Each series takes the next color from a
palette of eight that reads on both dark and light backgrounds. When the
terminal reports that it has no color support, or when the output is not
a terminal, the chart is drawn in one color and each series uses its own
character instead. The environment variable that turns color off in other
tools turns it off here too. A legend lists each series with its color or
character, and sits below the chart unless the chart is too short to
leave room for it, in which case it moves to the right.

### Large files

The tool reads the file once and keeps only what the chart needs. A bar
chart with more rows than the height allows keeps the largest values and
groups the rest into one bar at the bottom, labeled with the number of
rows it holds. A line chart with more points than the width allows takes
the average of the points that share a column. A scatter chart keeps every
point and draws the densest cells darker. Files of a few million rows
draw in about a second on a laptop, and the memory the tool uses grows
with the size of the chart rather than the size of the file.

### Support

Read the docs before asking. Questions already answered there will be closed without comment.

## Installation

Download a binary from the releases page. It's easy.

## License

MIT © Jane Doe

## Sponsors

Thanks, guys, for keeping the lights on.
