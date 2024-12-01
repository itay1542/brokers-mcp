# portfolio_service MCP server

A Model Context Protocol server implementing popular broker api's

## Supported APIs

- Currently only TradeStation API is supported *(partially)*

## Components

### Tools

The server implements five tools that are based on TradeStation API:
1. tradestation_get_bars - wraps the output of [TradeStation GetBars](https://api.tradestation.com/docs/specification#tag/MarketData/operation/GetBars) in a dataframe and returns it's `__str__`
2. tradestation_place_buy_order - Same as [TradeStation PlaceOrder](https://api.tradestation.com/docs/specification#tag/Order-Execution/operation/PlaceOrder) but only for buy orders
3. tradestation_place_sell_order - Same as [TradeStation PlaceOrder](https://api.tradestation.com/docs/specification#tag/Order-Execution/operation/PlaceOrder) but only for sell orders
4. tradestation_get_positions - Same as [TradeStation GetPositions](https://api.tradestation.com/docs/specification/#tag/Brokerage/operation/GetPositions)
5. tradestation_get_balances - Same as [TradeStation GetBalances](https://api.tradestation.com/docs/specification/#tag/Brokerage/operation/GetBalances)

see the exact schemas in the definition file [here](./src/portfolio_service/brokers/tradestation/tools.py)
## Configuration

The server is configured via environment variables:

```bash 
TRADESTATION_API_KEY="your_api_key"
TRADESTATION_API_SECRET="your_api_secret"
TS_REFRESH_TOKEN="your_refresh_token"
TS_ACCOUNT_ID="your_account_id"
```
If you are unsure about how to get the values of the environment variables, 
I have a blog post that explains it [here](https://medium.com/@itay1542/how-to-get-free-historical-intraday-equity-prices-with-code-examples-8f36fc57e1aa)

## Quickstart

### Install

#### Claude Desktop

On MacOS: `~/Library/Application\ Support/Claude/claude_desktop_config.json`

On Windows: `%APPDATA%/Claude/claude_desktop_config.json`

```
"mcpServers": {
  "portfolio_service": {
    "command": "uv",
    "args": [
      "--directory",
      "<path_to_project>/portfolio_service",
      "run",
      "portfolio_service"
    ]
  }
}
```

## Development

### Building and Publishing


1. Sync dependencies and update lockfile:
```bash
uv sync
```

### Debugging

Since MCP servers run over stdio, debugging can be challenging. For the best debugging
experience, we strongly recommend using the [MCP Inspector](https://github.com/modelcontextprotocol/inspector).


You can launch the MCP Inspector via [`npm`](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) with this command:

```bash
npx @modelcontextprotocol/inspector uv --directory <path_to_project>/portfolio_service run portfolio-service
```


Upon launching, the Inspector will display a URL that you can access in your browser to begin debugging.
