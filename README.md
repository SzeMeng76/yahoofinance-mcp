# Yahoo Finance MCP Server

A Model Context Protocol (MCP) server that provides financial data from Yahoo Finance. This server enables Claude to access real-time stock quotes, market data, and historical stock information without requiring API keys.

## Features

- **Stock Quotes**: Get current stock price, change, range, volume, and other key metrics
- **Market Indices**: Retrieve data for major market indices like S&P 500, Dow Jones, NASDAQ
- **Historical Data**: Fetch and analyze historical stock data with customizable time periods and intervals
- **Rate limiting**: Built-in rate limiting to ensure reliable access to Yahoo Finance

## Installation and Running

### Method 1: Using NPX (Easiest)

The simplest way to run the server is using NPX:

```bash
npx @modelcontextprotocol/server-yahoofinance
```

### Method 2: Local Installation

If you prefer to install the package locally:

```bash
# Install globally
npm install -g @modelcontextprotocol/server-yahoofinance

# Run the server
mcp-server-yahoofinance
```

### Method 3: Docker

For containerized deployment:

```bash
# Build the Docker image
docker build -t yahoofinance-mcp .

# Run the container
docker run -i --rm yahoofinance-mcp
```

### Method 4: From Source

To run from source:

```bash
# Clone the repository
git clone https://github.com/jasontoo/yahoofinance-mcp.git
cd yahoofinance-mcp

# Install dependencies
npm install

# Build the project
npm run build

# Run the server
node dist/index.js
```

## Integration with Claude Desktop

1. Download and install [Claude Desktop](https://claude.ai/download)
2. Create or modify the Claude Desktop configuration file:
   - Mac: `~/Library/Application Support/Claude/claude_desktop_config.json`
   - Windows: `%APPDATA%\Claude\claude_desktop_config.json`

3. Add the Yahoo Finance server configuration:

```json
{
  "mcpServers": {
    "yahoofinance": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-yahoofinance"
      ]
    }
  }
}
```

For local installation:

```json
{
  "mcpServers": {
    "yahoofinance": {
      "command": "mcp-server-yahoofinance"
    }
  }
}
```

For Docker:

```json
{
  "mcpServers": {
    "yahoofinance": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "yahoofinance-mcp"
      ]
    }
  }
}
```

4. Restart Claude Desktop

## Available Tools

### yahoo_stock_quote
Gets current stock quote information from Yahoo Finance.

**Parameters:**
- `symbol`: Stock ticker symbol (e.g., AAPL, MSFT, TSLA)

### yahoo_market_data
Gets current market data from Yahoo Finance for major indices.

**Parameters:**
- `indices` (optional): List of index symbols to fetch (default: ["^GSPC", "^DJI", "^IXIC"])

### yahoo_stock_history
Gets historical stock data from Yahoo Finance.

**Parameters:**
- `symbol`: Stock ticker symbol
- `period` (optional): Time period ("1d", "5d", "1mo", "3mo", "6mo", "1y", "2y", "5y", "10y", "ytd", "max")
- `interval` (optional): Data interval ("1m", "2m", "5m", "15m", "30m", "60m", "90m", "1h", "1d", "5d", "1wk", "1mo", "3mo")

## Example Prompts

- "What's the current price of AAPL stock?"
- "How has Tesla stock performed over the past month?"
- "Show me the current values of major market indices."
- "What's the stock price history for MSFT over the last year?"
- "Compare the performance of GOOGL and AMZN over the past 3 months."
- "What's the 52-week range for NVDA?"
- "How has the S&P 500 performed today?"

## Limitations

- The server relies on Yahoo Finance's public data and may be affected by changes to their API.
- Rate limiting is implemented to avoid being blocked by Yahoo Finance, so rapid sequential requests may be throttled.
- The server does not require an API key, but this means it's accessing Yahoo Finance as a regular user.

## Troubleshooting

If you encounter issues:

1. Check for error messages in the Claude Desktop logs
2. Ensure you have an active internet connection
3. Verify the ticker symbols are correct
4. If you see rate limiting errors, wait a few minutes before trying again

## License

This project is licensed under the MIT License - see the LICENSE file for details.
