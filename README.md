[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/ctvidic-whoop-mcp-server-badge.png)](https://mseep.ai/app/ctvidic-whoop-mcp-server)

# Whoop MCP Server
Python Package License: MIT Python 3.12

A Model Context Protocol (MCP) server that provides access to the Whoop API. It allows language models to query cycles, recovery, strain, and workout data from the Whoop API.

## Available Tools

The server exposes the following tools:

### Cycle Queries
- `get_cycle_collection(start_date: str, end_date: str)`: Get cycle data for a specific date range
- `get_latest_cycle()`: Get the most recent cycle data

### Recovery and Strain
- `get_recovery_data(start_date: str, end_date: str)`: Get recovery data for a specific date range
- `get_strain_data(start_date: str, end_date: str)`: Get strain data for a specific date range
- `get_average_strain(days: int = 7)`: Calculate average strain over specified number of days

### Profile and Authentication
- `get_profile()`: Get user profile information
- `check_auth_status()`: Check authentication status with Whoop API

Dates should be provided in ISO format (YYYY-MM-DD).

## Usage

You'll need Whoop credentials to use this server. The server uses email/password authentication with the Whoop API.

### Claude for Desktop

Update your `claude_desktop_config.json` (located in `~/Library/Application\ Support/Claude/claude_desktop_config.json` on macOS and `%APPDATA%/Claude/claude_desktop_config.json` on Windows) to include the following:

```json
{
    "mcpServers": {
        "Whoop": {
            "command": "python",
            "args": ["/path/to/whoop/src/whoop_server.py"],
            "cwd": "/path/to/whoop",
            "env": {
                "WHOOP_EMAIL": "your.email@example.com",
                "WHOOP_PASSWORD": "your_password"
            }
        }
    }
}
```

### HTTP API Server

The project also includes an HTTP API server that exposes the same functionality over HTTP endpoints. To run it:

```bash
./run_whoop_server.sh
```

## Example Queries

Once connected, you can ask Claude questions like:

- "What's my recovery score for today?"
- "Show me my strain data for the past week"
- "What's my average strain over the last 7 days?"
- "Get my latest cycle data"

## Error Handling

The server provides human-readable error messages for common issues:
- Invalid date formats
- API authentication errors
- Network connectivity problems
- Missing or invalid credentials

## Project Structure

```
whoop/
├── src/
│   ├── whoop_server.py      # MCP server implementation
│   └── whoop_http_server.py # HTTP API server implementation
├── config/
│   └── .env                 # Environment variables
├── requirements.txt         # Python dependencies
└── run_whoop_server.sh     # Script to run HTTP server
```

## License

This project is licensed under the MIT License - see the LICENSE file for details. 