# chartcli

[![CI](https://github.com/example/chartcli/actions/workflows/ci.yml/badge.svg)](https://github.com/example/chartcli/actions)

Draw CSV files as charts in the terminal.

chartcli reads CSV files from disk or standard input and draws them as bar,
line, or scatter charts, sized to the window.

## Install

Download a binary from the [releases page](https://github.com/example/chartcli/releases),
or build it with Go:

```sh
go install example.com/chartcli@latest
```

## Usage

Pass a CSV file to the tool:

```sh
chartcli data.csv
```

The tool picks a chart type from the shape of the data. To choose one, name
it first, as in `chartcli line data.csv`. The
[documentation](https://example.com/chartcli/docs) lists every option.

## Contributing

Ask questions in [Discussions](https://github.com/example/chartcli/discussions).
Pull requests are welcome; see [CONTRIBUTING.md](CONTRIBUTING.md) to get
started.

## License

MIT © Jane Doe

---

[Docs](https://example.com/chartcli/docs) · [Sponsors](https://example.com/chartcli/sponsors)
