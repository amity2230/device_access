# Device Access MCP Server

An MCP (Model Context Protocol) server that lets AI assistants like Claude interact with Cisco network devices over SSH. Built with [FastMCP](https://github.com/jlowin/fastmcp) and [Netmiko](https://github.com/ktbyers/netmiko).

## Features

- **List Devices** — View all network devices in your inventory
- **Run Commands** — Execute Cisco IOS show commands on devices via SSH
- **Get Device Info** — Retrieve connection details for any device
- **AI Command Suggestions** — Get AI-suggested commands based on your intent (powered by OpenAI)
- **AI Output Analysis** — Get AI-powered analysis of command output

## Prerequisites

- Python 3.13+
- Network devices reachable via SSH
- OpenAI API key (for AI-powered features)

## Installation

```bash
git clone https://github.com/amity2230/device_access.git
cd device_access
```

### Using uv (recommended)

```bash
uv sync
```

### Using pip

```bash
pip install fastmcp netmiko pyyaml openai python-dotenv
```

## Configuration

### 1. Set up environment variables

```bash
cp .env.example .env
```

Edit `.env` and add your OpenAI API key:

```
OPENAI_API_KEY=your-openai-api-key-here
```

### 2. Configure your device inventory

Edit `devices.yaml` with your network device details:

```yaml
vIOS-R1:
  host: 192.168.1.101
  device_type: cisco_ios
  username: your_username
  password: your_password
  description: "vIOS Router 1"
```

Supported `device_type` values: `cisco_ios`, `cisco_nxos`, `cisco_xr`, `arista_eos`, `juniper_junos`, `linux`, etc.

## Usage

### Run the MCP server

```bash
python device_mcp.py
```

### Use with Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "DeviceCommands": {
      "command": "python",
      "args": ["/path/to/device_access/device_mcp.py"]
    }
  }
}
```

### Available MCP Tools

| Tool | Description |
|------|-------------|
| `list_devices()` | List all devices in the inventory |
| `run_command(device_name, command)` | Execute a CLI command on a device |
| `get_device_info(device_name)` | Get connection details for a device |
| `suggest_commands(device_name, intent)` | AI-suggested commands for your intent |
| `analyze_output(device_name, command, output)` | AI analysis of command output |

## Project Structure

```
device_access/
├── device_mcp.py       # Main MCP server with tool definitions
├── devices.yaml        # Network device inventory
├── pyproject.toml      # Project dependencies
├── .env.example        # Environment variable template
├── .gitignore          # Git ignore rules
└── README.md           # This file
```

## License

MIT
