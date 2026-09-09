# PBI Example Contoso

This repository is a small Power BI Project (PBIP) used to practise agentic
development with Power BI Desktop, the Power BI modeling MCP, skills, tool
search, and tool calling. The project starts as a PBIP shell and keeps source
data locally so large files do not enter Git history.

## Project contents

- `PBI-Example-contoso.pbip`: Power BI Desktop entry point.
- `PBI-Example-contoso.SemanticModel/`: TMDL semantic-model definition.
- `PBI-Example-contoso.Report/`: PBIR report pages, metadata, and theme assets.
- `src/`: local CSV inputs loaded into the model.

The current source set contains eight CSV tables: `CurrencyExchange`,
`Customer`, `Date`, `OrderRows`, `Orders`, `Product`, `Sales`, and `Store`.
They cover currencies, customers, calendar attributes, orders and order lines,
products, sales, and stores. The model tables are imported from these files by
Power Query expressions that point to the local `src` directory.

The initial full refresh loaded 100,450 currency rates, 104,990 customers,
4,018 dates, 2,349,091 order rows, 980,666 orders, 2,517 products,
2,349,091 sales rows, and 74 stores.

## Relationships

The model uses `Orders` as the order header and hub for customer, store, and
date filtering. `Sales` and `OrderRows` connect to `Orders` by `OrderKey`, and
both connect to `Product` by `ProductKey`. `CurrencyExchange` connects to
`Date` by its date column. The delivery-date relationship is inactive so it can
be used explicitly in DAX without creating an ambiguous active date path.

The currency table also contains `FromCurrency` and `ToCurrency`; those fields
are intentionally not joined directly because they require a composite key or
a dedicated currency dimension.

## Finance measures

The `Measures` table contains five measures in the `Finance` display folder:
`Total Net Sales`, `Total Cost`, `Gross Profit`, `Gross Margin %`, and
`Average Order Value`. Numeric values are converted with `VALUE` inside
`SUMX` because the initial CSV import stores source columns as text.

## Working locally

Open `PBI-Example-contoso.pbip` in Power BI Desktop. When source files change,
refresh the model and check the affected report pages. For automated model
work, connect the open Desktop instance with the Power BI modeling MCP and use
its table and DAX operations to inspect or validate changes.

The CSV files are deliberately ignored by `.gitignore`, together with
`src-backup/`, Power BI cache files, and local settings. Keep those folders on
the local machine and do not commit credentials or generated archives.

See [AGENTS.md](AGENTS.md) for contributor workflow, style, validation, and
pull-request guidance.
