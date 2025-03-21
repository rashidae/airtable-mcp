# Airtable MCP

![Airtable](https://img.shields.io/badge/Airtable-18BFFF?style=for-the-badge&logo=Airtable&logoColor=white)
[![smithery badge](https://smithery.ai/badge/@rashidazarang/airtable-mcp)](https://smithery.ai/server/@rashidazarang/airtable-mcp)

> Connect your AI tools directly to Airtable. Query, create, update, and delete records using natural language. Features include base management, table operations, schema manipulation, record filtering, and data migration—all through a standardized MCP interface compatible with Cursor, Claude Desktop, Cline, Zed, and other Claude-powered editors.

This application is a powerful Airtable integration tool that enables AI-powered applications via Anthropic's Model Context Protocol (MCP) to access and manipulate Airtable data directly from your IDE.

## Features

- **Base Management**: List and select Airtable bases
- **Table Operations**: Browse tables, fields, and records
- **Data Access**: Read, create, update, and delete records
- **Schema Management**: Export, compare, and update schemas
- **Command-line Configuration**: Use API tokens directly through command-line parameters
- **NPX Compatible**: Easy installation with a single command
- **Smithery Integration**: One-click installation via Smithery

## Architecture

There are two core components used to access and manipulate Airtable data:

1. **Airtable MCP Server**: A Python server that provides standardized tools for AI clients to interact with Airtable.
2. **MCP Client**: Any client that supports the Model Context Protocol (Cursor, Claude Desktop, Cline, Zed, etc.).

```
┌─────────────┐     ┌──────────────┐     ┌───────────────┐
│  MCP Client │ ──► │  Airtable    │ ──► │   Airtable    │
│  (e.g.      │ ◄── │  MCP Server  │ ◄── │     API       │
│   Cursor)   │     │              │     │               │
└─────────────┘     └──────────────┘     └───────────────┘
```

Model Context Protocol (MCP) is a capability supported by Anthropic AI models that allows you to create custom tools for any compatible client. MCP clients like Claude Desktop, Cursor, Cline, or Zed can run an MCP server which "teaches" these clients about new tools they can use.

## Important Updates (March 2025)

This MCP has been updated to work with the latest MCP SDK version. The new implementation uses:

- **inspector_server.py**: A new server implementation compatible with MCP SDK 1.4.1+
- Updated configuration for both Cursor and Smithery integration
- Python 3.10+ compatibility

## Installation

### Prerequisites

- Node.js 14+
- Python 3.10+ (automatically detected)
- Airtable API token
- A compatible MCP client (Cursor, Claude Desktop, etc.)

### Smithery Installation (Recommended)

The easiest way to install:

1. Visit [Smithery](https://smithery.ai)
2. Search for "@rashidazarang/airtable-mcp"
3. Click "Install" and follow the prompts

### Quick Setup with NPX (Alternative)

Another fast way to get started:

```bash
# Install globally
npm install -g airtable-mcp

# Or run directly with npx
npx airtable-mcp --token "your_airtable_token" --base "your_base_id"
```

### MCP Client Integration

For detailed instructions on integrating with specific MCP clients, see:

- [Claude Integration Guide](CLAUDE_INTEGRATION.md) - Setup instructions for Claude Desktop, Cursor, Cline, and other clients
- [Smithery Setup](https://smithery.ai/server/@rashidazarang/airtable-mcp) - One-click installation via Smithery

### Configure Your MCP Client

For Cursor, update your `~/.cursor/mcp.json` file:

```json
{
  "mcpServers": {
    "airtable-tools": {
      "command": "npx",
      "args": [
        "airtable-mcp",
        "--token", "your_airtable_token",
        "--base", "your_base_id"
      ]
    }
  }
}
```

Restart your MCP client to load the new tools.

### Manual Installation (Advanced)

If you prefer to clone the repository and install manually:

1. Clone this repository:
   ```bash
   git clone https://github.com/rashidazarang/airtable-mcp.git
   cd airtable-mcp
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run the server:
   ```bash
   python3.10 inspector_server.py --token "your_airtable_token" --base "your_base_id"
   ```

## Testing Your Setup

To verify your Airtable connection works correctly, you can use the included test script:

```bash
python3.10 test_client.py
```

This will directly test your Airtable API access and list your bases and table schemas.

## Available Tools

| Tool Name | Description |
|-----------|-------------|
| `list_bases` | List all accessible Airtable bases |
| `list_tables` | List all tables in the specified or default base |
| `list_records` | List records from a table with optional filtering |
| `get_record` | Get a specific record from a table |
| `create_records` | Create records in a table from JSON string |
| `update_records` | Update records in a table from JSON string |
| `set_base_id` | Set the current Airtable base ID |

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.